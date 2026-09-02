# AI / SnailAI
- - -

主应用集成 SnailAI Agent、OpenAPI Client 和内嵌聊天页面；`ruoyi-snailai-server` 作为独立服务运行，负责 AI 控制台、模型、智能体、会话、RAG 等能力。


## 组件与代码位置

| 组件 | 路径 | 作用 |
| --- | --- | --- |
| SnailAI 公共模块 | `ruoyi-common/ruoyi-common-ai` | 按 `snail-ai.enabled` 条件启用 Agent 和 OpenAPI Client |
| RuoYi AI 模块 | `ruoyi-modules/ruoyi-ai` | 提供当前登录用户注册为 SnailAI OpenAPI 用户的接口 |
| SnailAI 独立服务 | `ruoyi-extend/ruoyi-snailai-server` | SnailAI Server 及管理控制台 |
| AI 聊天页 | `plus-ui-new/src/views/ai/chat/index.vue` | 注册用户后，以 iframe 加载 `/snail-chat/` |
| AI 用户 API | `plus-ui-new/src/api/ai/agent/index.ts` | 调用 `/snail-ai/user/register` |
| AI 控制台页 | `plus-ui-new/src/views/monitor/snailai/index.vue` | iframe 加载 `VITE_APP_SNAILAI_ADMIN` |


## 服务地址与端口

SnailAI Server 默认配置在 `ruoyi-snailai-server -> application.yml`：

| 用途 | 默认地址 |
| --- | --- |
| SnailAI Server HTTP 控制台/API | `http://localhost:8900/snail-ai` |
| SnailAI Server gRPC | `localhost:18888` |
| 主应用内嵌聊天入口 | 主应用 API 前缀下的 `/snail-chat/` |

前端环境变量中的控制台地址：

```dotenv
# .env.development
VITE_APP_SNAILAI_ADMIN = 'http://localhost:8900/snail-ai'

# .env.production
VITE_APP_SNAILAI_ADMIN = '/snail-ai'
```

生产环境使用相对路径时，需要在反向代理中将 `/snail-ai/` 转发到 SnailAI Server。项目自带 Nginx 配置已提供该代理示例，并关闭了代理缓冲以兼容长连接/SSE。

## 数据库脚本

先导入 RuoYi 基础库脚本（其中包含“AI会话”和“AI控制台”菜单），再导入 SnailAI 业务表：

```text
script/sql/ry_vue.sql
script/sql/ry_ai.sql
```

`ry_ai.sql` 会创建 `sai_*` 表并写入示例 AI 提供商及测试应用。生产环境应按实际情况修改或删除示例应用和令牌。

## 主应用配置

当前项目的核心配置如下（令牌仅示例，禁止直接用于生产）：

```yaml
snail-ai:
  enabled: false
  server:
    host: 127.0.0.1
    port: 18888
  app-id: 1
  token: ${SNAIL_AI_TOKEN:replace-me}
  # 客户端 gRPC 端口，默认使用 3${server.port}
  port: 3${server.port}
  skill-temp-dir: /tmp/snail-ai-agent/skills
  chat.ui.embed:
    enabled: true
    show-header: false
    show-sidebar-user: false
    show-agent-market: true
    compact-input: true
    lock-agent: false
  open-api:
    enabled: true
    web-port: 8900
    https: false
    prefix: snail-ai
    connect-timeout-ms: 5000
    read-timeout-ms: 60000
    chat-timeout-ms: 300000
```

说明：

- `snail-ai.enabled` 必须为 `true`，`ruoyi-common-ai` 才会启用 SnailAI Agent/OpenAPI Client。
- `server.host`、`server.port` 指向 SnailAI Server 的 gRPC 地址。
- `app-id`、`token` 必须与 SnailAI Server“应用管理”中的应用一致。
- `open-api.enabled` 控制 RuoYi 的 OpenAPI 适配接口是否注册。
- `open-api.web-port` 应与 SnailAI Server HTTP 端口一致；独立服务默认是 `8900`。
- `chat.ui.embed` 控制主应用内嵌聊天页的显示选项。

## 暴露的接口

当前 `ruoyi-ai` 模块只实现以下适配接口：

```text
POST /snail-ai/user/register
```

接口位于 `SnailAiController.java`，要求用户已登录。接口会以用户 ID 作为 `externalId`、昵称作为 `nickname`，向 SnailAI Server 注册或获取对应的 OpenAPI 用户，并返回 `openId` 等信息。

智能体、会话、消息和聊天等业务接口由 SnailAI Server 的内嵌页面和 OpenAPI 组件处理。

## 前端访问流程

“AI会话”菜单来自数据库菜单数据，路由为 `ai/chat/index`，页面加载流程如下：

1. 前端读取登录凭证。
2. 调用 `POST /snail-ai/user/register` 获取 SnailAI `openId`。
3. 组合 `${VITE_APP_BASE_API}/snail-chat/?openId=...&trustedCredential=...`。
4. 通过 iframe 加载 SnailAI 聊天页面。

“AI控制台”菜单路由为 `monitor/snailai/index`，地址由 `VITE_APP_SNAILAI_ADMIN` 提供，默认指向 `http://localhost:8900/snail-ai`。

## 启用步骤

1. 导入 `ry_vue.sql` 与 `ry_ai.sql`。
2. 启动 `ruoyi-extend/ruoyi-snailai-server`，确认 HTTP `8900` 和 gRPC `18888` 端口可用。
3. 打开 SnailAI 控制台，在“应用管理”中创建应用，记录 `app-id` 和 `token`；再配置模型、智能体等数据。
4. 修改 `ruoyi-admin` 的 `snail-ai` 配置，设置正确的 Server 地址、应用 ID 和令牌，并将 `enabled` 设为 `true`。
5. 启动 `ruoyi-admin`。
6. 设置前端 `VITE_APP_SNAILAI_ADMIN`，启动 `plus-ui-new`，为用户分配“AI会话”或“AI控制台”菜单权限后访问对应页面。

RAG 文档解析还依赖 Docling/PaddleOCR 时，按 SnailAI Server 配置中的 `snail-ai.rag.docling.*` 参数单独部署并配置对应服务；仅使用基础聊天时可不启用这些外部服务。

## 常见问题

| 现象 | 排查方向 |
| --- | --- |
| 菜单中没有 AI 会话或控制台 | 确认已导入 `ry_vue.sql`，并给角色分配 `AI会话` / `AI控制台` 菜单权限 |
| 页面提示无法注册 AI 用户 | 确认主应用已登录、`snail-ai.enabled=true`、`open-api.enabled=true`，并检查 `app-id`、`token` 与 Server 应用一致 |
| 聊天 iframe 空白或 404 | 检查主应用 `/snail-chat/**` 放行配置、`VITE_APP_BASE_API`，以及 SnailAI Server 是否正常运行 |
| AI 控制台打不开 | 检查 `VITE_APP_SNAILAI_ADMIN`、SnailAI Server 的 `8900` 端口及反向代理 `/snail-ai/` 配置 |
| 聊天流式输出中断 | 反向代理需关闭缓冲并放宽读取超时；项目 Nginx 示例已包含 SSE 相关配置 |
| RAG 文档解析失败 | 检查 Docling/PaddleOCR 是否单独启动，以及 `SNAIL_AI_RAG_*` 环境变量和 URL 是否可访问 |

生产环境必须替换示例令牌、加密密钥和数据库密码，并根据实际网络拓扑调整 HTTP/gRPC 地址、HTTPS 和反向代理配置。
