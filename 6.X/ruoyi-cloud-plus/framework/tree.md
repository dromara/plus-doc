# 项目结构
- - -

## 后端结构

```text
RuoYi-Cloud-Plus/
  ruoyi-api
  ruoyi-auth
  ruoyi-common
  ruoyi-example
  ruoyi-gateway
  ruoyi-modules
  ruoyi-visual
  script
```

## ruoyi-api

跨服务 API 与 DTO 定义：

| 模块 | 说明 |
| --- | --- |
| `ruoyi-api-resource` | 资源服务远程接口 |
| `ruoyi-api-system` | 系统服务远程接口 |
| `ruoyi-api-workflow` | 工作流远程接口 |
| `ruoyi-api-bom` | API 依赖管理 |

## 核心服务

| 模块 | 说明 |
| --- | --- |
| `ruoyi-gateway` | 网关服务，默认对外入口 |
| `ruoyi-auth` | 认证中心，处理登录、验证码、授权登录 |
| `ruoyi-modules/ruoyi-system` | 用户、角色、菜单、字典、参数等系统功能 |
| `ruoyi-modules/ruoyi-resource` | OSS、邮件、短信、统一消息推送 |
| `ruoyi-modules/ruoyi-gen` | 代码生成 |
| `ruoyi-modules/ruoyi-job` | SnailJob 客户端与任务示例 |
| `ruoyi-modules/ruoyi-workflow` | WarmFlow 工作流 |

## ruoyi-common

公共能力包：

| 模块 | 说明 |
| --- | --- |
| `ruoyi-common-core` | 基础对象、常量、工具 |
| `ruoyi-common-web` | Web、异常、过滤器 |
| `ruoyi-common-security` | 安全与接口放行 |
| `ruoyi-common-satoken` | Sa-Token 登录与权限 |
| `ruoyi-common-dubbo` | Dubbo RPC 封装 |
| `ruoyi-common-mybatis` | MyBatis-Plus、数据权限 |
| `ruoyi-common-redis` | Redis、Redisson、限流、防重 |
| `ruoyi-common-push` | SSE/WebSocket 统一消息推送 |
| `ruoyi-common-mcp` | Spring AI MCP Client 封装 |
| `ruoyi-common-mqtt` | MQTT 客户端接入 |
| `ruoyi-common-oss` | S3 协议对象存储 |
| `ruoyi-common-sms` | sms4j 短信 |
| `ruoyi-common-mail` | 邮件发送 |
| `ruoyi-common-doc` | SpringDoc 文档增强 |
| `ruoyi-common-encrypt` | 数据加解密 |
| `ruoyi-common-translation` | 数据翻译 |
| `ruoyi-common-sensitive` | 数据脱敏 |
| `ruoyi-common-seata` | Seata 分布式事务 |
| `ruoyi-common-loadbalancer` | 团队路由与负载均衡扩展 |
| `ruoyi-common-bus` | Spring Cloud Bus |

## ruoyi-visual

独立可视化服务：

| 模块 | 说明 |
| --- | --- |
| `ruoyi-monitor` | Spring Boot Admin 监控中心 |
| `ruoyi-snailjob-server` | SnailJob 调度中心 |

## ruoyi-example

| 模块 | 说明 |
| --- | --- |
| `ruoyi-demo` | 框架功能演示服务 |
| `ruoyi-test-mq` | RabbitMQ、RocketMQ、Kafka 示例 |

## script

```text
script/sql                 数据库脚本
script/config/nacos        Nacos 配置文件
script/docker              Docker 编排与中间件配置
script/leave               工作流演示流程 JSON
```

主要 SQL：

```text
script/sql/ry-cloud.sql
script/sql/ry-job.sql
script/sql/ry-workflow.sql
```
