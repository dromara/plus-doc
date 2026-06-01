# 统一消息推送
- - -

`ruoyi-common-push` 统一封装 SSE 与 WebSocket 两种推送方式。默认使用 SSE，前端会在登录后建立连接并拉取消息盒子。

## 模块位置

```text
ruoyi-common/ruoyi-common-push
ruoyi-modules/ruoyi-system
plus-ui-new/src/utils/push.ts
plus-ui-new/src/api/system/message
```

## 后端配置

配置位于：

```text
ruoyi-admin/src/main/resources/application.yml
```

```yaml
message:
  enabled: true
  transport: sse
  path: /resource/message
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

## 后端入口

SSE Controller：

```text
ruoyi-common/ruoyi-common-push/src/main/java/org/dromara/common/push/controller/SseController.java
```

连接地址：

```text
GET /resource/message
```

关闭连接：

```text
GET /resource/message/close
```

## 推送工具

业务代码使用：

```java
PushHelper.sendMessage(userId, "消息内容");
PushHelper.sendMessage("全局广播消息");
PushHelper.publishMessage(userIds, payload);
PushHelper.publishAll(payload);
```

自定义消息体：

```java
PushPayloadDTO.of(type, source, message, data, path)
```

## 前端配置

配置位于：

```text
plus-ui-new/.env.development
```

```env
VITE_APP_MESSAGE_ENABLED = true
VITE_APP_MESSAGE_TRANSPORT = 'sse'
VITE_APP_MESSAGE_PATH = '/resource/message'
```

前端入口：

```text
plus-ui/src/utils/push.ts
```

逻辑：

1. 登录后调用 `initPush()` 建立 SSE 或 WebSocket 连接。
2. 调用 `getMessageBox()` 初始化消息盒子。
3. 收到推送后写入 Pinia notice store，并弹出 Element Plus 通知。

## 工作流消息

工作流模块会通过统一消息推送发送待办、抄送、审批结果等提醒。相关逻辑位于：

```text
ruoyi-modules/ruoyi-workflow/.../FlwCommonServiceImpl.java
```

如果生产环境使用 Nginx 代理 SSE，需要关闭代理缓冲：

```nginx
proxy_buffering off;
```

如果使用 WebSocket，需要配置 `Upgrade` 与 `Connection` 请求头。
