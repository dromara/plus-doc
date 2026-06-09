# 统一消息推送
- - -

`ruoyi-common-push` 统一封装 SSE 与 WebSocket 两种推送方式。默认使用 SSE，前端会在登录后建立连接并拉取消息盒子。

## 模块位置

```text
ruoyi-common/ruoyi-common-push
ruoyi-modules/ruoyi-system
plus-ui/src/utils/push.ts
plus-ui/src/api/system/message
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

## 典型使用场景

| 场景 | 推荐做法 |
| --- | --- |
| 系统通知 | 后端保存通知/站内信后，调用 `PushHelper` 推送给指定用户 |
| 工作流待办 | 工作流服务在待办、抄送、审批完成后推送消息并跳转到对应页面 |
| 全局广播 | 使用 `publishAll` 推送系统维护、升级提醒等全员消息 |
| 业务提醒 | 自定义 `PushPayloadDTO`，在 `type`、`source`、`path` 中标识业务来源和跳转地址 |

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

## 后端发送示例

### 发送给单个用户

```java
import org.dromara.common.push.helper.PushHelper;
import org.dromara.common.push.model.PushPayloadDTO;

public void notifyUser(Long userId) {
    PushPayloadDTO payload = PushPayloadDTO.of(
        "todo",
        "workflow",
        "你有一条新的待办任务",
        Map.of("businessId", "10001"),
        "/workflow/task/todo"
    );
    PushHelper.publishMessage(List.of(userId), payload);
}
```

### 全员广播

```java
PushHelper.publishAll(
    PushPayloadDTO.of("notice", "system", "系统将在 22:00 进行维护", null, "/system/notice")
);
```

### Payload 字段建议

| 字段 | 建议用途 |
| --- | --- |
| `type` | 消息类型，如 `notice`、`todo`、`alarm` |
| `source` | 来源模块，如 `system`、`workflow`、`device` |
| `message` | 前端通知展示内容 |
| `data` | 业务扩展数据，如业务 ID、状态、跳转参数 |
| `path` | 前端点击后跳转路径 |

## 前端配置

配置位于：

```text
plus-ui/.env.development
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

## 调试方法

1. 登录系统后打开浏览器开发者工具 Network。
2. 过滤 `resource/message`，确认 SSE 或 WebSocket 连接已建立。
3. 后端调用 `PushHelper.sendMessage` 给当前登录用户发送一条测试消息。
4. 确认前端右上角消息盒子数量变化，并出现 Element Plus 通知。
5. 如果连接不断重试，检查 Token、代理路径、后端 `message.path` 与前端 `VITE_APP_MESSAGE_PATH` 是否一致。

## 使用建议

- 默认 `transport: sse`，前端 `.env.*` 中 `VITE_APP_MESSAGE_TRANSPORT` 需要与后端保持一致。
- 开发环境路径默认为 `/resource/message`，如修改后端 `message.path`，需同步修改前端 `VITE_APP_MESSAGE_PATH`。
- 生产环境使用 Nginx 代理 SSE 时，需要关闭代理缓冲：

```nginx
proxy_buffering off;
```

- 如果使用 WebSocket，需要配置 `Upgrade` 与 `Connection` 请求头。
