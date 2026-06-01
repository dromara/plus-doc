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

## 使用方式

业务服务在完成 Spring AI MCP Client 配置后，可注入 `McpClientTemplate`：

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

## 能力说明

| 方法 | 说明 |
| --- | --- |
| `listTools()` | 查询所有已连接 MCP Server 的工具列表 |
| `callTool(toolName, arguments)` | 调用所有 Server 上的同名工具 |
| `callTool(serverName, toolName, arguments)` | 调用指定 Server 的工具 |
| `readResource(uri)` | 读取所有 Server 上的同名资源 |
| `readResource(serverName, uri)` | 读取指定 Server 的资源 |
| `getClients()` | 获取当前 MCP Client 列表 |

`ruoyi-common-mcp` 只提供项目内统一封装，具体 MCP Server 连接配置遵循 Spring AI MCP Client 约定。
