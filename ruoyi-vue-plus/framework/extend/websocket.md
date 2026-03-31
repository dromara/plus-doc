# WebSocket 功能
- - -

## 版本

- >= 5.1.0

## 配置说明

默认关闭（推送建议优先使用 SSE）。

![输入图片说明](https://foruda.gitee.com/images/1688356273985385949/5e4d1de8_1766278.png "屏幕截图")

参数说明：

- `enabled`：是否启用
- `path`：应用路径
- `allowedOrigins`：访问源地址

**注意：关闭 WebSocket 时需同步关闭前端开关，否则前端启动会报错。**

![输入图片说明](https://foruda.gitee.com/images/1700644877512019497/052d2f46_1766278.png "屏幕截图")

补充说明：

- 后端配置位于 `application.yml` 的 `websocket` 节点。
- 前端开关位于 `.env.*` 中的 `VITE_APP_WEBSOCKET`，默认前端会在 `src/layout/index.vue` 中初始化连接。
- 当前项目默认同时保留 SSE 与 WebSocket 能力，但推送场景优先推荐使用 SSE，只有确实需要双向通信或长连接自定义协议时再开启 WebSocket。
- 当前前端封装里已经带了自动重连和心跳包逻辑。

## 前端连接示例

```text
ws://后端ip:端口/resource/websocket?clientid=import.meta.env.VITE_APP_CLIENT_ID&Authorization=Bearer <token>
```

由于 JS 不支持自定义请求头，这里使用参数传输。若前端支持 Header，请优先使用 Header。

Header 示例：

```js
headers: {
    Authorization: "Bearer " + getToken(),
    clientid: import.meta.env.VITE_APP_CLIENT_ID
}
```

连接成功后，登录态获取方式与框架内其他接口一致。

补充说明：

- 浏览器原生 WebSocket 不方便统一附带自定义 Header，所以当前项目默认使用 URL 参数方式携带 `Authorization` 与 `clientid`。
- 如果部署在 HTTPS 下，需要使用 `wss://` 协议。
- `allowedOrigins` 要和实际访问域名保持一致，生产环境不建议长期使用全放开的 `*`。

## 消息发送

- `WebSocketUtils.sendMessage`：单机消息（特殊需求）
- `WebSocketUtils.subscribeMessage`：订阅分布式消息（默认已订阅）
- `WebSocketUtils.publishMessage`：发布分布式消息（推荐）
- `WebSocketUtils.publishAll`：群发消息

补充说明：

- 和 SSE 一样，集群环境优先使用 `publishMessage` / `publishAll`，不要只依赖单机 `sendMessage`。
