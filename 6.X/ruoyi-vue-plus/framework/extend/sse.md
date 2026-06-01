# SSE 功能
- - -

## 版本

- >= 5.2.2

## 配置说明

![输入图片说明](https://foruda.gitee.com/images/1721986820599622433/1abe5d60_1766278.png "屏幕截图")

参数说明：

- `enabled`：是否启用
- `path`：应用路径

**注意：关闭 SSE 时需同步关闭前端开关，否则前端启动会报错。**

![输入图片说明](https://foruda.gitee.com/images/1728971445611402828/06519718_1766278.png "屏幕截图")

补充说明：

- 后端配置位于 `application.yml` 的 `sse` 节点。
- 前端开关位于 `.env.*` 中的 `VITE_APP_SSE`，默认前端会在 `src/layout/index.vue` 启动后初始化连接。
- 前端连接地址实际使用的是 `import.meta.env.VITE_APP_BASE_API + '/resource/sse'`。
- 当前项目会把 `Authorization` 和 `clientid` 以查询参数形式拼接到 SSE 地址中，`clientid` 要与登录时使用的 `VITE_APP_CLIENT_ID` 保持一致。
- 退出登录时前端会额外调用 `/resource/sse/close` 主动关闭连接。

## 前端连接示例

```text
http://后端ip:端口/resource/sse?clientid=import.meta.env.VITE_APP_CLIENT_ID&Authorization=Bearer <token>
```

`Authorization` 为登录后获取的 token，连接成功后与其他接口的登录态一致。

补充说明：

- 浏览器原生 `EventSource` 不方便自定义请求头，因此当前项目采用 URL 参数传 token。
- 如果是通过网关访问，通常应连接网关地址下的 `/resource/sse`，不要直接写死某个服务实例地址。

## 消息发送

- `SseMessageUtils.sendMessage`：单机消息（特殊需求）
- `SseMessageUtils.subscribeMessage`：订阅分布式消息（默认已订阅）
- `SseMessageUtils.publishMessage`：发布分布式消息（推荐）
- `SseMessageUtils.publishAll`：群发消息

补充说明：

- 一般业务场景优先使用 `publishMessage` 或 `publishAll`，由框架统一处理分布式投递。
- 需要给指定登录用户推送消息时，优先沿用框架现有的登录态和 `clientid` 体系，不建议自行再维护一套连接标识。
