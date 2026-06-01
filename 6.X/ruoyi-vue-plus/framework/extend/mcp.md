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

如果业务只需要接入 SnailAI 聊天，优先阅读 [AI / SnailAI](/6.X/ruoyi-vue-plus/framework/extend/ai.md)。
