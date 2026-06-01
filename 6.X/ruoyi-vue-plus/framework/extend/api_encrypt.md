# API 加解密
- - -

## 核心说明

API 加密主要用于防止传输过程被拦截（如代理劫持）。  
前端必须解密后展示，因此无论公钥/私钥最终都可被用于解密。  
由于 JS 环境缺少“公钥解密”的通用实现，因此前端使用私钥进行解密。

如有更优方案，欢迎反馈与共建。

## 模块位置

API 加解密由公共加密模块提供：

```text
ruoyi-common/ruoyi-common-encrypt
```

核心类：

```text
annotation/ApiEncrypt.java
filter/CryptoFilter.java
filter/DecryptRequestBodyWrapper.java
filter/EncryptResponseBodyWrapper.java
properties/ApiDecryptProperties.java
```

单体项目后端配置位于：

```text
ruoyi-admin/src/main/resources/application.yml
```

前端实现位于：

```text
plus-ui/src/utils/request.ts
plus-ui/src/utils/crypto.ts
plus-ui/src/utils/jsencrypt.ts
```

## 开启方式

后端在接口方法上标注：

```java
@ApiEncrypt(response = true)
@PostMapping("/login")
public R<LoginVo> login(@RequestBody LoginBody loginBody) {
    return R.ok(loginService.login(loginBody));
}
```

`@ApiEncrypt` 只支持标注在方法上：

```java
boolean response() default false;
```

- 标注注解后，请求体需要按前端规则加密。
- `response = true` 时响应体也会加密。
- 未开启 `response` 时只处理请求解密。

前端请求需要设置请求头：

```ts
headers: {
  isEncrypt: true
}
```

同时环境变量需要开启：

```text
VITE_APP_ENCRYPT=true
```

当前前端只对 `POST`、`PUT` 请求体执行加密。

## 加密流程

请求加密：

1. 前端生成随机 AES key。
2. 使用 AES 加密请求体。
3. 使用 RSA 公钥加密 AES key。
4. 将加密后的 AES key 放入 `encrypt-key` 请求头。
5. 后端 `CryptoFilter` 读取请求头，用 RSA 私钥解出 AES key，再解密请求体。

响应加密：

1. 后端生成随机 AES key。
2. 使用 AES 加密响应体。
3. 使用 RSA 公钥加密 AES key。
4. 将加密后的 AES key 放入 `encrypt-key` 响应头。
5. 前端解出 AES key 后解密响应体。

## 配置项

后端主要配置：

```yaml
api-decrypt:
  enabled: true
  headerFlag: encrypt-key
  publicKey: 前端解密响应密钥对应的公钥
  privateKey: 后端解密请求密钥对应的私钥
```

字段含义：

| 配置 | 说明 |
| --- | --- |
| `enabled` | 是否启用 API 加解密过滤器 |
| `headerFlag` | 传递加密 AES key 的请求/响应头 |
| `publicKey` | 后端响应加密时使用 |
| `privateKey` | 后端请求解密时使用 |

## 使用注意

- 前后端密钥必须配对，密钥不一致会表现为登录、注册或用户保存接口解密失败。
- 只有标注 `@ApiEncrypt` 的接口会强制走加解密逻辑。
- `GET` 参数不会按请求体方式加密，敏感数据不要放在 URL 查询参数里。
- API 加密只能降低明文传输暴露风险，不能替代 HTTPS、鉴权和后端权限校验。
