# 数据加解密
- - -

## API 加密注解 `@ApiEncrypt`
1. 对于标注了 `@ApiEncrypt` 注解的接口，请求参数都必须进行加密。
2. 注解的参数 `response` 为响应加密标识，默认 `false` 不加密，为 `true` 表示响应加密。
3. 加密解密逻辑由过滤器实现，详情可参考 `org.dromara.common.encrypt.filter.CryptoFilter`。

## API 加密配置
`application.yml`

![输入图片说明](https://foruda.gitee.com/images/1701131796468961065/83c464cd_4959041.png "屏幕截图")

`.env.development` / `.env.production`

![输入图片说明](https://foruda.gitee.com/images/1701131922417984949/7f91d943_4959041.png "屏幕截图")

> 注：
> 1. 公私钥与前端配置文件互为配对，如果需要更换请一同更换。
> 2. 后端公钥对应前端私钥；后端私钥对应前端公钥。

