# MCP 集成
- - -

`ruoyi-common-mcp` 基于 Spring AI MCP Client 封装通用调用模板，用于连接外部 MCP Server 并调用工具或读取资源。

## 模块位置

```text
ruoyi-common/ruoyi-common-mcp
```

主要类：

```text
org.dromara.common.mcp.config.McpAutoConfiguration
org.dromara.common.mcp.core.McpClientTemplate
```

## 默认状态

`ruoyi-common-mcp` 是通用封装模块，本身不主动连接外部 MCP Server。只有在业务引入 Spring AI MCP Client 并配置出 `McpSyncClient` Bean 后，`McpAutoConfiguration` 才会注册 `McpClientTemplate` 供业务使用。

当前模块同时声明了 MCP Client 与 MCP Server WebMVC starter，文档重点说明项目内封装的 Client 调用模板；如果需要对外暴露 MCP Server，请按 Spring AI MCP Server 约定另行补充业务端点与安全控制。

## 依赖能力

模块引入：

```xml
<artifactId>spring-ai-starter-mcp-server-webmvc</artifactId>
<artifactId>spring-ai-starter-mcp-client</artifactId>
```

`McpAutoConfiguration` 会在存在 `McpSyncClient` Bean 时自动注册：

```java
McpClientTemplate
```

## McpClientTemplate 能力

| 方法 | 说明 |
| --- | --- |
| `listTools()` | 查询所有已连接 MCP Server 的工具列表 |
| `callTool(toolName, arguments)` | 调用所有 Server 上的同名工具 |
| `callTool(serverName, toolName, arguments)` | 调用指定 Server 的工具 |
| `readResource(uri)` | 读取所有 Server 上的同名资源 |
| `readResource(serverName, uri)` | 读取指定 Server 的资源 |
| `getClients()` | 获取当前 MCP Client 列表 |

## 使用方式

业务模块注入模板：

```java
@RequiredArgsConstructor
public class DemoService {

    private final McpClientTemplate mcpClientTemplate;

    public void call() {
        Map<String, Object> args = Map.of("keyword", "RuoYi");
        mcpClientTemplate.callTool("search", args);
    }
}
```

## 配置说明

MCP Client 的具体连接配置遵循 Spring AI MCP Client 约定。`ruoyi-common-mcp` 不负责创建连接细节，只在 Spring AI 已创建 `McpSyncClient` 后提供项目内统一封装。

适合场景：

- 调用文件系统、数据库、检索、浏览器等外部 MCP 工具。
- 在 AI 业务中统一管理可用工具。
- 将不同 MCP Server 的调用结果以统一结构返回给业务层。

## 常见问题

| 现象 | 排查方向 |
| --- | --- |
| `McpClientTemplate` 未注入 | 检查是否已创建 `McpSyncClient` Bean，或 MCP Client 自动配置是否生效 |
| 工具列表为空 | 检查外部 MCP Server 是否已启动、连接配置是否正确 |
| 调用工具失败 | 检查工具名称、参数结构和目标 Server 名称是否匹配 |
| 只需要 AI 聊天 | 优先使用 SnailAI 文档，MCP 适合扩展外部工具调用能力 |

如果业务只需要接入 SnailAI 聊天，优先阅读 [AI / SnailAI](/6.X/ruoyi-vue-plus/framework/extend/ai.md)。
