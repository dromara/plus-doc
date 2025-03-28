# API加解密
- - -

## 重点声明

**很多人问我 为啥要在前端放私钥 在这里解答一下**

首先 api加密功能主要是为了防止传输过程中拦截的 例如伪基站拦截 代理拦截等<br>
其次 无论是放公钥 还是放私钥 最终前端都是要解密做展示的 也就是说 无论你放什么钥最终都是可以拿来做解密的这个没有区别<br>
最主要的原因 是因为js并没有提供 也没有三方工具支持公钥解密 所以只能用私钥做解密(谁有或者知道有什么工具能做 可以告诉作者)<br>
如果看了上述观点还是觉得作者搞的有问题 那你可以选择不用这个功能了 作者表示也没有办法 如果你有更好的解决方案 希望可以提供给作者共同进步<br>

## 1：API 加密注解 `@ApiEncrypt`
1. 对于标注了 `@ApiEncrypt` 注解的接口，请求参数都必须进行加密。
2. 注解的参数 `response` 为响应加密标识，默认 `false` 不加密，为 `true` 表示响应加密。
3. 加密解密逻辑由过滤器实现，详情可参考 `org.dromara.common.encrypt.filter.CryptoFilter`。

## 2：API 加密配置
`application.yml`

![输入图片说明](https://foruda.gitee.com/images/1701131796468961065/83c464cd_4959041.png "屏幕截图")

`.env.development` / `.env.production`

![输入图片说明](https://foruda.gitee.com/images/1709533252413969800/1d0dff25_1766278.png "屏幕截图")

> 注：
> 1. 公私钥与前端配置文件互为配对，如果需要更换请一同更换。
> 2. 后端公钥对应前端私钥；后端私钥对应前端公钥。

## 3：前端开启加密
如果需要开启 API 加密，则需要修改 `request` 的 `headers` 内容：
```Javascript
headers: {
  isEncrypt: true
}
```

![输入图片说明](https://foruda.gitee.com/images/1701137141916998346/5e839bbe_4959041.png "屏幕截图")

## 4.关于请求响应参数加解密说明

如何加解密请求响应参数看这里 -> [关于请求响应参数解密](/questions/api_encrypt.md)

## 密钥生成说明

![输入图片说明](https://foruda.gitee.com/images/1675577852271308699/9b30258e_1766278.png "屏幕截图")