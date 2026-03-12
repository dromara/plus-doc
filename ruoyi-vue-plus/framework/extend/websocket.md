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

## 消息发送

- `WebSocketUtils.sendMessage`：单机消息（特殊需求）
- `WebSocketUtils.subscribeMessage`：订阅分布式消息（默认已订阅）
- `WebSocketUtils.publishMessage`：发布分布式消息（推荐）
- `WebSocketUtils.publishAll`：群发消息
