# 项目初始化
- - -

## 分支选择

| 分支       | 用途   | 说明             |
|----------|------|----------------|
| 6.X      | 稳定发布 | 推荐生产与学习        |
| dev      | 开发分支 | 代码随时更新，不建议直接使用 |
| future/* | 预览分支 | 新功能预览，稳定性不保证   |

## 运行环境清单
> 推荐使用 `Docker` 安装，项目内置编排文件。

**注意：禁止使用 `OracleJDK`（已知会导致 Spring 打包/运行异常）**

![输入图片说明](https://foruda.gitee.com/images/1720080025744223375/0213a652_1766278.png "屏幕截图")

| 组件            | 版本建议        | 说明                                                                       |
|---------------|-------------|--------------------------------------------------------------------------|
| JDK           | 21 / 25     | 推荐 OpenJDK [JDK下载地址](https://bell-sw.com/pages/downloads/)               |
| MySQL         | 8.0 / 8.4   | 其他版本未测试，可反馈                                                              |
| Oracle        | >= 12c      | 其他版本未测试，可反馈                                                              |
| PostgreSQL    | 15 ... 18   | 其他版本未测试，可反馈                                                              |
| SQL Server    | 2017 / 2019 | 其他版本未测试，可反馈                                                              |
| Redis         | >= 6.x      | 框架大量使用新特性 [win redis 下载地址](https://github.com/zkteco-home/redis-windows) |
| MinIO         | 按需          | 可用 RustFS 替代（新方案需谨慎）                                                     |
| Maven         | >= 3.8.x    | 构建工具                                                                     |
| Node.js       | >= 20.19.0  | 前端工程 `package.json` 已声明 engines 要求                                         |
| pnpm          | >= 10.0.0   | 前端推荐包管理工具，使用 `pnpm install` 安装依赖                                      |
| IntelliJ IDEA | 见下方         | 有版本避坑说明                                                                  |


## IntelliJ IDEA 版本建议

- 2023 全系列不推荐（问题较多）
- 2024.1 / 2024.2：Maven 插件无法刷新依赖
- 2025.1 / 2025.2：存在已知问题
- 推荐使用：2024.3（JDK21）或 2025.3（JDK21，JDK25 请按需自行验证）

## 初始化步骤

### 1. 勾选 Maven 对应环境
![输入图片说明](https://foruda.gitee.com/images/1678976284045210056/a2f28d33_1766278.png "屏幕截图")

### 2. 确认 JDK 版本与配置
后端工程基于 `JDK21` 编译运行，请确认 IDEA Project SDK、Maven Runner JRE 与项目语言级别均使用 JDK21。

![输入图片说明](https://foruda.gitee.com/images/1678941027820943505/c688e01e_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678941120518807034/4d56fcc9_1766278.png "屏幕截图")

### 3. 导入数据库 SQL
请按顺序依次导入，默认使用 `MySQL`。  
如需使用其他数据库，请参考 [多数据库数据源](/6.X/ruoyi-vue-plus/framework/extend/dynamic_datasource.md)。

基础功能导入主库脚本即可；如需启用定时任务、工作流、AI 等扩展能力，请按需继续导入对应脚本，例如 `ry_job.sql`、`ry_workflow.sql`、`ry_ai.sql`。

![输入图片说明](https://foruda.gitee.com/images/1726304546467780078/b78cabd4_1766278.png "屏幕截图")

### 4. 配置主服务
在已勾选的环境配置文件中填写数据库与 Redis 配置。

![输入图片说明](https://foruda.gitee.com/images/1678941357316005626/70559736_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678941405169571070/0d06a955_1766278.png "屏幕截图")

其他数据库配置可按系统自带模板进行调整。

![输入图片说明](https://foruda.gitee.com/images/1678941444707120259/b274592a_1766278.png "屏幕截图")

### 5. 启动顺序与建议

必启基础服务：`MySQL`、`Redis`、`DromaraApplication`<br>
可选基础服务：`MinIO`（文件上传）、`Monitor`（监控）、`SnailJob`（定时任务）、`SnailAI`（AI 能力）

![输入图片说明](https://foruda.gitee.com/images/1716175484919688429/8b9a79b7_1766278.png "屏幕截图")

- `MonitorAdminApplication`：Admin 监控服务  
- `SnailJobServerApplication`：任务调度中心服务  
- `SnailAiServerApplication`：AI 服务
- `DromaraApplication`：主应用服务

> 仅体验基础功能时，可先启动 `DromaraApplication`；监控、定时任务、AI 等服务按需启动。<br>
> 工作流相关初始化请参考 [工作流初始化](/6.X/ruoyi-vue-plus/quickstart/worker_init.md)。

## 示例：最小化启动

仅体验基础功能时，可先启动 `MySQL`、`Redis` 与 `DromaraApplication`，其余服务按需再补充。

启动成功后建议检查：

1. 控制台无数据库、Redis、端口占用异常。
2. 浏览器访问接口文档或后端健康接口，确认主应用可访问。
3. 启动前端 `plus-ui` 后，能正常打开登录页并获取验证码。
4. 使用默认账号登录后，菜单、字典、参数、用户等基础功能能正常加载。

## 常见问题

| 现象 | 排查方向 |
| --- | --- |
| Maven 依赖刷新失败 | 确认 IDEA 版本、Maven Runner JRE 是否为 JDK21，必要时清理本地仓库对应依赖后重新刷新 |
| 启动提示端口占用 | 检查 `server.port`、Monitor、SnailJob、SnailAI 等服务端口是否冲突 |
| 登录验证码或接口请求失败 | 检查 Redis 是否启动、前端 `VITE_APP_BASE_API` 与后端端口/代理是否一致 |
| 数据表不存在 | 确认主库脚本和按需模块脚本已导入到正确数据库 |
| 文件上传失败 | 检查 OSS/MinIO 配置与服务是否启用 |
