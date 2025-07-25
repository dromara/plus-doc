# 异常处理

- - -

`@/utils/request.ts` 是基于 `axios` 的封装，便于统一处理 POST，GET
等请求参数，请求头，以及错误提示信息等。它封装了全局 `request拦截器`、`response拦截器`、`统一的错误处理`、`统一做了超时处理`、`baseURL`设置等。
如果有自定义错误码可以在`RespEnum.ts`中设置对应 `enum` 值。

```typescript
import axios, {AxiosResponse, InternalAxiosRequestConfig} from 'axios';
import {useUserStore} from '@/store/modules/user';
import {getToken} from '@/utils/auth';
import {tansParams, blobValidate} from '@/utils/ruoyi';
import cache from '@/plugins/cache';
import {HttpStatus} from '@/enums/RespEnum';
import {errorCode} from '@/utils/errorCode';
import {LoadingInstance} from 'element-plus/es/components/loading/src/loading';
import FileSaver from 'file-saver';
import {getLanguage} from '@/lang';
import {encryptBase64, encryptWithAes, generateAesKey, decryptWithAes, decryptBase64} from '@/utils/crypto';
import {encrypt, decrypt} from '@/utils/jsencrypt';
import router from "@/router";

const encryptHeader = 'encrypt-key';
let downloadLoadingInstance: LoadingInstance;
// 是否显示重新登录
export const isRelogin = {show: false};
export const globalHeaders = () => {
    return {
        Authorization: 'Bearer ' + getToken(),
        clientid: import.meta.env.VITE_APP_CLIENT_ID
    };
};

axios.defaults.headers['Content-Type'] = 'application/json;charset=utf-8';
axios.defaults.headers['clientid'] = import.meta.env.VITE_APP_CLIENT_ID;
// 创建 axios 实例
const service = axios.create({
    baseURL: import.meta.env.VITE_APP_BASE_API,
    timeout: 50000
});

// 请求拦截器
service.interceptors.request.use(
    (config: InternalAxiosRequestConfig) => {
        // 对应国际化资源文件后缀
        config.headers['Content-Language'] = getLanguage();

        const isToken = config.headers?.isToken === false;
        // 是否需要防止数据重复提交
        const isRepeatSubmit = config.headers?.repeatSubmit === false;
        // 是否需要加密
        const isEncrypt = config.headers?.isEncrypt === 'true';

        if (getToken() && !isToken) {
            config.headers['Authorization'] = 'Bearer ' + getToken(); // 让每个请求携带自定义token 请根据实际情况自行修改
        }
        // get请求映射params参数
        if (config.method === 'get' && config.params) {
            let url = config.url + '?' + tansParams(config.params);
            url = url.slice(0, -1);
            config.params = {};
            config.url = url;
        }

        if (!isRepeatSubmit && (config.method === 'post' || config.method === 'put')) {
            const requestObj = {
                url: config.url,
                data: typeof config.data === 'object' ? JSON.stringify(config.data) : config.data,
                time: new Date().getTime()
            };
            const sessionObj = cache.session.getJSON('sessionObj');
            if (sessionObj === undefined || sessionObj === null || sessionObj === '') {
                cache.session.setJSON('sessionObj', requestObj);
            } else {
                const s_url = sessionObj.url; // 请求地址
                const s_data = sessionObj.data; // 请求数据
                const s_time = sessionObj.time; // 请求时间
                const interval = 500; // 间隔时间(ms)，小于此时间视为重复提交
                if (s_data === requestObj.data && requestObj.time - s_time < interval && s_url === requestObj.url) {
                    const message = '数据正在处理，请勿重复提交';
                    console.warn(`[${s_url}]: ` + message);
                    return Promise.reject(new Error(message));
                } else {
                    cache.session.setJSON('sessionObj', requestObj);
                }
            }
        }
        if (import.meta.env.VITE_APP_ENCRYPT === 'true') {
            // 当开启参数加密
            if (isEncrypt && (config.method === 'post' || config.method === 'put')) {
                // 生成一个 AES 密钥
                const aesKey = generateAesKey();
                config.headers[encryptHeader] = encrypt(encryptBase64(aesKey));
                config.data = typeof config.data === 'object' ? encryptWithAes(JSON.stringify(config.data), aesKey) : encryptWithAes(config.data, aesKey);
            }
        }
        // FormData数据去请求头Content-Type
        if (config.data instanceof FormData) {
            delete config.headers['Content-Type'];
        }
        return config;
    },
    (error: any) => {
        return Promise.reject(error);
    }
);

// 响应拦截器
service.interceptors.response.use(
    (res: AxiosResponse) => {
        if (import.meta.env.VITE_APP_ENCRYPT === 'true') {
            // 加密后的 AES 秘钥
            const keyStr = res.headers[encryptHeader];
            // 加密
            if (keyStr != null && keyStr != '') {
                const data = res.data;
                // 请求体 AES 解密
                const base64Str = decrypt(keyStr);
                // base64 解码 得到请求头的 AES 秘钥
                const aesKey = decryptBase64(base64Str.toString());
                // aesKey 解码 data
                const decryptData = decryptWithAes(data, aesKey);
                // 将结果 (得到的是 JSON 字符串) 转为 JSON
                res.data = JSON.parse(decryptData);
            }
        }
        // 未设置状态码则默认成功状态
        const code = res.data.code || HttpStatus.SUCCESS;
        // 获取错误信息
        const msg = errorCode[code] || res.data.msg || errorCode['default'];
        // 二进制数据则直接返回
        if (res.request.responseType === 'blob' || res.request.responseType === 'arraybuffer') {
            return res.data;
        }
        if (code === 401) {
            // prettier-ignore
            if (!isRelogin.show) {
                isRelogin.show = true;
                ElMessageBox.confirm('登录状态已过期，您可以继续留在该页面，或者重新登录', '系统提示', {
                    confirmButtonText: '重新登录',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(() => {
                    isRelogin.show = false;
                    useUserStore().logout().then(() => {
                        router.replace({
                            path: '/login',
                            query: {
                                redirect: encodeURIComponent(router.currentRoute.value.fullPath || '/')
                            }
                        })
                    });
                }).catch(() => {
                    isRelogin.show = false;
                });
            }
            return Promise.reject('无效的会话，或者会话已过期，请重新登录。');
        } else if (code === HttpStatus.SERVER_ERROR) {
            ElMessage({message: msg, type: 'error'});
            return Promise.reject(new Error(msg));
        } else if (code === HttpStatus.WARN) {
            ElMessage({message: msg, type: 'warning'});
            return Promise.reject(new Error(msg));
        } else if (code !== HttpStatus.SUCCESS) {
            ElNotification.error({title: msg});
            return Promise.reject('error');
        } else {
            return Promise.resolve(res.data);
        }
    },
    (error: any) => {
        let {message} = error;
        if (message == 'Network Error') {
            message = '后端接口连接异常';
        } else if (message.includes('timeout')) {
            message = '系统接口请求超时';
        } else if (message.includes('Request failed with status code')) {
            message = '系统接口' + message.substr(message.length - 3) + '异常';
        }
        ElMessage({message: message, type: 'error', duration: 5 * 1000});
        return Promise.reject(error);
    }
);

// 通用下载方法
export function download(url: string, params: any, fileName: string) {
    downloadLoadingInstance = ElLoading.service({text: '正在下载数据，请稍候', background: 'rgba(0, 0, 0, 0.7)'});
    // prettier-ignore
    return service.post(url, params, {
        transformRequest: [
            (params: any) => {
                return tansParams(params);
            }
        ],
        headers: {'Content-Type': 'application/x-www-form-urlencoded'},
        responseType: 'blob'
    }).then(async (resp: any) => {
        const isLogin = blobValidate(resp);
        if (isLogin) {
            const blob = new Blob([resp]);
            FileSaver.saveAs(blob, fileName);
        } else {
            const resText = await resp.data.text();
            const rspObj = JSON.parse(resText);
            const errMsg = errorCode[rspObj.code] || rspObj.msg || errorCode['default'];
            ElMessage.error(errMsg);
        }
        downloadLoadingInstance.close();
    }).catch((r: any) => {
        console.error(r);
        ElMessage.error('下载文件出现错误，请联系管理员！');
        downloadLoadingInstance.close();
    });
}

// 导出 axios 实例
export default service;

```

> **提示**
>
> hraders中的参数说明：
>
> 1. **isToken**
>    * 类型: boolean
>    * 默认值: true
>    * 作用: 控制是否在请求头中添加 Authorization 字段。
>    * 详细说明:
>      * 如果 isToken 为 false，则不会在请求头中添加 Authorization 字段。
>      * 如果 isToken 为 true 或未指定，则会在请求头中添加 Authorization 字段，并附带从 getToken() 函数获取到的 token。
> 2. **isEncrypt**
>    * 类型: boolean
>    * 默认值: false
>    * 作用: 控制是否对请求数据进行加密。
>    * 详细说明:
>      * 如果 isEncrypt 为 'true'，并且项目配置中开启了参数加密（即 import.meta.env.VITE_APP_ENCRYPT 为 'true'），则会对 POST 和 PUT 请求的数据进行 AES 加密。
>      * 加密过程包括生成一个 AES 密钥，并将密钥和加密后的数据分别添加到请求头和请求体中。
> 3. **repeatSubmit**
>    * 类型: boolean
>    * 默认值: true
>    * 作用: 控制是否防止数据重复提交。
>    * 详细说明:
>      * 如果 repeatSubmit 为 false，则不进行重复提交检查。
>      * 如果 repeatSubmit 为 true 或未指定，则会对 POST 和 PUT 请求进行重复提交检查。
>      * 检查逻辑：
>      * 将当前请求的 URL、数据和时间存储在会话缓存中。
>      * 在每次请求时，检查会话缓存中是否存在相同的请求数据，并且请求时间间隔小于 500毫秒（默认，可在请求拦截其中修改）。
>      * 如果检测到重复提交，会返回一个错误提示。
>
> ```typescript
> export function login(data: LoginData): AxiosPromise<LoginResult> {
>  const params = {
>    ...data,
>    clientId: data.clientId || clientId,
>    grantType: data.grantType || 'password'
> };
> return request({
> url: '/auth/login',
>    headers: {
>      isToken: false,
>      isEncrypt: true,
>      repeatSubmit: false
>    },
>    method: 'post',
>    data: params
>  });
> }
> ```