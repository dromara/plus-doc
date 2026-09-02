# AI / SnailAI
- - -

与单体版不同，AI 能力拆分为独立的 `ruoyi-ai` 微服务；`ruoyi-snailai-server` 负责 SnailAI 控制台、模型、智能体、会话和 RAG 等能力。

## 组件与代码位置

| 组件 | 路径 | 作用 |
| --- | --- | --- |
| SnailAI 公共模块 | `ruoyi-common/ruoyi-common-ai` | 按 `snail-ai.enabled` 条件启用 Agent 和 OpenAPI Client |
| AI 微服务 | `ruoyi-modules/ruoyi-ai` | 注册为 Nacos 服务并提供当前用户 OpenAPI 注册接口 |
| SnailAI 独立服务 | `ruoyi-visual/ruoyi-snailai-server` | SnailAI Server 及管理控制台 |
| 网关配置 | `script/config/nacos/ruoyi-gateway.yml` | 转发 `/snail-ai/**` 和放行 `/snail-chat/**` |
| 前端 AI 聊天页 | `plus-ui-new/src/views/ai/chat/index.vue` | 注册用户后，以 iframe 加载 `/snail-chat/` |
| 前端 AI 用户 API | `plus-ui-new/src/api/ai/agent/index.ts` | 调用 `/snail-ai/user/register` |
| 前端 AI 控制台页 | `plus-ui-new/src/views/monitor/snailai/index.vue` | iframe 加载 `VITE_APP_SNAILAI_ADMIN` |

Cloud 版的 `ruoyi-ai` 是独立可启动服务，不由其他业务服务内嵌启动。当前 `ry-cloud.sql` 默认只初始化“AI控制台”外链菜单。

## 服务地址与端口

| 用途 | 默认地址 |
| --- | --- |
| AI 微服务 HTTP | `http://localhost:9206` |
| AI 微服务 SnailAI 客户端 gRPC | `localhost:29206` |
| SnailAI Server HTTP 控制台/API | `http://localhost:8900/snail-ai` |
| SnailAI Server gRPC | `localhost:18888` |
| 网关对外 AI API | 网关地址下的 `/snail-ai/**` |
| 网关对外聊天入口 | 网关地址下的 `/snail-chat/` |

`ruoyi-ai` 默认端口和容器参数位于 `ruoyi-ai -> application.yml` 及其 Dockerfile；SnailAI Server 默认配置位于 `ruoyi-snailai-server -> application.yml`。

## 数据库与 Nacos 配置

Cloud 版使用独立 AI 数据库。`script/config/nacos/datasource.yml` 中的默认数据源为 `ry-ai`：

```yaml
datasource:
  ai:
    url: jdbc:mysql://localhost:3306/ry-ai
    username: root
    password: password
```

导入脚本：

```text
script/sql/ry-ai.sql
```

脚本会创建 `sai_*` 表并写入示例 AI 提供商及测试应用。生产环境应修改或删除示例应用、令牌和默认密钥。

AI 微服务配置文件为 `script/config/nacos/ruoyi-ai.yml`，通过 `ruoyi-ai` 的 Nacos 配置导入机制加载；SnailAI Server 配置文件为 `script/config/nacos/ruoyi-snailai-server.yml`。

## AI 微服务配置

`script/config/nacos/ruoyi-ai.yml` 的核心配置如下（令牌仅示例）：

```yaml
snail-ai:
  enabled: true
  server-host: 127.0.0.1
  server-port: 18888
  app-id: 1
  token: ${SNAIL_AI_TOKEN:replace-me}
  # 客户端 gRPC 端口，默认使用 2${server.port}
  port: 2${server.port}
  host:
  max-concurrent-chats: 10
  skill-temp-dir: /tmp/snail-ai-agent/skills
  chat.ui.embed:
    enabled: true
    show-header: false
    show-sidebar-user: false
    show-agent-market: true
    compact-input: true
    lock-agent: false
  server-callback:
    timeout: 5000
    retry-times: 3
    retry-interval: 1000
  openapi:
    enabled: true
    server-host:
    web-port: 8900
    https: false
    prefix: snail-ai
    connect-timeout-ms: 5000
    read-timeout-ms: 60000
    chat-timeout-ms: 300000
```

说明：

- Cloud 配置键为 `server-host`、`server-port`，不是单体版的 `server.host`、`server.port`。
- Cloud 配置键为 `openapi`，不是单体版的 `open-api`。
- `server-host/server-port` 指向 SnailAI Server gRPC；`openapi.server-host` 留空时默认使用 `server-host`。
- `port` 使用 `2${server.port}` 时，`ruoyi-ai` 默认服务端口 9206 对应客户端端口为 29206。
- `app-id`、`token` 必须与 SnailAI Server“应用管理”中的应用一致。

## 接口

AI 微服务控制器位于 `SnailAiController.java`，当前提供：

```text
POST /user/register
```

经网关访问时，完整路径为：

```text
POST /snail-ai/user/register
```

接口要求用户已登录，会以 Cloud 用户 ID 作为 `externalId`、昵称作为 `nickname`，向 SnailAI Server 注册或获取 OpenAPI 用户，并返回 `openId` 等信息。智能体、会话、消息和聊天接口由 SnailAI Server 的内嵌页面和 OpenAPI 组件处理。

## 网关与前端访问流程

网关在 `ruoyi-gateway.yml` 中将 `/snail-ai/**` 转发到 `lb://ruoyi-ai`，并放行 `/snail-chat/**`。前端仍按以下流程访问：

1. 读取登录凭证。
2. 调用网关地址的 `POST /snail-ai/user/register` 获取 SnailAI `openId`。
3. 组合 `${VITE_APP_BASE_API}/snail-chat/?openId=...&trustedCredential=...`。
4. 通过 iframe 加载 SnailAI 聊天页面。

“AI控制台”地址由 `plus-ui` 的 `VITE_APP_SNAILAI_ADMIN` 提供：

```dotenv
# .env.development
VITE_APP_SNAILAI_ADMIN = 'http://localhost:8900/snail-ai'

# .env.production
VITE_APP_SNAILAI_ADMIN = '/snail-ai'
```

生产环境使用相对路径时，需要将 `/snail-ai/` 反向代理到 SnailAI Server；项目 Nginx 示例已关闭代理缓冲并放宽读取超时，以兼容长连接/SSE。

## 启用步骤

1. 创建 `ry-ai` 数据库，导入 `script/sql/ry-ai.sql`（PostgreSQL 使用对应脚本）。
2. 在 Nacos 发布或确认 `datasource.yml`、`ruoyi-ai.yml`、`ruoyi-snailai-server.yml` 配置。
3. 启动 `ruoyi-visual/ruoyi-snailai-server`，确认 HTTP `8900` 和 gRPC `18888` 可用。
4. 在 SnailAI 控制台创建应用，记录 `app-id` 和 `token`，并配置模型、智能体等数据。
5. 启动 `ruoyi-modules/ruoyi-ai`，确认服务注册到 Nacos，HTTP `9206`、客户端 gRPC `29206` 正常。
6. 启动认证、系统、网关等基础服务，确认网关已加载 `ruoyi-ai` 路由。
7. 配置并启动 `plus-ui`，为用户分配“AI控制台”菜单权限；如已新增 `ai/chat/index` 菜单，再分配“AI会话”权限后访问聊天页面。

RAG 文档解析依赖 Docling/PaddleOCR 时，按 `ruoyi-snailai-server.yml` 中的 `snail-ai.rag.docling.*` 参数单独部署并配置；仅使用基础聊天时可不启用这些外部服务。

## 常见问题

| 现象 | 排查方向 |
| --- | --- |
| `/snail-ai/user/register` 返回 404 | 确认网关已加载 `ruoyi-ai` 路由，且 AI 服务已注册到 Nacos |
| 页面提示无法注册 AI 用户 | 检查登录状态、`snail-ai.enabled`、`openapi.enabled`、`app-id`、`token` 及 AI 服务到 SnailAI Server 的网络连通性 |
| 聊天 iframe 空白或 404 | 检查网关 `/snail-chat/**` 放行配置、`VITE_APP_BASE_API` 和 SnailAI Server 状态 |
| AI 控制台打不开 | 检查 `VITE_APP_SNAILAI_ADMIN`、SnailAI Server `8900` 端口及 `/snail-ai/` 反向代理 |
| AI 微服务启动失败 | 检查 Nacos 配置导入、`datasource.ai` 数据源及 `ry-ai` 数据库连接 |
| 聊天流式输出中断 | 网关或反向代理需关闭缓冲并放宽响应超时；SSE 长连接需调整连接池和超时参数 |
| RAG 文档解析失败 | 检查 Docling/PaddleOCR 服务是否启动，以及 `SNAIL_AI_RAG_*` 环境变量和 URL 是否可访问 |

生产环境必须替换示例令牌、加密密钥和数据库密码，并根据实际网络拓扑调整 Nacos、网关、HTTP/gRPC 地址、HTTPS 和反向代理配置。
