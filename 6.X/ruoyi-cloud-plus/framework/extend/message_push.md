# 统一消息推送
- - -

Cloud 使用 `ruoyi-common-push` 统一封装 SSE 与 WebSocket。连接承载在 `ruoyi-resource` 服务中，外部通过网关访问。

## 模块位置

```text
ruoyi-common/ruoyi-common-push
ruoyi-modules/ruoyi-resource
ruoyi-api/ruoyi-api-resource
```

主要类：

```text
org.dromara.common.push.helper.PushHelper
org.dromara.common.push.controller.SseController
org.dromara.common.push.config.MessageSseConfiguration
org.dromara.common.push.config.MessageWebSocketConfiguration
org.dromara.resource.dubbo.RemoteMessageServiceImpl
```

## 服务端配置

配置位于：

```text
script/config/nacos/ruoyi-resource.yml
```

```yaml
message:
  enabled: true
  transport: sse
  path: /message
  allowedOrigins: '*'
  sse-timeout: 86400000
  heartbeat-interval: 60
  web-socket-send-time-limit: 10000
  web-socket-buffer-size-limit: 64000
```

`transport` 可选：

```text
sse
websocket
```

网关路由位于：

```text
script/config/nacos/ruoyi-gateway.yml
```

外部访问 `/resource/**` 时会路由到 `ruoyi-resource`，并通过 `StripPrefix=1` 去掉 `/resource` 前缀。所以外部连接地址是：

```text
/resource/message
```

资源服务内部实际处理路径是：

```text
/message
```

## 前端配置

`plus-ui-new` 中的消息推送配置：

```env
VITE_APP_MESSAGE_ENABLED = true
VITE_APP_MESSAGE_TRANSPORT = 'sse'
VITE_APP_MESSAGE_PATH = '/resource/message'
```

前端入口：

```text
plus-ui-new/src/utils/push.ts
```

## 关闭连接白名单

网关白名单中已包含：

```text
/resource/message/close
```

对应配置文件：

```text
script/config/nacos/ruoyi-gateway.yml
```

## 业务发送

资源服务内部可使用 `PushHelper`：

```java
PushHelper.sendMessage(userId, "消息内容");
PushHelper.sendMessage("全局广播消息");
PushHelper.publishMessage(userIds, payload);
PushHelper.publishAll(payload);
```

其他服务需要跨服务推送时，通过 `ruoyi-api-resource` 中的远程消息接口调用资源服务，由 `ruoyi-resource` 统一维护客户端连接和推送逻辑。

## 代理注意

使用 SSE 时，Nginx 建议关闭代理缓冲：

```nginx
proxy_buffering off;
```

使用 WebSocket 时，需要配置升级头：

```nginx
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";
```
