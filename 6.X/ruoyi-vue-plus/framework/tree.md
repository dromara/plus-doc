# 项目结构
- - -

## 后端结构

```text
RuoYi-Vue-Plus/
  ruoyi-admin
  ruoyi-api
  ruoyi-common
  ruoyi-extend
  ruoyi-modules
  script
```

## ruoyi-admin

主应用模块，包含：

- `DromaraApplication` 启动入口
- 登录、验证码、首页等 Web Controller
- `application.yml` 与多环境配置
- 全局 Web 初始化与监听器

## ruoyi-api

跨模块 API 与 DTO 定义。系统、OSS、工作流等模块会通过这里暴露内部服务接口，避免业务模块之间直接耦合实现类。

## ruoyi-common

公共能力包：

| 模块 | 说明 |
| --- | --- |
| `ruoyi-common-core` | 基础对象、常量、工具 |
| `ruoyi-common-web` | Web、异常、过滤器 |
| `ruoyi-common-satoken` | Sa-Token 登录与权限 |
| `ruoyi-common-security` | 安全与接口放行 |
| `ruoyi-common-mybatis` | MyBatis-Plus、数据权限 |
| `ruoyi-common-redis` | Redis 与 Redisson |
| `ruoyi-common-push` | SSE/WebSocket 统一消息推送 |
| `ruoyi-common-ai` | SnailAI 客户端公共配置 |
| `ruoyi-common-mcp` | Spring AI MCP Client 封装 |
| `ruoyi-common-mqtt` | MQTT 客户端接入 |
| `ruoyi-common-doc` | SpringDoc 文档增强 |
| `ruoyi-common-oss` | S3 协议对象存储 |
| `ruoyi-common-excel` | Fesod Excel 导入导出 |
| `ruoyi-common-translation` | 数据翻译 |

## ruoyi-modules

业务模块：

| 模块 | 说明 |
| --- | --- |
| `ruoyi-system` | 用户、角色、菜单、部门、消息、OSS 等系统功能 |
| `ruoyi-gen` | 代码生成 |
| `ruoyi-job` | SnailJob 任务示例与执行器 |
| `ruoyi-workflow` | WarmFlow 工作流 |
| `ruoyi-ai` | SnailAI OpenAPI 对接与聊天接口 |
| `ruoyi-demo` | 示例功能 |

## ruoyi-extend

独立扩展服务：

| 模块 | 说明 |
| --- | --- |
| `ruoyi-monitor-admin` | Spring Boot Admin 监控中心 |
| `ruoyi-snailjob-server` | SnailJob 调度中心 |
| `ruoyi-snailai-server` | SnailAI 服务端 |

## script

```text
script/sql                 数据库脚本
script/docker              Docker 编排与 Nginx/Redis 配置
script/bin                 启停脚本
script/leave               工作流演示流程 JSON
```

MySQL 主脚本：

```text
script/sql/ry_vue.sql
script/sql/ry_job.sql
script/sql/ry_workflow.sql
script/sql/ry_ai.sql
```

Oracle、PostgreSQL、SQLServer 脚本在对应子目录中。
