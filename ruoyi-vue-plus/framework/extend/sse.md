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

## 前端连接示例

```text
http://后端ip:端口/resource/sse?clientid=import.meta.env.VITE_APP_CLIENT_ID&Authorization=Bearer <token>
```

`Authorization` 为登录后获取的 token，连接成功后与其他接口的登录态一致。

## 消息发送

- `SseMessageUtils.sendMessage`：单机消息（特殊需求）
- `SseMessageUtils.subscribeMessage`：订阅分布式消息（默认已订阅）
- `SseMessageUtils.publishMessage`：发布分布式消息（推荐）
- `SseMessageUtils.publishAll`：群发消息
