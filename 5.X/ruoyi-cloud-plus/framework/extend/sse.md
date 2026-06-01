# SSE 功能
- - -

## 版本

- >= 2.2.1

## 配置说明

配置位于 `ruoyi-resource`，远程调用可使用 `RemoteMessageService`。

![输入图片说明](https://foruda.gitee.com/images/1721986989993234455/4214cbbd_1766278.png "屏幕截图")

参数说明：

- `enabled`：是否启用
- `path`：应用路径

**注意：关闭 SSE 时需同步关闭前端开关，否则前端启动会报错。**

![输入图片说明](https://foruda.gitee.com/images/1728971445611402828/06519718_1766278.png "屏幕截图")

补充说明：

- Cloud 版本的服务端配置实际位于 Nacos 配置 `script/config/nacos/ruoyi-resource.yml`。
- 前端使用方式与 Vue 版本一致，仍然依赖 `.env.*` 中的 `VITE_APP_SSE`、`VITE_APP_CLIENT_ID` 和 `/resource/sse` 路径。
- 业务服务如果需要跨服务推送消息，优先通过 `RemoteMessageService` 调用 `ruoyi-resource`，避免各服务重复维护推送入口。
- 前端退出登录时同样会请求 `/resource/sse/close` 关闭连接，因此网关白名单也需要保留该地址。

## 前端连接示例

```text
http://后端ip:端口/resource/sse?clientid=import.meta.env.VITE_APP_CLIENT_ID&Authorization=Bearer <token>
```

`Authorization` 为登录后获取的 token，连接成功后与其他接口的登录态一致。

补充说明：

- 实际部署时通常连接网关地址下的 `/resource/sse`，而不是直接访问 `ruoyi-resource` 实例。
- 前端连接、通知展示、自动重连逻辑与 Vue 版本一致，可直接参考 [Vue 版本说明](/ruoyi-vue-plus/framework/extend/sse.md)。

## 消息发送

- `SseMessageUtils.sendMessage`：单机消息（特殊需求）
- `SseMessageUtils.subscribeMessage`：订阅分布式消息（默认已订阅）
- `SseMessageUtils.publishMessage`：发布分布式消息（推荐）
- `SseMessageUtils.publishAll`：群发消息

补充说明：

- Cloud 项目中推荐统一从业务服务调用远程消息服务，再由 `ruoyi-resource` 完成实际推送。
