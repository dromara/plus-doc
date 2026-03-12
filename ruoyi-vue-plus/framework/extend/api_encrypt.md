# API 加解密
- - -

## 核心说明

API 加密主要用于防止传输过程被拦截（如代理劫持）。  
前端必须解密后展示，因此无论公钥/私钥最终都可被用于解密。  
由于 JS 环境缺少“公钥解密”的通用实现，因此前端使用私钥进行解密。

如有更优方案，欢迎反馈与共建。

## 1. 使用注解 `@ApiEncrypt`

- 标注该注解的接口，请求参数必须加密
- `response` 参数控制响应是否加密，默认 `false`
- 加解密逻辑由过滤器处理：`org.dromara.common.encrypt.filter.CryptoFilter`

## 2. 配置方式

后端配置：`application.yml`

![输入图片说明](https://foruda.gitee.com/images/1701131796468961065/83c464cd_4959041.png "屏幕截图")

前端配置：`.env.development` / `.env.production`

![输入图片说明](https://foruda.gitee.com/images/1709533252413969800/1d0dff25_1766278.png "屏幕截图")

注意事项：

- 公私钥需前后端配对一致
- 后端公钥对应前端私钥；后端私钥对应前端公钥

## 3. 前端开启加密

在请求头中加入 `isEncrypt: true`：

```js
headers: {
  isEncrypt: true
}
```

![输入图片说明](https://foruda.gitee.com/images/1701137141916998346/5e839bbe_4959041.png "屏幕截图")

## 4. 请求/响应加解密说明

详见：[关于请求响应参数解密](/questions/api_encrypt.md)

## 密钥生成说明

![输入图片说明](https://foruda.gitee.com/images/1675577852271308699/9b30258e_1766278.png "屏幕截图")
