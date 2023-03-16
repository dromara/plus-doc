# 更新日志
- - -
## v1.6.0 - 2023-03-14

### 重大更新

[重大更新] add 新增 通用翻译模块 `ruoyi-common-translation` 实现(部门名、字典、oss、用户名)
[重大更新] add 新增 数据加解密模块 `ruoyi-common-encrypt`


### 依赖升级

* update springboot 2.7.7 => 2.7.9
* update springcloud 2021.0.5 => 2021.0.6
* update easyexcel 3.1.5 => 3.2.1
* update redisson 3.19.1 => 3.20.0
* update springdoc 1.6.14 => 1.6.15
* update hutool 5.8.12 => 5.8.15 (13与14有问题勿使用)
* update logstash-sdk 7.1.1 => 7.2
* update aws-java-sdk-s3 1.12.373 => 1.12.400
* update tencent-sms 3.1.660 => 3.1.687
* update skywalking 8.9.1 => 9.3.0
* update skywalking-agent 8.13.0 => 8.14.0
* update dubbo 3.1.4 => 3.1.7 解决dubbo报一些无用警告问题
* update element-ui 2.15.10 => 2.15.12

### 功能更新

* update 优化 修改 oss 配置页面开关说明 避免造成误解
* update 优化 `gateway` 对接 `sentinel` 使用网关特定模式
* update 优化 转移 `logback-common` 配置到 `common-web` 模块 `gateway` 单独处理
* update 优化 调整连接池默认参数
* update 优化 `zookeeper` 自带控制台占用 `8080` 端口
* update 优化 `DictDataMapper` 注解标注过期 推荐使用 `@Translation` 注解
* update 优化 获取菜单数据权限接口 删除无用角色属性与逻辑
* update 优化 调整连接池最长生命周期 防止出现警告
* update 优化 连接池增加 `keepaliveTime` 探活参数
* update 优化 `DataPermissionHelper` 增加 `开启/关闭` 忽略数据权限功能
* update 重构 `OssFactory` 加载方式 改为每次比对配置做实例更新
* update 优化 更新角色后踢掉所有相关的登录用户 用户量过大会导致redis阻塞卡顿(应粉丝要求)
* update 优化 翻译组件 支持返回值泛型 支持多种类型数据翻译(例如: 根据主键翻译成对象)
* update 优化 `tagsView` 右选框，首页不应该存在关闭左侧选项
* update 优化 `copyright 2023`
* update 优化 日志注解支持排除指定的请求参数
* update 优化 业务校验优化代码
* update 优化 日志管理使用索引提升查询性能
* update 优化 框架时间检索使用时间默认值 `00:00:00 - 23:59:59`
* update 优化 oss 预览使用 `ImagePreview` 组件
* update 优化 统一登录接口令牌key


### 新功能

* add 新增 数据加解密模块 测试案例
* add 新增 `StringUtils` `splitTo` 与 `splitList` 方法 优化业务代码

### 问题修复

* fix 修复 vue3模板 删除功能书写错误
* fix 修复 部分服务未开启日志存储
* fix 修复 接口问题开关不生效问题
* fix 修复 优化文件下载出现的异常
* fix 修复 修改密码日志存储明文问题
* fix 修复 代码生成 `postgreSQL` 查出多余的已删除字段

## v1.5.0 - 2023-01-13

### 重大更新

* [重大更新] 框架主体业务与代码生成器 完成 oracle postgres 多数据库类型支持(中间件不支持)
* [重大更新] 使用 spring 事件发布机制 重构登录日志与操作日志 支持多事件监听无入侵扩展
* 例如: 可以增加一个监听者将日志上传至ES等存储 对原有逻辑无影响

### 依赖升级

* update springboot 2.7.6 => 2.7.7
* update springboot-admin 2.7.7 => 2.7.10
* update dubbo 3.1.3 => 3.1.4
* update seata 1.5.2 => 1.6.1 适配升级
* update nacos 2.1.2 => 2.2.0 适配升级
* update mybatis-plus 3.5.2 => 3.5.3.1
* update sa-token 1.33.0 => 1.34.0
* update springdoc 1.6.13 => 1.6.14
* update snakeyaml 1.32 => 1.33
* update easyexcel 3.1.3 => 3.1.5
* update redisson 3.18.0 => 3.19.1
* update easy-es 1.1.0 => 1.1.1
* update hutool 5.8.10 => 5.8.11
* update aws-s3 1.12.349 => 1.12.373
* update aliyun-sms 2.0.22 => 2.0.23
* update tencent-sms 3.1.635 => 3.1.660
* update echarts 4.9.0 => 5.4.0

### 功能更新

* update 优化 BaseMapperPlus 使用 MP V3.5.3 新工具类 Db 简化批处理操作实现
* update 优化 demo服务 过滤健康检查 sql 打印
* update 优化 代码生成与框架主体使用相同的主键生成器 全局统一避免问题
* update 优化 系统登录 使用单表查询校验用户 避免多次join查询
* update 优化 适配框架多数据库支持 完成 oracle postgres 数据库适配(放弃 sqlserver 适配 原因: 基础中间件均不支持)
* update 优化 删除主 sql 内无用数据
* update 优化 删除 vue3 模板无用参数
* update 优化 重构 ExcelUtil 全导出方法支持 OutputStream 流导出 不局限于 response
* update 优化 maven 地址切换回 aliyun 仓库
* update 优化 springdoc 配置鉴权头写死问题 增加持久化鉴权头配置
* update 优化 actuator 依赖整合到 common-web 模块
* update 优化 验证码结果使用 spel 引擎自动计算
* update 优化 数据权限处理器 变量命名错误
* update 优化 去除 RedisUtils 无用继承
* update 优化 弹窗内容过多展示不全问题
* update 优化 删除 fuse 无效选项 maxPatternLength
* update 优化 minio 安装警告 使用新版本参数
* update 优化 使用 spring 事件发布机制 重构登录日志与操作日志
* update 优化 使用 spring 事件机制 重构 OssConfig 缓存更新
* update 优化 单元格合并判断cellValue是否相等方法
* update 优化 调整 gateway 拦截器执行顺序 优先处理 xss 过滤 然后进行缓存处理

### 新功能

* add 增加 GET 请求提交日期参数 默认格式化配置
* add 增加 RedisUtils 检查缓存对象是否存在方法
* add 增加 oracle postgres docker编排
* add 新增 代码生成器适配 多数据库可切换生成代码
* add 新增 oracle postgres 数据库框架sql脚本
* add 增加 DataBaseHelper 数据库助手 用于适配多类型数据库
* add 新增 BeanCopyUtils#mapToMap 方法

### 问题修复

* fix 修复 注册页面 验证码开关不生效问题
* fix 修复 新版本 dubbo-filter-seata 插件内核与seata不一致问题(临时)
* fix 修复 根据 key 更新参数配置报 null 问题
* fix 修复 用户注册 用户类型字段书写错误
* fix 修复 代码生成图片/文件/单选时选择必填无法校验问题
* fix 修复 修改参数键名时 未移除过期缓存配置
* fix 修复 内网鉴权 Filter 优先级问题 导致 websocket 连接失败
* fix 修复 gateway 流控规则生效但不显示问题
* fix 修复 新版本 Redisson 存在与 boot 2.X 的兼容性问题

## v1.4.0 - 2022-12-01

### 重大更新
* [重大更新] 新增 对接 skywalking 全功能(详细看下方新功能列表)
* [重大更新] 重构 ruoyi-nacos 使用官方依赖整合 解决一些问题 并升级 2.1.2 版本
* [重大更新] 新增 oss 私有库功能(数据库结构改动 需执行升级sql)
* [重大更新] 优化 数据源连接池从 druid 切换到 hikari(原因看文档)
* [重大更新] 新增 对接 prometheus + grafana 全功能(详细看下方新功能列表)

### 依赖升级
* update springcloud 2021.0.4 => 2021.0.5
* update springboot 2.7.4 => 2.7.6
* update springboot-admin 2.7.5 => 2.7.7
* update springdoc 1.6.11 => 1.6.13
* update poi 5.2.2 => 5.2.3
* update hutool 5.8.6 => 5.8.10
* update aliyun-sms 2.0.18 => 2.0.22
* update tencent-sms 3.1.591 => 3.1.611
* update sa-token 1.30.0 => 1.33.0
* update redisson 3.17.6 => 3.18.0
* update easy-es 1.0.2 => 1.1.0
* update easyexcel 3.1.1 => 3.1.3
* update lock4j 2.2.2 => 2.2.3
* update s3-adk 1.12.300 => 1.12.349
* update sentinel 1.8.5 => 1.8.6
* update nacos 2.1.1 => 2.1.2
* update ELK 7.17.2 => 7.17.6 升级镜像版本
* update nginx 1.21.6 => 1.22.1 修复漏洞
* update mysql-docker 8.0.29 => 8.0.31

### 功能更新
* update 优化 分页对象 PageQuery 支持多排序 适配 文件管理 页面支持多排序
* update 优化 获取用户信息getInfo接口 使用缓存数据获取
* update 优化 rpc文件上传 增加 ossId 数据返回
* update 优化 nacos 集群模式搭建 关于 nacos.home 注释说明
* update 优化 修改头像在小屏幕上页面布局错位的问题
* update 优化 oss 云厂商增加 华为obs关键字
* update 优化 重置时取消部门选中
* update 优化 新增返回警告消息提示
* update 优化 抽取 logback 通用配置 logback-common.xml 简化其他服务日志文件书写
* update 更改 nacos 配置文件目录 从dev文件夹迁移到nacos文件夹与其他配置区分
* update 优化 gateway 只缓存body
* update 优化 Dockerfile 创建目录命令简化操作
* update 优化 gateway filter顺序 与 代码工具封装
* update 优化 将空 catch 块形参重命名为 ignored
* update 优化 satoken 依赖传递
* update 优化 重写字典查询 使用本地缓存优化网络开销 提升到上级实现减少rpc调用频率 使用流处理减少字符串操作
* update 优化 减小腾讯短信引入jar包的体积
* update 优化 简化一些方法的写法
* update 优化 消除Vue3控制台出现的警告信息
* update 优化 忽略不必要的属性数据返回
* update 优化 重构 mysql-jdbc 依赖到 mybatis 包内 替换为最新坐标

### 新功能
* add 新增 所有服务 docker 部署对接 skywalking
* add 新增 三大 mq 整合 skywalking
* add 新增 seata 整合 skywalking 手动编译 seata 插件包
* add 新增 ruoyi-common-skylog 整合 skywalking 日志推送
* add 增加 skywalking docker编排
* add 增加 ruoyi-seata-server redis模式配置
* add 新增 ruoyi-common-prometheus 模块 用于对接 prometheus 监控
* add 新增 docker prometheus + grafana 容器编排
* add 新增 ruoyi-monitor 监控服务 提供 prometheus http_sd 服务发现功能
* add 新增 所有服务整合 ruoyi-common-prometheus 模块
* add 新增 grafana 监控大屏配置文件(框架定制)
* add 新增 使用 mica-metrics 为 undertow 提供健康检查
* add 新增 字典数据映射翻译注解
* add 增加 RedisUtils 获取缓存Map的key列表

### 问题修复
* fix 修复 开启账号同端互斥登录 被顶掉后登出报null异常问题
* fix 修复 设置NameMapper导致队列功能异常问题
* fix 修复 EnvironmentPostProcessor 不生效问题
* fix 修复 文件上传组件格式验证问题
* fix 修复 ruoyi-xxl-job-admin 服务健康检查配置缺失问题
* fix 修复 Excel导出字典值转换方法由于内部调用缓存不生效bug
* fix 修复 SysOss 方法内部调用导致缓存不生效 bug
* fix 修复 主题颜色在Drawer组件不会加载问题
* fix 修复 修改用户信息 校验用户名未排除当前用户问题
* fix 修复 升级 nginx 修复漏洞 https://www.oschina.net/news/214309
* fix 修复 用户编辑时角色和部门存在无法修改情况
* fix 修复 RemoteDictServiceImpl 代理对象获取异常bug
* fix 修复 菜单激活无法填充颜色 去除某些svg图标的fill属性
* fix 修复 使用透明底png图片时, 自动填充黑色背景
* fix 修复 table中更多按钮切换主题色未生效修复问题
* fix 修复 dubbo 使用 tri 协议 header 请求头变为小写导致无法获取参数问题
* fix 修复 DubboRequestFilter 优先级过高导致的 skywalking tid 取不到问题
* fix 修复 前端脚本乱码问题
* fix 修复 WebFluxUtils 读取空 body 报 null 问题
* fix 修复 Log注解GET请求记录不到参数问题
* fix 修复 某些特性的环境生成代码变乱码TXT文件问题
* fix 修复 开启TopNav没有子菜单隐藏侧边栏
* fix 修复 回显数据字典数组异常问题
* fix 修复 升级 satoken 导致白名单热更不生效问题
* fix 修复 swagger 版本与 springdoc 版本不一致导致找不到class问题
* fix 修复 grafana 监控模板绑定数据源ID 导致无法正常读取数据问题

## v1.3.0 - 2022-09-29

### 重大更新

* [重大更新] 新增 ruoyi-nacos 源码集成 nacos 服务端控制台 支持单机/集群模式
* [重大更新] 重写 spring-cache 实现 更人性化的操作 支持注解指定ttl等一些参数
* [重大更新] 新增 RuoYi-Cloud-Plus-UI 项目 Vue3 前端分支
* [重大更新] 移除maven docker插件 过于老旧功能缺陷大 使用idea自带的docker插件替代
* [重大更新] 优化 ruoyi-common-job 支持通过调度中心服务名注册 xxl-job-admin
* [重大更新] 新增 ruoyi-common-sentinel 模块 支持使用服务名注册 sentinel 控制台

### 依赖升级

* update spring-cloud 2021.0.3 => 2021.0.4
* update springboot 2.7.2 => 2.7.4
* update springboot-admin 2.7.3 => 2.7.5
* update sentinel 1.8.4 => 1.8.5 集成新 dubbo3 插件
* update springdoc 1.6.9 => 1.6.11
* update easy-es 0.9.80 => 1.0.2
* update dubbo 3.0.10 => 3.1.1
* update redisson 3.17.5 => 3.17.6
* update druid 1.2.11 => 1.2.12
* update hutool 5.8.5 => 5.8.6
* update dynamic-ds 3.5.1 => 3.5.2
* update aws-java-sdk-s3 1.12.264 => 1.12.300
* update aliyun-sms 2.0.16 => 2.0.18
* update tencent-sms 3.1.555 => 3.1.591
* update snakeyaml 1.30 => 1.32

### 功能更新

* update 优化 getLoginId 增加必要参数空校验
* update 优化 将 elasticsearch 解压后放入 避免造成用户误解
* update 优化 修改资料头像与部门被覆盖的问题
* update 优化 字典管理操作类型新增其他
* update 优化 使用 spring-cache 注解优化缓存
* update 优化 easy-es.enable=false 关闭 actuator 健康检查
* update 优化 优化多角色数据权限匹配规则
* update dubbo 升级 3.1.0 删除自行处理的源码修复 采用官方修复后的代码
* update 优化 页面内嵌iframe切换tab不刷新数据
* update 优化 调整 oss表key 与 ossconfig的service 字段长度不匹配
* update 优化 操作日志密码脱敏
* update 优化 补全缺失的接口 更改更新日志链接
* update 优化 插入 SysOperLog 时, 限制 operUrl 属性的长度
* update 优化 satoken 鉴权拦截器 优化多次校验

### 新功能

* add 增加 项目中使用到的请求头放行跨域
* add 新增 获取oss对象元数据方法
* add 新增 字典管理操作类型 其他

### 问题修复

* fix 修复 个人中心卡死或鼠标点击和键盘输入无效
* fix 修复 BaseMapperPlus 方法命令不一致问题
* fix 修复 图片预览组件src属性为null值控制台报错问
* fix 修复 短信功能是否启用判断不生效
* fix 修复 web模块 不引入nacos依赖报错问题
* fix 修复 sentinel 构建无法读取webapp目录问题
* fix 修复 菜单管理遗漏的prop属性
* fix 修复 minio配置https遇到的问题
* fix 修复 点击删除后点击取消控制台报错问题
* fix 修复 文件/图片上传组件 第一次上传报错导致后续上传无限loading问题
* fix 修复 ruoyi-auth 服务与 elasticsearch 端口号冲突问题
* fix 修复 ruoyi-resource 服务与 elasticsearch 端口号冲突问题
* fix 修复 角色部门状态字典错误 与 菜单注释错误
* fix 修复 hutool 存在多版本问题
* fix 修复 openapi结构体 因springdoc缓存导致多次拼接接口路径问题
* fix 修复 oss配置删除内部数据id匹配类型问题
* fix 修复 没有权限的用户编辑部门缺少数据
* fix 修复 用户导入存在则更新不生效
* fix 修复 日志转换非json数据导致报错
* fix 修复 p6spy输出sql语句时间格式化不正确问题
* fix 修复 不同网段因reset请求头导致下载导出跨域问题
* fix 修复 在线用户设置永不过期 超时时间-1推送redis无效问题
* fix 修复 snakeyaml 1.31 依旧存在漏洞 升级 1.32

## v1.2.0 - 2022-08-09

### 重大更新

* [重大更新] 新增 ruoyi-common-elasticsearch 模块 集成 easy-es 傻瓜式操作搜索引擎
* [重大更新] 新增 ruoyi-common-doc 整合 springdoc 基于 javadoc 实现无注解零入侵生成接口文档
* [不兼容更新] 移除 swagger 所属 ruoyi-doc ruoyi-common-swagger 两个模块 建议使用 ruoyi-common-doc 模块

### 依赖升级

* update springboot 2.6.9 => 2.7.2 重构使用最新自动配置方式
* update springboot-admin 2.6.7 => 2.7.3
* update dubbo 3.0.9 => 3.0.10
* update redisson 3.17.4 => 3.17.5
* update hutool 5.8.3 => 5.8.5
* update okhttp 4.9.1 => 4.10.0
* update aws-java-sdk-s3 1.12.248 => 1.12.264 修复依赖安全漏洞
* update aliyun.sms 2.0.9 => 2.0.16
* update tencent.sms 3.1.537 => 3.1.555
* update guava 30.0-jre => 31.1-jre

### 功能更新

* update 修改 资源服务 不提供默认短信 sdk 依赖
* update 优化表格上右侧工具条（搜索按钮显隐&右侧样式凸出）
* update 优化 前后端多环境部署保持一致 删除无用环境文件
* update 优化 错误登录锁定与新增解锁功能
* update 优化字典数据使用store存取
* update 优化布局设置使用el-drawer抽屉显示
* update 更新框架文档 专栏与视频 链接地址
* update 优化 对象上传 主动设置文件公共读 解决天翼云OSS文件私有问题
* update 优化 网关验证码过滤器 路径匹配改为严格匹配
* update 优化 数据导致权限生成 SQL 重复问题

### 新功能

* add 增加 全局跨域过滤器 处理跨域请求 适配移动端访问
* add 增加 搜索引擎 crud 演示案例

### 问题修复

* fix 防止date-picker组件报错，降级element-ui版本
* fix 修复 RedisUtils 并发 set ttl 错误问题
* fix 防止vue3主键字段名与row或ids一致导致报错的问题
* fix 修复 幂等组件 逻辑问题导致线程变量未清除
* fix 修复 图片回显查询 路径错误问题
* fix 修复 脱敏没有实现类导致返回数据异常问题
* fix 修复 xxljob 错误导入配置文件引发的问题
* fix 修复 gateway模块 dockerfile 端口编写错误
* fix 修复用户导出字典使用错误
* fix 修复 demo 模块 远程调用失败问题
* fix 修复 sentinel 控制台未适配 springboot 2.6 新路由策略导致无法登录问题

## v1.1.0 - 2022-07-18

### 重大更新

* [重大更新] 新增 ELK 分布式日志中心整合
* [重大更新] 新增 ruoyi-stream-mq 演示模块 完成 RabbitMQ RocketMQ Kafka 整合
* [重大更新] 优化 docker 部署方式 使用 host 模式简化部署流程 降低使用成本
* [重大更新] 调整 dubbo 服务注册命名空间与 cloud 服务保持一致 通过注册组区分访问服务
* [安全性] 优化 nginx 限制外网访问内网 actuator 相关路径 建议升级

### 依赖升级

* update springboot 2.6.8 => 2.6.9
* update easyexcel 3.1.0 => 3.1.1
* update hutool 5.8.2 => 5.8.3
* update redisson 3.17.2 => 3.17.4
* update aws-java-sdk-s3 1.12.215 => 1.12.248
* update tencentcloud-sdk-java 3.1.500 => 3.1.537
* update dubbo 3.0.8 => 3.0.9
* update seata 1.5.1 => 1.5.2

### 功能更新

* update 增加 redisson key 前缀配置
* update 优化 DateColumn 支持单模板多key场景
* update 优化部署脚本 增加 elk kafka rabbitmq rocketmq 等配置
* update 修改 oss 客户端自定义域名 统一使用https开关控制协议头
* update 优化 使用 StreamUtils 简化业务流操纵
* update 优化 ruoyi-demo 模块 去除用不上的 seata 依赖
* update 优化 接口文档 接口地址与服务地址不匹配问题
* update 优化字典数据回显样式下拉框显示值
* update 默认不启用压缩文件缓存防止node_modules过大
* update 优化登出方法

### 新功能

* add 增加 rocketmq docker编排
* add 新增 rabbitmq docker编排 包含延迟插件
* add 新增 kafka docker编排
* add 增加 es ik 分词器插件集成
* add 增加 StreamUtils 流工具 简化 stream 流操纵

### 问题修复

* fix 修复 获取 SensitiveService 空问题 增加空兼容
* fix 修复 演示页面导出路径错误
* fix 修复 minio 上传自定义域名回显路径错误问题
* fix 修复 hutool 工具返回不可操纵类型 导致报错问题
* fix 修复 远程调用短信功能返回实体 SysSms 序列化报错问题
* fix 修复 复制过程错误 导致演示excel文件损坏问题
* fix 修复 dubbo 注册组不生效问题 通过覆盖源码方式
* fix 修复代码生成首字母大写问题


## v1.0.0 - 2022-06-20

### 新增/优化 工程模块

* add 新增 ruoyi-common-alibaba-bom 工程管理 alibaba 相关依赖
* add 新增 ruoyi-common-bom 工程管理 ruoyi-common 相关依赖
* add 新增 ruoyi-api-bom 工程管理 ruoyi-api 依赖项
* add 新增 ruoyi-api-resource 模块 规范用法 移除 ruoyi-file 模块
* add 新增 ruoyi-common-web 模块 使用 undertow 替换 tomcat
* add 新增 ruoyi-common-dubbo 整合 dubbo 3.X 实现高性能 rpc 远程调用 替换 feign
* add 新增 ruoyi-common-dict 实现字典多服务调用
* add 新增 ruoyi-common-loadbalancer 自定义负载均衡模块 用于多团队开发
* add 新增 ruoyi-common-excel 模块 集成 Alibaba EasyExcel 替换 自带excel实现
* add 新增 ruoyi-common-oss 模块 支持 AWS S3 协议 分布式文件存储
* add 新增 ruoyi-common-mail 邮件模块
* add 新增 ruoyi-common-sms 短信模块 整合 阿里云、腾讯云 短信功能
* add 新增 ruoyi-common-idempotent 分布式幂等模块
* add 新增 ruoyi-common-satoken 整合 sa-token 重写所有权限
* add 新增 ruoyi-xxl-job-admin 整合 xxljob 替换 quartz 支持分布式任务调度
* add 新增 ruoyi-job 模块 统一远程处理任务 规范用法
* add 新增 ruoyi-doc 模块 集成 Knife4j 替换 swagger
* add 新增 ruoyi-seata-server 源码集成 Seata 1.5.X 服务端
* add 新增 ruoyi-sentinel-dashboard 模块 源码集成 sentinel 控制台
* update 抽取所有公用配置到 maven profile 管理

### 代码依赖改动

* update SpringCloud 2021.0.3
* update 适配 SpringCloudAlibaba 2021.0.1.0 全新配置方式
* update poi 4.1.2 => 5.2.2 性能大幅提升
* update 重构 整合 jackson 替换 fastjson
* update 重构 整合 redisson 客户端
* update 重构 整合 mybatis-plus
* update 重写 数据权限实现 基于 mybatis-plus
* add 增加 lombok 优化原生代码
* add 整合 hutool 优化相关代码
* add 新增 国际化 功能
* add 新增 lock4j 分布式锁
* add 增加监控中心 在线日志监控 优化日志文件格式
* add 适配 docker 部署方式

### 后续/进行中计划

* 增加 Vue3 前端工程
* 应用模块 适配 Oracle、PostgreSQL、SQLServer
* 增加 SpringCloud Stream 支持
* 适配 Apache Kafka、Apache RocketMQ、RabbitMQ
* 适配 ElasticSearch 分布式搜索引擎
* 适配 Alibaba Canal 分布式数据同步中心
* 适配 Apache SkyWalking 分布式链路追踪监控中心
* 适配 ELK 分布式日志中心
* 适配 Prometheus、Grafana 分布式全方位数据大屏监控
