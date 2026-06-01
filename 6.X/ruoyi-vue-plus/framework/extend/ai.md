# AI / SnailAI
- - -

项目包含 `ruoyi-ai` 业务模块，并在 `ruoyi-extend` 中提供 `ruoyi-snailai-server` 独立服务。主应用通过 SnailAI OpenAPI Client 与 SnailAI Server 通信，前端提供 AI 聊天页面。

## 模块位置

```text
ruoyi-common/ruoyi-common-ai
ruoyi-modules/ruoyi-ai
ruoyi-extend/ruoyi-snailai-server
plus-ui-new/src/views/ai
plus-ui-new/src/api/ai
```

## 数据库脚本

AI 模块脚本：

```text
script/sql/ry_ai.sql
```

使用 AI 功能前需要导入该脚本。

## 主应用配置

配置位于：

```text
ruoyi-admin/src/main/resources/application-dev.yml
```

核心配置：

```yaml
snail-ai:
  enabled: false
  chat-mode: stream
  server:
    host: 127.0.0.1
    port: 18888
  app-id: 1
  token: SAI_7c557fc05a304b0482a65ca67afdb0b8
  port: 18889
  open-api:
    enabled: true
    web-port: 8900
    https: false
    prefix: snail-ai
```

说明：

- `enabled` 控制主应用是否启用 SnailAI 客户端。
- `chat-mode` 支持 `stream` 与 `sync`。
- `server.host`、`server.port` 指向 SnailAI Server gRPC 地址。
- `app-id` 与 `token` 来自 SnailAI Server 应用管理。

## 后端接口

控制器：

```text
ruoyi-modules/ruoyi-ai/src/main/java/org/dromara/ai/controller/SnailAiController.java
```

接口前缀：

```text
/snail-ai
```

主要接口：

| 接口 | 说明 |
| --- | --- |
| `POST /snail-ai/user/register` | 注册当前用户到 SnailAI |
| `GET /snail-ai/agents` | 查询当前用户可用智能体 |
| `GET /snail-ai/agent/{agentId}` | 查询智能体详情 |
| `POST /snail-ai/agent/{agentId}/conversation` | 创建会话 |
| `GET /snail-ai/agent/{agentId}/conversations` | 查询会话列表 |
| `GET /snail-ai/agent/{agentId}/conversation/{conversationId}/messages` | 查询会话消息 |
| `POST /snail-ai/agent/{agentId}/chat/sync` | 同步聊天 |
| `POST /snail-ai/agent/{agentId}/chat/stream` | SSE 流式聊天 |

## 前端接入

前端 API：

```text
plus-ui/src/api/ai/agent/index.ts
```

页面：

```text
plus-ui/src/views/ai/chat
```

流式聊天使用原生 `fetch` 读取 `text/event-stream`，会处理 `thinking`、`text`、`done`、`error` 等事件。

## 启用步骤

1. 导入 `script/sql/ry_ai.sql`。
2. 启动 `ruoyi-extend/ruoyi-snailai-server`。
3. 在 SnailAI Server 创建应用，拿到 `app-id` 和 `token`。
4. 修改主应用 `snail-ai` 配置并设置 `enabled: true`。
5. 启动 `ruoyi-admin`。
6. 启动 `plus-ui`，进入 AI 聊天页面验证。

生产环境必须替换默认 token，并按实际网络修改 Server 地址。
