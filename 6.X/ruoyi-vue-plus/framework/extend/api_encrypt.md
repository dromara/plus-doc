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

## 后端接口示例

### 登录/提交类接口

```java
@SaIgnore
@ApiEncrypt(response = true)
@PostMapping("/login")
public R<LoginVo> login(@RequestBody LoginBody loginBody) {
    LoginVo loginVo = loginService.login(loginBody);
    return R.ok(loginVo);
}
```

### 普通业务保存接口

```java
@ApiEncrypt(response = true)
@PutMapping("/profile/password")
public R<Void> updatePassword(@RequestBody UserPasswordBo bo) {
    userService.updatePassword(bo);
    return R.ok();
}
```

使用建议：

- 登录、注册、修改密码、重置密钥等包含敏感字段的接口建议启用。
- 列表查询、字典查询等普通 GET 接口不建议强行加密，避免增加排查成本。
- `response = true` 会加密响应体，适合响应中包含敏感数据的场景。

## 前端请求示例

```typescript
export function updatePassword(data: { oldPassword: string; newPassword: string }) {
  return request({
    url: '/system/user/profile/password',
    method: 'put',
    headers: {
      isEncrypt: 'true',
      repeatSubmit: false
    },
    data
  });
}
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

## 前后端配合步骤

1. 后端确认 `api-decrypt.enabled=true`。
2. 后端在需要加密的接口方法上增加 `@ApiEncrypt`。
3. 如果响应也需要加密，设置 `@ApiEncrypt(response = true)`。
4. 前端 `.env.*` 中确认 `VITE_APP_ENCRYPT=true`。
5. 前端请求对应接口时设置 `headers.isEncrypt`。
6. 使用浏览器 Network 检查请求头/响应头中是否存在 `encrypt-key`。

## 使用注意

## 常见问题

| 现象 | 排查方向 |
| --- | --- |
| 后端提示解密失败 | 检查前端 RSA 公钥是否与后端请求解密私钥配对 |
| 前端提示响应解密失败 | 检查后端响应加密公钥是否与前端 RSA 私钥配对 |
| GET 请求参数未加密 | 当前只对 POST、PUT 请求体加密，敏感信息不要放 URL |
| 本地正常生产失败 | 检查生产环境 `.env.production`、后端密钥、反向代理是否过滤 `encrypt-key` 头 |

- 前后端密钥必须配对，密钥不一致会表现为登录、注册或用户保存接口解密失败。
- 只有标注 `@ApiEncrypt` 的接口会强制走加解密逻辑。
- `GET` 参数不会按请求体方式加密，敏感数据不要放在 URL 查询参数里。
- API 加密只能降低明文传输暴露风险，不能替代 HTTPS、鉴权和后端权限校验。
