# 项目简介

---

## 平台简介

- 本仓库为前端技术栈 [Vue3](https://v3.cn.vuejs.org) + [TS](https://www.typescriptlang.org/) + [Element Plus](https://element-plus.org/zh-CN) + [Vite](https://cn.vitejs.dev) 版本。
- 成员项目: 基于 vben5(ant-design-vue) 的前端项目 [ruoyi-plus-vben5](https://github.com/imdap/ruoyi-plus-vben5)
- 成员项目: 基于 soybean 的前端项目 [ruoyi-plus-soybean](https://gitee.com/xlsea/ruoyi-plus-soybean)
- 配套后端代码仓库地址
- [RuoYi-Vue-Plus 6.X(注意版本号)](https://gitee.com/dromara/RuoYi-Vue-Plus)
- [RuoYi-Cloud-Plus 6.X(注意版本号)](https://gitee.com/dromara/RuoYi-Cloud-Plus)

## 分支说明

- 6.X分支(稳定发布主分支 生产可用)
- dev分支(开发分支 开发过程中使用)

## 前端运行

```bash
# 克隆项目
git clone https://gitee.com/JavaLionLi/plus-ui.git

# 安装依赖
pnpm install --registry=https://registry.npmmirror.com

# 启动服务
pnpm dev

# 构建生产环境
pnpm build:prod

# 前端访问地址默认 http://localhost:80
# 端口由 .env.* 中的 VITE_APP_PORT 控制
```

### 本地配置说明

常用环境变量位于 `.env.development`、`.env.production`：

| 配置 | 说明 |
| --- | --- |
| `VITE_APP_BASE_API` | 后端接口代理前缀，开发环境默认 `/dev-api` |
| `VITE_APP_CONTEXT_PATH` | 前端部署访问前缀，例如 `/admin/` |
| `VITE_APP_PORT` | 本地开发服务端口，默认 `80` |
| `VITE_APP_ENCRYPT` | 接口加密开关，需与后端保持一致 |
| `VITE_APP_CLIENT_ID` | 登录客户端 ID，需与后端客户端配置匹配 |
| `VITE_APP_MESSAGE_ENABLED` | 统一消息推送开关 |
| `VITE_APP_MESSAGE_TRANSPORT` | 消息推送方式：`sse` 或 `websocket` |
| `VITE_APP_MESSAGE_PATH` | 消息推送连接路径 |

开发环境接口代理在 `vite.config.ts` 中配置，默认将 `VITE_APP_BASE_API` 代理到后端服务。若后端端口或上下文路径调整，需要同步修改 `.env.*` 或代理配置。
