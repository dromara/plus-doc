# 更新日志
- - -

## 6.0.0-BETA - 2026-06-22

### 🔴 重大更新
1. 不兼容整体升级 SpringBoot 4.X 全系列生态
2. 增加 MyBatis-Plus 扩展工具，大幅简化整体业务代码写法
3. 集成 MyBatis-Plus-Join 重构项目代码
4. 重写翻译和脱敏实现，使用 Jackson tree 解析 + ResponseBodyAdvice 批量翻译，效率大幅提升
5. 数据权限增加角色与菜单关联，实现 角色->菜单->数据权限 精细化控制
6. 提炼所有通用 Service 接口与实体类为 ruoyi-api 模块，通用性与扩展性增强
7. 全局将 Date 替换为 LocalDateTime 时间类型
8. 合并 common-sse / common-websocket 为 ruoyi-common-push 推送模块
9. 整体移除多租户相关功能
10. 集成 snail-ai，并新增 ruoyi-snailai-server 独立服务

### 📦 依赖更新
1. SpringBoot 4.1 全版本升级
2. SpringBoot-Admin 4.1
3. Springdoc 3.0.2
4. Redisson 4.6.1
5. dynamic-ds 4.5.0
6. AWS-SDK 2.42.9
7. bcpkix-jdk18on 1.84
8. Spring AI 2.0.0
9. snail-ai 0.0.6
10. snailjob 2.0.0
11. warm-flow 1.8.8
12. MySQL 8.0.42 → 8.4.9
13. Nginx 1.23.4 → 1.31.1
14. Redis 7.2.8 → 8.6.3
15. Minio 升级至 RELEASE.2026-04-17T00-00-00Z
16. JDK 版本更新至 21.0.11（Dockerfile 同步适配）
17. FastExcel 迁移至 Apache Fesod

### 🆕 功能新增
1. 新增 ruoyi-snailai-server 独立服务，提供 snail-ai 企业级 AI Agent 平台整合
2. 新增 ruoyi-common-mcp 模块，支持 MCP 服务端/客户端
3. 新增 ruoyi-common-mqtt 消息推送模块
4. 新增 ruoyi-common-elasticsearch 模块，支持 ES 开发
5. 新增 AI 编程支持（codex、claude）
6. 新增 SQL join 工具，简化业务代码
7. 新增链式查询函数、聚合函数、子查询支持
8. 新增 R.data 方法，解决 R<String> 等泛型返回问题
9. 新增 maven-wrapper，保证项目构建环境一致
10. 新增 Spring AI、snail-ai 相关 Docker / Run 配置
11. 新增 公共基础模块开发规范与 AI Agent 辅助文档
12. 新增 自定义sql日志输出 性能比p6spy更好更详细 可以精确定位mapper具体位置

### ☁️ Cloud 版本单独更新
1. 不兼容整体升级 Spring Cloud 2025.1.2、Spring Cloud Alibaba 2025.1，适配 SpringBoot 4.X 微服务生态
2. 升级 Nacos 至 3.2.2、Seata 至 2.6.0，并调整 Nacos / Seata 部署方式，因底层结构变化不再内置维护源码服务，改为使用者自行下载搭建
3. 删除 Gateway WebFlux 版本，统一使用 MVC Gateway，降低网关维护复杂度并统一异常处理行为
4. 集成 snail-ai-server，并新增 `ruoyi-ai` 服务，补充对应 Run / Docker 配置
5. 增加 Spring Cloud Bus Redis 实现，workflow 模块默认可使用 Redis 作为事件中心，降低对 MQ 的强依赖
6. 优化 Dubbo 相关适配，修复 JDK 25 SPI 加载兼容问题、Dubbo 元数据处理异常，以及远程调用中手动使用虚拟线程导致上下文丢失的问题
7. 优化微服务远程接口与 API 模块，调整 RemoteMessageService、RemotePushPayLoad、RemoteLoginInfo 等远程调用对象与包结构
8. 升级并适配微服务周边组件：Elasticsearch / Kibana / Logstash 8.19.16、RocketMQ 5.5.0、RocketMQ Spring Boot Starter 2.3.5、Kafka 4.3.0
9. 升级监控链路：SkyWalking OAP / UI 10.4.0、Java Agent 9.6.0、Prometheus 3.12.0、Grafana 13.0.2
10. 更新 Grafana 看板，替换旧 Spring Boot 2.1 看板为 Spring Boot 3.x Statistics，并补充 Nacos 与 JVM Micrometer 看板模板说明
11. 调整 Elasticsearch 默认关闭认证，并保留启用认证初始化说明；适配 Logstash 输出到 Elasticsearch 8.x 的 hosts 配置
12. 优化 Gateway 默认请求头覆盖逻辑，修复 MVC 网关与 Flux 网关异常返回内容不一致问题
13. 修复 Cloud 配置文件路径错误、Spring 包名调整导致的启动异常等微服务版本适配问题

### ✨ 功能优化
### 代码规范与可读性
1. 简化类型检查、优化代码格式、简化条件判断
2. 使用 getFirst() 替代 get(0)，提升代码可读性
3. 规范 Mapper / DTO 命名，统一 bo 对象结构
4. 统一用户性别字段 gender、统一系统用词
5. 全模块补充注释，增强代码可维护性
6. 使用常量替代硬编码状态值
7. 全局格式化代码、清理冗余分隔符、消除编译警告
8. 新增上传附件保存扩展信息
9. 未知异常和系统异常增加随机编号方便查找
10. 重构将代码生成vm模板替换为fm模板 语法更清晰明了

### 核心功能优化
1. **代码生成器**：支持多前端模板、自动数据库类型映射、自定义路径导出、清理无用代码
2. **公共模块**：重构 common-core / common-web / common-json / common-mybatis / common-redis / common-oss / common-excel / common-encrypt 等基础能力
3. **数据访问**：引入 MyBatis-Plus 扩展工具与 MPJ，优化分页、数据权限、联表查询和 Mapper 处理逻辑
4. **翻译脱敏**：重写翻译与脱敏链路，支持批量翻译、缓存解析结果，减少重复序列化
5. **登录认证**：优化登录异常提示、客户端 ID 与 Token 不匹配提示，统一 SSE/WS 认证处理
6. **工作流**：优化审批逻辑、批量翻译、撤销权限控制、防 XSS 过滤和流程图提示查询性能
7. **Excel**：重构导入导出构建器，大数据量导出支持多线程 ZIP 打包，优化导入转换逻辑
8. **OSS**：重构客户端生命周期，新增 S3 客户端，优化配置管理、路径风格和下载处理
9. **消息推送**：扩展消息类型/来源/跳转路径，完成消息盒子前后端联动
10. **接口响应**：统一 R 类型返回，优化路由数据与 ext 扩展数据，清理无用接口
11. **性能**：优化菜单树构建、虚拟线程查询、任务处理器转换和批量远程调用逻辑

### 其他优化
1. 优化日期解析、LocalDateTime 序列化和代码生成器时间类型
2. 优化 Redis 工具类、缓存管理、加解密逻辑，并将 idempotent / ratelimiter 能力合并进 redis 模块
3. 头像上传改为先上传 OSS 后更新用户数据
4. 优化 Dockerfile、Docker 配置、README 和项目文档
5. 调整系统标题、描述、AI 页面路径及相关展示文案
6. 优化安全相关工具类，增加 SM2 验签能力
7. 优化日志参数字段排除处理 采用更好的JsonNode节点树处理 性能更好 避免报错
8. 优化 岗位表增加逻辑删除字段

### 🐛 功能修复
1. 修复代码生成默认菜单上级 ID 错误
2. 修复大文件分片断点续传失败问题
3. 修复 OSS 路径风格、配置切换、文件下载异常
4. 修复多次驳回无法锁定审批人问题
5. 修复“我的已办”接口报错问题
6. 修复多数据库 SQL 语法兼容问题
7. 修复前端输入性 CVE 漏洞，禁止代码生成到本地路径
8. 修复手机号/邮箱格式校验错误
9. 修复 DeptExcelConverter 内存泄漏问题
10. 修复接口文档、Mapper 执行异常
11. 修复登录日志路由名错误
12. 修复租户删除后 SQL 执行异常
13. 修复短信/邮箱验证码发送失败后仍写入缓存等异常场景
14. 修复 ValidatorUtils 空指针校验、重复提交切面过滤对象扫描等边界问题
15. 修复 Excel 级联下拉一级选项名称规则校验和重复校验问题

### 前端修改内容
1. **技术栈升级**：升级 Vue、Vue Router、Element Plus、Vite、UnoCSS、Sass、vue-tsc、Oxlint 等前端核心依赖，并适配类型检查、键盘事件和 Sass 命名空间写法
2. **工程化调整**：由 npm 迁移至 pnpm，使用 oxfmt / Oxlint 替代 Prettier / ESLint，新增 pnpm-lock.yaml，清理旧构建脚本与过时配置
3. **主题样式重构**：整体主题样式重写为卡片式布局，拆分 SCSS 文件，统一暗黑模式颜色、圆角变量、Element Plus 组件样式和页面壳样式
4. **布局与标签页**：优化 TagsView 左右滚动、右侧下拉、单独刷新、全屏显示、持久化标签页、快速刷新 404 和动态路由缓存清理问题
5. **菜单与路由**：重写菜单搜索，优化动态路由组件解析性能，支持路由 ext 扩展数据，菜单管理增加类型、激活菜单、隐藏和禁用图标展示
6. **消息推送**：适配 common-push，移除旧 SSE / WebSocket 工具，新增统一 push 工具、消息类型/来源/跳转路径、消息盒子分组与已读未读联动
7. **AI 功能**：新增 snail-ai 集成与 AI 聊天页面，补充 AI Agent API、聊天输入区、主面板和侧边栏模块
8. **代码生成器**：新增前端代码生成模板，支持多前端模板选择，适配后端生成器增强字段、导出、状态切换、排序、组合唯一校验等配置
9. **系统管理页面**：优化用户、角色、菜单、部门、字典、客户端、OSS、通知公告等页面，新增用户详情抽屉、客户端白名单路径/IP、角色菜单权限与数据权限整合
10. **工作流页面**：优化流程定义、流程实例、待办/已办/抄送、审批记录、办理人展示和设计器页面，新增工作流权限标识符适配
11. **上传与富文本**：优化文件/图片上传 token 过期处理和 loading 关闭问题，富文本编辑器改用 wangeditor-next，并增加富文本内容 XSS 过滤与 OSS 内容解析工具
12. **通用组件与 Hooks**：新增 TreePanel、UserNameDisplay、useLoading、useFormDialog、useSearchToggle、useTableSelection、useTreeCollapsed 等通用组件与 hooks，简化页面编码
13. **安全与数据处理**：登录“记住我”仅保存用户名和 rememberMe 并清理历史明文密码缓存，修复默认密码覆盖、雪花 ID 精度丢失、前端输入性 CVE 等问题
14. **性能与稳定性**：优化 loadView 查找、generateRoutes 克隆、useDict 并发去重、上传 headers 响应式、TagsView 内存泄漏、ECharts resize 监听和 SSE watcher 清理
15. **功能修复**：修复 SvgIcon 空图标白屏、图标选择 Tooltip 错位、字典筛选框图标状态、部门树禁用部门不显示、文件下载异常、表单滚动背景透明、OSS 配置状态等问题

### React 前端版本（plus-ui-react）
1. 新增官方 React 前端版本 `plus-ui-react`，作为 6.X 前端可选实现，适配 RuoYi-Vue-Plus 后端接口与权限体系
2. 技术栈采用 React 19 + TypeScript + Ant Design + Umi Max + Vite，配套 Zustand、TanStack Query、Ahooks、ECharts、WangEditor-Next、Ant Design Pro Components 等生态
3. 工程链路统一使用 pnpm、oxfmt、Oxlint、TypeScript 6、OpenAPI，要求 Node >= 20、pnpm >= 10，提升构建、格式化、类型检查和接口类型维护效率
4. 完成后台基础能力适配，覆盖登录认证、动态路由、菜单权限、字典、参数、通知公告、文件管理、在线用户、操作日志、登录日志、缓存监控等常用模块
5. 完成系统管理核心页面适配，支持用户管理、角色管理、菜单管理、部门管理、岗位管理、客户端管理、OSS 文件与配置管理等功能
6. 完成工作流相关页面适配，支持流程分类、流程定义、流程实例、待办、已办、抄送、审批记录、流程图和流程设计器等业务场景
7. 新增 AI 聊天页面与 AI Agent 接口适配，支持 6.X snail-ai 能力在 React 前端中展示与使用
8. 新增消息盒子与消息推送能力，支持消息类型、消息来源、跳转路径、已读未读状态等交互
9. 新增通用组件与业务组件封装，包括 TagsView、菜单搜索、布局设置、树面板、用户选择、文件/图片上传、富文本编辑、JSON 展示、审批组件等
10. 新增通用 hooks 与工具封装，覆盖字典加载、日期范围查询、表格选择、导出、树表展开、上传处理、权限校验、菜单处理、XSS 过滤等常见场景
11. 移除多租户相关前端页面与接口，保持与 6.X 后端整体移除多租户的架构一致
12. React 版本与 Vue 版本并行维护，开发者可根据团队技术栈选择 Vue + Element Plus 或 React + Ant Design 前端实现


## v2.6.1 - 2026-04-24
## v2.6.0 - 2026-03-24
## v2.5.3 - 2026-01-23
## v2.5.2 - 2025-12-23
## v2.5.1 - 2025-10-28
## v2.5.0 - 2025-09-22
## v2.4.1 - 2025-07-01
## v2.4.0 - 2025-05-29
## v2.3.0 - 2025-03-28
## v2.2.2 - 2024-10-25
## v2.2.1 - 2024-08-26
## v2.2.0 - 2024-07-09
## v2.1.2 - 2023-12-22
## v1.8.2 - 2023-11-27
## v2.1.1 - 2023-11-14
## v1.8.1 - 2023-09-26
## v2.1.0 - 2023-09-06
## v1.8.0 - 2023-07-11
## v2.0.0 - 2023-06-15
## v1.7.0 - 2023-05-10
## v1.6.0 - 2023-03-14
## v1.5.0 - 2023-01-13
## v1.4.0 - 2022-12-01
## v1.3.0 - 2022-09-29
## v1.2.0 - 2022-08-09
## v1.1.0 - 2022-07-18
## v1.0.0 - 2022-06-20
## v0.12.0 - 2022-05-31
## v0.11.0 - 2022-05-10
## v0.10.0 - 2022-04-13
## v0.9.0 - 2022-03-04
## v0.8.0 - 2022-02-21
## v0.7.0 - 2022-02-16
## v0.6.0 - 2022-02-09
## v0.5.0 - 2022-01-28
## v0.4.0 - 2022-01-21
## v0.3.0 - 2022-01-10
## v0.2.0 - 2022-01-05
## v0.1.0 - 2021-12-31
