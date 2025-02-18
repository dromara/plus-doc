# 更新日志
- - -

## v2.2.2 - 2024-10-25

### 依赖升级

* update springboot 3.2.9 => 3.2.11
* update anyline 20240808 => 20241022
* update sms4j 3.3.2 => 3.3.3
* update easyexcel 4.0.2 => 4.0.3
* update redisson 3.34.1 => 3.37.0
* update mybatis-plus 3.5.7 => 3.5.8
* update sa-token 1.38.0 => 1.39.0
* update aws-s3 2.25.15 => 2.28.22
* update aws-crt 0.29.13 => 0.31.3
* update mapstruct-plus 1.4.4 => 1.4.5

### cloud内容更新

* update 优化 将ip2region.xdb文件转移到web包下 防止其他项目使用core包打包太大问题
* update 优化 增加dubbo元数据中心 redis集群配置示例
* fix 修复 经过加密的请求无法过滤xss问题 将xss实现从gateway移动到common-web解密后过滤

### 功能更新

* update 优化 适配mp新版本 方法名改动
* update 优化 redis操作 如果无法忽略租户id则全局处理
* update 优化 sse 异常单独处理 避免出现异常报错问题
* update 优化 删除掉有问题的方法(使用RedisUtils)
* update 优化 全局开启xss过滤 提高安全性 与cloud版本保持一致
* update 优化 去除返回前端的异常信息里包含html标签问题
* update 优化 查询表名列表增加注释 (感谢 AprilWind)
* update 优化 判断当前会话是否已经登录
* update 优化 删除不应该set的属性
* update 优化 租户状态更改接口严谨性
* update 优化 postgres适配findInSet写法 提高查询效率
* update 优化 过滤器初始化写法
* update 优化 监听器兼容所有demo案例
* update 优化 操作日志记录DELETE请求参数
* update 优化 snailjob客户端ip配置说明
* update 优化 补全 pg 数据类型
* update 优化 统一sql文件命名方式
* update 优化 提供生产环境默认组配置
* update 优化 通过角色ID查询用户逻辑 (感谢 AprilWind)
* update 优化 查询用户时多余重复判断以及去重 (感谢 AprilWind)
* update 优化 连接SSE token过期导致的 Servlet异常
* update 优化 代码生成菜单id匹配写法
* update 优化 更新sql关键字
* update 优化 删除多余的引号
* update 优化 RegexUtils#extractFromString 方法未匹配返回null不返回默认值问题
* update 优化 oss上传直接从请求头获取文件类型
* update 优化 代码生成表名判断 使用开头判断避免误判
* update 优化 excel导入 适配异常结构
* update 优化 删除okhttp无用版本限制(spring已经限制过了)
* update 优化 自行开启云存储访问控制ACl策略注释 (感谢 AprilWind)
* update 优化 admin监控 账号密码 从pom配置文件读取
* update 优化 操作日志查询代码

### 功能新增

* add 新增 TreeUtil获取节点列表中所有节点的叶子节点 (感谢 AprilWind)
* add 新增 同步租户字典功能

### 问题修复

* fix 修复 设置流程变量 代码使用错误问题
* fix 修复 xss过滤器 未过滤url参数问题
* fix 修复 代码书写错误
* fix 修复 及其特殊场景下获取 StopWatch 为null问题
* fix 修复 重新生成租户ID未生效的问题 (感谢 秋辞未寒)
* fix 修复 oss上传10秒超时，设置默认时间一分钟 (感谢 AprilWind)
* fix 修复 腾讯云oss不支持高危权限设置ACL (感谢 AprilWind)
* fix 修复 同步云厂商要求明确配置访问样式（路径样式访问） (感谢 AprilWind)
* fix 修复 特性情况下自定义验证异常处理器报null问题
* fix 修复 EncryptorManager 缓存失效问题导致的内存膨胀
* fix 修复 同一个用户不同token连接不同服务导致发送不到问题(改为全局发送)
* fix 修复 同步字典存储是未忽略租户
* fix 修复 部分web异常被CryptoFilter截胡问题
* fix 修复 postgres sql文件菜单挂载错误 (感谢 Zyyi)
* fix 修复 代码生成器 postgres 数据库主键类型映射错误问题
* fix 修复 临时处理 scala库版本漏洞问题
* fix 修复 工作流的分页查询语句不兼容sqlserver的问题 (感谢 sushuai)
* fix 修复 commons-io 依赖冲突问题
* fix 修复 开启子部门 父部门未关联开启问题
* fix 修复 升级依赖导致的依赖冲突

### 前端改动

* update 优化 流程提交用户id使用字符串提交避免雪花id失真问题
* add 增加 SSE功能开关 (感谢 陈西瓜i)
* fix 修复 请假日期选择格式不对问题
* fix 修复 登录日志excel导出名称错误
* fix 修复 重新登录无法跳转到过期前页面问题
* fix 修复 租户套餐导出路径编写错误


## v2.2.1 - 2024-08-26

### 重大改动

* 增加 ruoyi-common-sse 模块 支持SSE推送 比ws更轻量更稳定的推送
* 增加 springboot snailjob 等 actuator 账号密码认证 杜绝内外网信息泄漏问题
* 增加 重构代码生成器 集成anyline开源框架 支持400+种数据库适配

### 依赖升级

* update springboot 3.2.6 => 3.2.9
* update snailjob 1.0.1 => 1.1.2
* update mapstruct-plus 1.4.3 => 1.4.4
* update hutool 5.8.27 => 5.8.31 解决hutool不兼容jakarta问题
* update anyline 8.7.2-20240808
* update sms4j 3.2.1 => 3.3.2
* update redisson 3.31.0 => 3.34.1
* update mapstruct-plus 1.3.6 => 1.4.3
* update lombok 1.18.32 => 1.18.34
* update easyexcel 3.3.4 => 4.0.2
* update springdoc 2.5.0 => 2.6.0
* update flowable 7.0.0 => 7.0.1

### cloud内容更新

* update springcloud 2023.0.2 => 2023.0.3
* update springcloud-alibaba 2023.0.1.0 => 2023.0.1.2
* update redis 6.2.7 => 6.2.12 解决订阅key报错问题
* update 优化 seata dockerfile 增加环境变量
* update 优化 增加日志处理器顺序说明
* update 优化 使用 seata-server 官方依赖简化seata集成方式
* update 优化 屏蔽 sentinel 心跳日志
* update 优化 dubbo元数据注册redis支持timeout(注意时间必须使用数字)
* update 优化 调整sentinel日志级别 屏蔽心跳日志
* update 优化 sky-agent 默认开启即使连不上服务端也跟踪配置 (有些人就爱这么用)
* update 优化 kafka 自动创建 topic 部分人副本数不够报错问题
* add 增加 nacos sentinel snailjob 健康检查 actuator 账号密码认证
* fix 修复 dubbo redis元数据中心 获取监听器null问题
* fix 修复 nacos sentinel seata 不适配新版undertow问题 先换回tomcat
* fix 修复 依赖漏洞 限制部分依赖版本
* fix 修复 由于alibaba sentinel 初始化机制变更导致的无法连接问题
* fix 修复 dubbo 日志输出异常判断错误
* remove 删除 kafka-streams 所有人都不会用也不学怎么用 删除了事

### 功能更新

* update 优化 去除日志部署环境判断 通过日志级别控制
* update 优化 忽略租户与忽略数据权限支持嵌套使用(感谢 amadeus5201)
* update 优化 租户相关controller 增加租户开关配置控制是否注册
* update 优化 移除 alibaba ttl 与线程池搭配有问题(可传递但无法清除与更新)
* update 优化 个人中心编辑 忽略数据权限
* update 优化 兼容部分用户不想给用户分配角色与部门的场景
* update 优化 租户套餐重名校验
* update 优化 部门下存在岗位不允许删除
* update 优化 角色编辑状态未校验问题
* update 优化 用户脱敏增加编辑权限标识符
* update 优化 代码生成器 自动适配oss翻译
* update 优化 临时升级 undertow 版本 解决虚拟线程溢出问题
* update 优化 支持通过配置文件关闭工作流
* update 优化 增加mybatis-plus填充器兜底策略
* update 优化 TenantSpringCacheManager 处理逻辑
* update 优化 角色权限判断
* update 优化 增加删除标志位常量优化查询代码
* update 优化 监控使用独立web依赖
* update 优化 更多脱敏策略(感谢 hemengji)
* update 优化 设置nginx sse相关代理参数
* update 优化 调整默认推送使用SSE
* update 优化 Monitor监控服务通知分类打印(感谢 AprilWind)
* update 优化 限流注解 又写key又不是表达式的情况
* update 优化 WorkflowUtils查询用户信息发送消息未查询邮件和手机号(感谢 yanzy)
* update 优化 注释掉其他数据库 jdbc 依赖 由用户手动添加
* update 优化 oracle snailjob 兼容低版本oracle索引名称长度限制
* update 优化 数据权限支持通过菜单标识符获取数据所有权
* update 优化 数据权限支持自定义连接符
* update 优化 TestDemo 删除前校验数据权限
* update 优化 更换docker镜像底层系统 避免无字体情况

### 问题修复

* fix 修复 三方登录构建去除无用代码
* fix 修复 多线程对同一个session发送ws消息报错问题
* fix 修复 依赖漏洞 限制部分依赖版本
* fix 修复 excel 基于其他字段 合并错误问题
* fix 修复 一级缓存key未区分租户问题
* fix 修复 id字符串格式转换错误问题
* fix 修复 登出无法正确删除对应的租户数据问题
* fix 修复 登录错误锁定不区分租户问题
* fix 修复 转换模型缺少分类字段
* fix 修复 权限标识符处理未设置成功状态问题
* fix 修复 无法导入 bpmn 类型文件问题

### 前端改动

* update element-plus 2.7.5 => 2.7.8
* update vue 3.4.25 => 3.4.34
* update vite 5.2.10 => 5.2.12
* add 增加 使用 vueuse 编写 sse 推送功能
* update 优化 使用匹配模式简化预编译配置
* update 优化 时间搜索组件统一
* update 优化 oss 配置按钮 使用ossConfig权限标识符与oss权限分离
* update 优化 类型报错问题
* update 优化 切换租户后刷新首页
* update 优化 实现表格行选中切换
* update 优化 使用 vueuse 重构 websocket 实现
* update 优化 代码生成器编辑页禁用缓存 防止同步后页面不更新问题
* update 优化 调整默认推送使用SSE
* fix 修复 租户套餐导出路径错误问题
* fix 修复 登出后重新登录 sse推送报错问题


## v2.2.0 - 2024-07-09

### 重大更新

* [重大更新] 使用 caffeine 重构 PlusSaTokenDao 层实现 减少将近90%的redis查询提高性能
* [重大更新] 新增 PlusCacheWrapper 装饰器 为 SpringCache 增加本地缓存减少redis查询提高性能
* [重大更新] 升级 awsS3 到2.X版本 支持异步与自动分片上传下载(感谢 AprilWind)
* [重大更新] 新增 flowable 工作流功能(感谢 May)
* [重大更新] 新增 snailjob 调度中心 移除 powerjob (投诉的人太多) (感谢 dhb52)
* [重大更新] 重构 将spring-cloud-stream改为普通的mq依赖用法(感谢 Xbhog)
* [重大更新] 新增 ruoyi-common-bus 消息总线组件 基于MQ跨服务投递事件消息

### 依赖升级

* update springboot 3.1.7 => 3.2.6 支持虚拟线程
* update springboot-admin 3.1.8 => 3.2.3
* update springdoc 2.2.0 => 2.5.0
* update redisson 3.24.3 => 3.29.0 支持虚拟线程
* update hutool 5.8.22 => 5.8.26
* update dynamic-ds 4.2.0 => 4.3.0
* update mybatis-plus 3.5.4 => 3.5.7 修复与boot代码冲突问题
* update lock4j 2.2.5 => 2.2.7 消除启动警告
* update sms4j 2.2.0 => 3.2.1 支持自定义配置key 可用于多厂商多租户等
* update mapstruct-plus 1.3.5 => 1.3.6
* update easyexcel 3.3.3 => 3.3.4
* update lombok 1.18.30 => 1.18.32
* update satoken 1.37.0 -> 1.38.0
* update aws-oss 1.12.600 => 2.25.15

### 功能更新

* update 优化 StreamUtils 抽取 findFirst findAny 方法
* update 优化 更新使用 Spring 官方推荐 JDK
* update 优化 webscoket 配置与异常拦截
* update 优化 isTenantAdmin 空校验
* update 优化 修改路由name命名规则(感谢 玲娜贝er)
* update 优化 大数据量下join卡顿问题 使用子查询提高性能
* update 优化 用户ID查询角色列表(感谢 AprilWind)
* update 优化 获取用户账户(感谢 AprilWind)
* update 优化 租户列表接口 避免登录之后列表被域名过滤
* update 优化 三方登录不同域名获取不到租户id问题
* update 优化 获取aop代理的方式 减少与其他使用aop的功能冲突的概率
* update 优化 临时解决 spring 启动报 warn 问题
* update 优化 移除表单构建菜单(没有可用组件 用处不大以后再考虑)
* update 优化 修改用户信息接口(感谢 AprilWind)
* update 优化 切换动态租户 默认线程内切换(如需全局 手动传参)
* update 优化 适配最新前端代码生成模板
* update 优化 代码生成 el-radio 标签过期属性
* update 优化 文件下载(使用对流传递 降低内存使用量)(感谢 秋辞未寒)
* update 优化 去除gc日志参数(有需要自己加)
* update 优化 拆分异常处理器
* update 优化 常规web异常状态码
* update 优化 设置静态资源路径防止所有请求都可以访问静态资源
* update 优化 代码生成表导入 排除工作流相关表
* update 优化 redis 对Long值的存储类型不同问题
* update 优化 去除加密请求类型限制
* update 优化 mp多租户插件注入逻辑
* update 优化 移除删表语句 用户自行处理
* update 优化 RedisUtils 支持忽略租户
* update 更新 ip地址 xdb文件
* update 优化 新增修改菜单权限字符校验
* update 优化 验证码背景色改为浅灰色
* update 优化 更新 mybatis 多包扫描配置
* update 优化 RateLimiter 注解使用体验(感谢 ly-chn)
* update 优化 GET 方法响应体支持加密
* update 优化 excel 单元格合并可以基于注解选择需要依赖哪些字段(感谢 司猫子)
* update 优化 OssFactory 获取实例锁性能(感谢 fanc)
* update 优化 登录消息 支持集群发送
* update 优化 数据权限 使用预扫描mapper注解提升代码性能
* update 优化 数据加密 使用预扫描实体类提升代码性能(感谢 老马)
* update 优化 Async 针对虚拟线程配置 与其他注意事项注释
* update 优化 框架整体sql提高查询性能
* update 优化 将p6spy配置文件统一放置到 common-mybatis 插件包内
* update 优化 使用翻译注解简化用户查询 调整用户查询逻辑


### 新增功能

* add 新增 SMS异常处理器(感谢 AprilWind)
* add 新增 在线设备管理(个人中心)(感谢 AprilWind)
* add 新增 岗位编码与部门编码 并将岗位放到部门下(感谢 秋辞未寒)
* add 新增 分布式锁Lock4j异常拦截(感谢 AprilWind)
* add 新增 BaseMapperPlus提供一组可选是否抛出异常的selectVoOne方法(感谢 秋辞未寒)
* add 新增 用户、部门、角色、岗位 下拉选接口与代码实现优化
* add 新增 JustAuth 整合 TopIam 单点登录(感谢 马铃薯头)
* add 新增 StringUtils.isVirtual 方法
* add 新增 正则工具类 字符串提取 字符串校验

### 问题修复

* fix 修复 isLogin 方法抛异常无法正常返回值问题
* fix 修复 spring路径规则 导致 actuator 被特殊方式访问问题
* fix 修复token无效时关闭ws(感谢 AprilWind)
* fix 修复 oss未使用租户 拼接租户id null问题
* fix 修复 用户昵称修改后未清除对应缓存问题
* fix 修复 文件上传图片预览问题
* fix 修复 三方账号可以被同一个用户多次绑定问题
* fix 修复 兼容redis5.0出现的问题
* fix 修复 字典键值可重复配置问题
* fix 修复 部分浏览器无法获取加密响应头问题
* fix 修复 用户未设置部门 登录报错问题
* fix 修复 全局异常处理器 空指针null问题
* fix 修复 excel 表达式字典 下拉框导出格式错误
* fix 修复 InjectionMetaObjectHandler 已存在数据依旧会获取用户信息报异常问题
* fix 修复 关闭租户功能 三方登录报错问题
* fix 修复 部门树排序问题
* fix 修复 CryptoFilter 代码逻辑问题

### 前端改动

* update 升级 element vite 版本 最低nodejs版本提升到18.18.0
* update 优化 更改客户端状态接口 使用clientId传参
* update 优化 ws开关改为常开(vite5修复了崩溃bug)
* update 优化 移除cjs
* update 优化 对Volar支持
* update 优化 富文本组件，修复两个组件上传图片位置错乱问题
* update 优化 request请求类判断请求头方式
* update 优化 密码校验策略增加非法字符限制
* update 优化 支持全局开启或关闭接口加密功能
* update 优化 暗黑模式，增加vxe的暗黑模式
* update 优化 首页打开topNav不展开菜单问题
* update 优化 el-select 与 el-input 全局样式
* update 优化 跟密码相关的默认前端关闭防重功能
* add 新增 社交登录整合 TopIam
* add 新增 图片上传组件增加压缩功能支持，可自行开关
* add 新增 vxe-table依赖支持
* add 新增 全局用户选择组件
* add 新增 工作流相关页面与组件
* add 新增 使用bpmnjs流程预览
* add 新增 在线登录设备管理(感谢 AprilWind)
* add 新增 用户选择角色时 可搜索功能(感谢 追梦稻草人Li)
* fix 修复 登录失效，重新登录丢失参数问题(感谢 爱宇阳)
* fix 修复 websocket 非index页面刷新无法重连问题
* fix 修复 全局属性找不到的问题(感谢 ahaos)
* fix 修复 vue 类型识别问题
* fix 修复 富文本编辑器 单页面多实例图片混乱问题
* fix 修复 i18n无感刷新问题
* fix 修复 文件预览大写后缀不展示的问题(感谢 北桥)
* fix 修复 面板因为min width原因收缩不全
* fix 修复 移动端下 无法展开菜单问题
* fix 修复 菜单搜索下方出现白色区域
* fix 修复 el-tag标签类型不一致问题
* fix 修复 角色必填*号

### 微服务修改

* update springcloud 2022.0.4 => 2023.0.2
* update springcloud-alibaba 2022.0.0.0 => 2023.0.1.0
* update dubbo 3.2.7 => 3.2.14
* update easy-es 2.0.0-beta4 => 2.0.0 正式版
* update nacos 2.2.1 => 2.3.2 默认开启nacos服务端授权认证 (感谢 OldDriver9527)
* update rocketmq 4.9.4 => 5.2.0 docker镜像升级
* update kafka 3.2.0 => 3.6.2 docker镜像升级
* update rabbitmq 3.10.6 => 3.13.3 docker镜像升级
* update sentinel 1.8.6 => 1.8.8
* update skywalking 9.3.0 => 9.7.0
* update skywalking-agent 8.16.0 => 9.2.0
* update 优化 dubbo 使用 redis 作为元数据中心管理 支持过期时间 避免过期数据堆积 解放nacos存储空间
* update 优化 调整配置文件语法
* update 优化 使用spring工具自定义dubbo ip获取方法(针对多网卡ip获取不正确问题)
* update 优化 common-dubbo 删除无用依赖
* update 优化 去除重复的扫描器 @EnableDubbo 会自行扫描包
* update 优化 加密组件 mp依赖改为可选
* update 优化 mybatis依赖设置为可选依赖 避免出现不应该注入的情况
* fix 修复 sentinel-dashboard的pom引入logaback冲突问题
* fix 修复 nacos 不兼容 logback 1.4 新版本问题
* fix 修复 开启数据库加密 auth服务报错问题
* fix 修复 gateway sentinel 限流报错问题(临时方案) https://github.com/alibaba/Sentinel/issues/3298


## v2.1.2 - 2023-12-22

### 依赖升级

* update springboot 3.1.5 => 3.1.7
* update springboot 2.7.17 => 2.7.18(扩展服务升级到boot2最终版本)
* update mybatis-boot 3.0.2 => 3.0.3 优化依赖传递
* update powerjob 4.3.3 => 4.3.6
* update easyexcel 3.3.2 => 3.3.3
* update transmittable-thread-local 2.14.2 => 2.14.4
* update justauth 1.16.5 => 1.16.6
* update redisson 3.24.1 => 3.24.3 修复订阅重启连接超时问题
* update easy-es 1.1.1 => 2.0.0-beta4

### 功能更新

* update 优化 oss 远程调用 支持降级处理
* update 优化 丰富RedisUtils对List Set类型的操作
* update 优化 为 admin 模块 单独增加ratelimiter模块
* update 优化 验证码接口 增加限流配置
* update 优化 excel合并注解会根据第一合并列的结果来决定后续的列合并 (感谢 Simple)
* update 优化 SocialUtils 代码
* update 优化 删除无用异常类
* update 优化 补全三方登录校验国际化
* update 优化 sms组件 预留自动配置类
* update 更新 关于数据库的说明
* update 优化 sms组件 预留自动配置类
* update 优化 将 OSS配置 改为全局模式 降低使用难度 保留sql便于用户自行扩展(常规项目用不上配置分多租户)
* update 优化 细化oss配置管理权限控制
* update 优化 开启 redisson 脚本缓存 减少网络传输
* update 优化 删除 hikaricp 官方不推荐使用的配置 jdbc4 协议自带校验方法
* update 优化 减少 PlusSaTokenDao 不必要的查询优化性能
* update 优化 更新用户异常提示 使用登录账号
* update 优化 使用登录用户判断是否登录 提高效率
* update 优化 重构 LoginHelper 将本地存储代码操作封装
* update 优化 getTenantId 判断是否开启多租户
* update 优化 Dockerfile 使用shell模式 支持环境变量传入jvm参数
* update 优化 WebSocketUtils 连接关闭改为警告
* update 优化 excel多sheet页导出 (感谢 May)
* update 优化 删除无用接口实现
* update 优化 jvm参数调整 全面启用zgc
* update 优化 使用动态租户重构业务对租户的逻辑
* update 优化 TenantHelper 动态租户支持函数式方法
* update 优化 支持多租户绑定相同的三方登录
* update 优化 更新用户登录信息方法忽略数据权限
* update 优化 补全三方绑定时间字段 删除无用excel注解
* update 优化 将登录记录抽取到监听器统一处理
* update 优化 登录消息推送异常拦截(未启动resource也不耽误用)
* update 优化 租户插件 ignoreTable 方法支持动态租户

### 新增功能

* add 新增 RedisUtils.setObjectIfExists 如果存在则设置方法
* add 新增 丰富RedisUtils对List Set类型的操作
* add 新增 翻译组件 用户昵称翻译实现
* add 新增 响应加密功能 支持注解强制加密接口数据 (感谢 MichelleChung)
* add 新增 common-ratelimiter 限流模块 用于自定义业务限流 与 sentinel不冲突

### 问题修复

* fix 修复 stream-mq 测试服务未导入租户模块 导致鉴权不一致问题
* fix 修复 使用zgc导致seata报错(未知原因 将alibaba组件全还原)
* fix 修复 sentinel 镜像添加了多余接口参数
* fix 修复 注册接口获取开关未在租户范围内问题
* fix 修复 seata-server logback版本冲突问题
* fix 修复 selectDictTypeByType 查询方法错误问题
* fix 修复 一些不正常类无法加载报错问题
* fix 修复 powerjob sql脚本针对其他数据库转义符问题 (感谢 branches)
* fix 修复 MybatisSystemException 空指针问题
* fix 修复 excel合并注解会根据第一合并列的结果来决定后续的列合并
* fix 修复 session 多账号共用覆盖问题 改为 tokenSession 独立存储
* fix 修复 token 失效后 登录获取用户null问题
* fix 修复 powerjob部署方案 高版本nginx不生效问题
* fix 修复 OssFactory 并发多创建实例问题
* fix 修复 延迟队列在投递消息未到达时间的时候 服务死机导致重启收不到消息

### 前端改动

* update 优化 用户头像 img 变量无确定类型问题
* update 优化 细化oss配置管理权限控制
* update 优化 明确打包命令
* update 优化 代码中存在的警告
* update 优化 前端白名单页面放行逻辑
* update 优化 页面关于权限标识符说明
* fix 修复 append-to-body 编写错误 (感谢 Ai3_刘小龙)
* fix 关闭动态路由tab页签时不清理组件缓存 (感谢 NickLuo)
* fix 删除重复环境变量ElUploadInstance (感谢 棉花)
* fix 修复 在线用户 强推按钮点击取消控制台警告问题
* fix 修复 字典使用 default 样式报警告问题

## v1.8.2 - 2023-11-27

### 依赖升级

* update springboot 2.7.16 => 2.7.18 升级到2.X最终版本(官方停更)
* update mybatis-plus 3.5.3.2 => 3.5.4
* update satoken 1.36.0 => 1.37.0
* update hutool 5.8.20 => 5.8.22
* update aws-java-sdk-s3 1.12.400 => 1.12.540
* update vue-quill 1.1.0 => 1.2.0

### 功能更新

* update 优化 页面关于权限标识符说明
* update 优化 数据权限拦截器优先判断方法是否有效 提高性能减少无用sql解析
* update 优化 部门数据权限使用默认兜底方案
* update 优化 补全代码生成 columnList 接口参数注解缺失
* update 优化 AddressUtils 兼容linux系统本地ip
* update 优化 操作日志 部门信息完善
* update 优化 数据权限 减少二次校验查询
* update 修改 获取用户token和后端不一致的问题 (感谢 bestrevens)
* update 优化 vue3 版本用户初始密码从字典查询
* update 优化 富文本Editor组件检验图片格式
* update 优化 操作日志列表新增IP地址查询
* update 优化 全局数据存储用户编号
* update 优化 菜单管理类型为按钮状态可选

### 问题修复

* fix 修复 OssFactory 并发多创建实例问题
* fix 修复 demo页面字段编写错误
* fix 修复 数据权限优化后 update delete 报null问题
* fix 修复 五级路由缓存无效问题
* fix 修复 oss服务无法连接
* fix 修复 内链iframe没有传递参数问题
* fix 修复 外链带端口出现的异常
* fix 修复 普通角色编辑使用内置管理员code越权问题
* fix 修复 seata XA模式缺失druid工具问题
* fix 修复 代码生成 是否必填与数据库不匹配问题
* fix 修复 富文本上传接口地址错误
* fix 修复 HeaderSearch组件跳转query参数丢失问题
* fix 修复树结构代码生成新增方法赋值错误

## v2.1.1 - 2023-11-14

### 依赖升级

* update springboot 3.1.3 => 3.1.5
* update springboot 2.7.14 => 2.7.17(扩展服务)
* update springboot-admin 3.1.5 => 3.1.7
* update satoken 1.35.0.RC => 1.37.0
* update mybatis-plus 3.5.3.2 => 3.5.4 适配mp新版本改动
* update dynamic-ds 4.1.3 => 4.2.0
* update bouncycastle 1.72 => 1.76
* update poi 5.2.3 => 5.2.4
* update redisson 3.23.2 => 3.24.1
* update hutool 5.8.20 => 5.8.22
* update lombok 1.18.26 => 1.18.30(适配支持jdk21)
* update vue-quill 1.1.0 => 1.2.0
* update seata 1.7.0 => 1.7.1
* update dubbo 3.2.5 => 3.2.7

### 功能更新

* update 优化 移除不合理的方法 携带附件的邮件建议直接集成插件发送
* update 优化 携带 clientid 跨域问题
* update 优化 数据权限拦截器优先判断方法是否有效 提高性能减少无用sql解析
* update 优化 适配 maxkey 新版本
* update 优化 @Sensitive脱敏增加角色和权限校验 (感谢 盘古给你一斧)
* update 优化 部门数据权限使用默认兜底方案
* update 优化 更改默认日志等级为info 避免日志过多(按需开启debug)
* update 优化 登录策略代码优化(感谢 David Wei)
* update 优化 补全代码生成 columnList 接口参数注解缺失
* update 优化 nginx 配置支持 websocket
* update 优化 notice 新增通知公告发送ws推送
* update 优化 websocket 模块减少日志输出 增加登录推送
* update 优化 重构登录策略增加扩展性降低复杂度
* update 优化 addressUtils 兼容linux系统本地ip
* update 优化 补全操作日志部门数据
* update 优化 支持数据库操作在非web环境下切换租户
* update 优化 排除powerjob无用的依赖 减少打包30M体积
* update 优化 删除 satoken yml 时间配置 此功能已迁移至客户端管理
* update 优化 redis 集群模式注释说明
* update 优化 客户端禁用限制
* update 优化 登录日志, 在线用户展示信息(增加 客户端, 设备类型)(感谢 MichelleChung)
* update 优化 限制框架中的fastjson版本
* update 优化 数据权限 减少二次校验查询
* update 优化 将部门id存入token避免过度查询redis
* update 优化 增加租户ID为Null错误日志
* update 优化 操作日志列表新增IP地址查询
* update 优化 通过参数键名获取键值接口的返回体(感谢 David Wei)
* update 优化 为 sys_grant_type 字典增加样式
* update 优化 代码生成 页面输入框样式
* update 优化 全业务分页查询增加排序规则避免因where条件导致乱序问题
* update 优化 登录接口租户id被强制校验问题
* update 优化 加密模块 支持父类统一使用加密注解(感谢 Tyler Ge)
* update 优化 将graalvm镜像更新为openjdk镜像 需要的人自行切换即可
* update 优化 部分使用者乱设权限导致无法获取用户信息 增加权限提示
* update 优化 表格列的显示与隐藏小组件(感谢 bestrevens)
* update 优化 增加表单构建不能使用说明
* update 优化 富文本Editor组件检验图片格式
* update 优化 操作日志列表新增IP地址查询
* update 优化 菜单管理类型为按钮状态可选
* update 优化 用户初始密码从参数配置查询
* update 优化 通过参数键名获取键值接口的返回体(感谢 David Wei)
* update 优化 字典标签支持数组和多标签(感谢 抓蛙师)

### 新增功能

* add 新增 websocket 群发功能
* add 新增 前端接入websocket接收消息(感谢 三个三)
* add 增加 rpc消息推送接口与实现
* add 新增 CacheController Redis 缓存监控接口(感谢 Michelle.Chung)

### 问题修复

* fix 修复 因扩展服务不支持boot3导致无法引入common-web包 日志写出不生效问题
* fix 修复 seata XA模式缺失druid工具问题
* fix 修复 oss服务无法连接 导致业务异常问题 查询不应该影响业务
* fix 修复 租户id为null 无法匹配字符串导致的嵌套key问题
* fix 修复 部门管理orderNum排序失效问题
* fix 修复 外链带端口出现的异常
* fix 修复 普通角色编辑使用内置管理员code越权问题
* fix 修复 代码生成 是否必填与数据库不匹配问题
* fix 修复 用户注册接口校验用户名不区分租户问题
* fix 修复 错误增加组导致的校验不生效问题
* fix 修复 新增校验主键id问题
* fix 修复 powerjob 使用 nginx 部署无法访问的问题
* fix 修复 SysUserMapper 内标签使用错误(不影响使用)
* fix 修复 新增或编辑 SysOssConfig 数据后 推送到 redis 数据不完整
* fix 修复 树表生成查询变量使用错误
* fix 修复 个人信息修改密码接口隐藏新旧密码参数明文(感谢 bleachtred)
* fix 修复 删除字段后 * update sql 未更新问题
* fix 修复 三方登录支付宝source与实际支付宝业务code不匹配问题
* fix 修复 五级路由缓存无效问题
* fix 修复 内链iframe没有传递参数问题
* fix 修复 绑定第三方帐号参数“wechar”更正为“wechat” (感谢 scmiot)
* fix 修复 用户注册缺失 clientid 问题
* fix 修复 HeaderSearch组件跳转query参数丢失问题
* fix 修复 自定义字典样式不生效的问题
* fix 修复 login 页面 loading 未关闭问题

## v1.8.1 - 2023-09-26

### 依赖升级

* update springboot 2.7.14 => 2.7.16
* update springboot-admin 2.7.10 => 2.7.11
* update satoken 1.35.0.RC => 1.36.0
* update lombok 1.18.26 =. 1.18.30
* update springboot 2.7.13 => 2.7.14
* update mybatis-plus 3.5.3.1 => 3.5.3.2
* update easyexcel 3.3.1 => 3.3.2
* update hutool 5.8.18 => 5.8.20
* update dubbo 3.1.8 => 3.1.11

### 功能更新

* update 优化 代码生成 vo实体类序列化
* update 优化 excel 导出不必要的请求头
* update 优化 字典标签支持传分隔符分隔的字符串和数组
* update 优化 控制台debuger位置错误问题 
* update 优化 TopNav 菜单样式
* update 优化 注册用户异常报错不正确问题
* update 优化 全局异常处理器 业务异常不输出具体堆栈信息 减少无用日志存储
* update 优化 用户管理 只查询未禁用的部门角色岗位数据
* update 优化 岗位如果绑定了用户则不允许禁用
* update 优化 部门与角色如果绑定了用户则不允许禁用
* update 优化 加密实现 使用 EncryptUtils 统一处理
* update 优化 适配 mysql 8.0.34 升级连接机制
* update 优化 excel导出字典转下拉框 无需标记index自动处理
* update 优化 excel 导出字典默认转为下拉框
* update 删除一些跟swagger有关的字眼 避免误解
* update 优化 角色权限支持仅本人权限查看 解决无法查看自己创建的角色问题
* update 优化 xxljob 端口随着主应用端口飘逸 避免集群冲突

### 问题修复

* fix 修复 自定义字典样式不生效的问题
* fix 修复 新建用户可能会存在的越权行为
* fix 修复 字典缓存删除方法参数错误问题
* fix 修复 修复树模板父级编码变量错误
* fix 修复 demo 模块缺少 security 依赖问题
* fix 修复 升级 mp 版本导致的问题
* fix 修复 加密模块数据转换异常问题
* fix 修复 动态设置 token 有效期不生效问题
* fix 修复 token 过期登出无法清理在线用户问题


## v2.1.0 - 2023-09-06

# 开发历程

* 2023年5月 开始 2.1.0 计划 历经1个月的设计与讨论
* 2023年6月 开始着手开发 历经2个多月的开发 特别感谢团队的小伙伴与一些热心的粉丝 参与功能开发与测试
* 2023年8月 开始公测 历经将近1个月的公测与修复工作(期间成功支持多位使用者生产使用)
* 2023年9月初 正式发布(经过多个小伙伴的生产实践 已基本可尝试生产使用)
> 关于1.X的说明 由于SpringBoot2.X与vue2.X均在11月底停止维护<br>
> 故而咱们vue版本1.X也无法再继续更新<br>
> 介于1.X的用户量特别庞大 功能也非常的稳定<br>
> 计划于11月底同Boot2.X一同停止更新但还会持续维护修复bug(修复的形式为直接提交到1.X分支停止发版)<br>

# 视频介绍

为了更好的让大家了解 2.1.0 作者录制了相关的视频 供大家快速了解上手

* 2.1.0 新功能与变更介绍: https://www.bilibili.com/video/BV1fj411y71X/

# 更新日志

### 重大更新

* [重大更新] 优化 相关代码 完成代码生成多数据源统一存储(感谢 WangBQ)
* [不兼容更新] 移除 原短信功能 集成更强大的 sms4j 短信工具包(感谢 友杰)
* [不兼容更新] 对接 powerjob 实现分布式任务调度 删除原有 xxljob 原因为社区不更新功能太少只支持mysql(感谢 yhan219)
* [重大更新] 新增 三方授权绑定登录功能 基于 justauth 支持市面上大部分三方登录(感谢 三个三)
* [不兼容更新] 新增 客户端授权功能 不需要更改任何代码即可完成多端动态对接(感谢 Michelle.Chung)
* [重大更新] 新增 前后端接口请求加密传输 基于AES+RSA动态高强度加密(感谢 wdhcr)
* [重大更新] 新增 三方授权登录 对接 maxkey 单点登录
* [不兼容更新] 优化 redis序列化配置 更改为通用格式(升级需清除redis所有数据)
* [重大更新] 新增 通过 sharding-proxy 实现分库分表(感谢 rice666 !pr94)

### 依赖升级

* update springboot 3.0.7 => 3.1.3
* update springboot-admin 3.1.3 => 3.1.5
* update springcloud 2022.0.2 => 2022.0.4
* update springcloud-alibaba 2022.0.0.0-RC2 => 2022.0.0.0
* update springdoc 2.1.0 => 2.2.0
* update spring-mybatis 3.0.1 => 3.0.2
* update mybatis-plus 3.5.3.1 => 3.5.3.2
* update easyexcel 3.2.1 => 3.3.2
* update mapstruct-plus 1.2.3 => 1.3.5 解决修改实体类 idea不编译问题
* update satoken 1.34.0 => 1.35.0.RC 优化过期配置 支持多端token自定义有效期
* update dynamic-ds 3.6.1 => 4.1.3 支持 SpringBoot3
* update sms4j 2.2.0
* update hutool 5.8.18 => 5.8.20
* update redisson 3.20.1 => 3.23.4
* update lock4j 2.2.4 => 2.2.5
* update aws-java-sdk-s3 1.12.400 => 1.12.540
* update maven-surefire-plugin 3.0.0 => 3.1.2
* update seata 1.6.1 => 1.7.0
* update sharding-proxy 5.4.0
* update dubbo 3.2.2 => 3.2.5
* update skywalking-toolkit 8.14.0 => 8.16.0
* update logstash 7.2 => 7.4

### 功能更新

* update 优化 与 vue 版本同步代码结构
* update 优化 放行springboot默认error接口
* update 优化 RepeatSubmitAspect 逻辑避免并发请求问题
* update 调整 gateway 访问日志输出等级
* update 优化 修改角色如果未绑定用户则无需清理
* update 优化 用户昵称非空校验
* update 优化 在全局异常拦截器中增加两类异常处理
* update 优化 StreamUtils 方法过滤null值
* update 优化 powerjob 端口随着主应用端口飘逸 避免集群冲突
* update 优化 角色权限支持仅本人权限查看 解决无法查看自己创建的角色问题
* update 修改代码生成模版，日期范围统一采用addDateRange方法
* update 优化 树表生成前端缺少 children 字段
* update 优化 ruoyi-resource 服务添加 websocket 模块
* update 优化 放行验证码接口、第三方登录请求与回调
* update 更新 GlobalLogFilter#filter 根据请求头判断加密参数(感谢 Michelle.Chung !pr100)
* update 优化 SaReactorFilter 过滤器判断 token 客户端 id 是否有效(感谢 Michelle.Chung !pr101)
* update 删除一些跟swagger有关的字眼 避免误解
* update 优化 兼容 clientid 通过 param 传输
* update 优化 excel导出字典转下拉框 无需标记index自动处理(感谢 一夏coco)
* update 优化 增加线程池销毁配置
* update 优化 屏蔽 powerjob 无用的心跳日志
* update 优化 适配 mysql 8.0.34 升级连接机制
* update 优化 加密实现 使用 EncryptUtils 统一处理
* update 优化 删除字典无用状态字段(基本用不上 禁用后还会导致回显问题)
* update 优化 部门与角色如果绑定了用户则不允许禁用
* update 优化 岗位如果绑定了用户则不允许禁用
* update 优化 用户管理 只查询未禁用的部门角色岗位数据
* update 优化 登录用户增加昵称返回
* update 优化 全局异常处理器 业务异常不输出具体堆栈信息 减少无用日志存储
* update 优化 将部门管理 负责人选项改为下拉框选择
* update 优化 登录用户缓存 去除冗余统一存储
* update 优化 注册用户异常报错不正确问题
* update 优化 放宽菜单权限 角色关联菜单无需管理员

### 新增功能

* add 增加 RedisUtils 批量删除 hash key 方法
* add 新增 Oss 上传 File 文件方法(感谢 jenn)
* add 增加 excel 导出下拉框功能
* add 新增 RedisUtils.setObjectIfAbsent 如果不存在则设置方法

### 修复问题

* fix 修复 用户重名登录报错问题
* fix 修复 服务未添加 common-security 模块导致异常拦截器不生效问题
* fix 修复 用户篡改管理员角色标识符越权问题
* fix 修复 文件管理 创建人未翻译问题
* fix 修复 monitor 监控无法展示数据问题
* fix 修复 更换 satoken dubbo 插件导致包名不一致问题
* fix 修复 字典缓存注解使用错误问题
* fix 修复 接口文档未拼接服务路径问题
* fix 修复 excel 枚举反向解析失败问题
* fix 修复 查询部门下拉树未过滤数据权限问题
* fix 修复 CacheName 缓存key存储错误问题
* fix 修复 oss 列表 用户名回显错误
* fix 修复 不同vo相同字段mybatis会自动赋值问题
* fix 修复 删除 skywalking dubbo 2.X 插件避免与 3.X 出现兼容性问题
* fix 修复 新增角色使用内置管理员标识符问题
* fix 修复 token 过期登出无法清理在线用户问题
* fix 修复 动态设置 token 有效期不生效问题
* fix 修复 加密模块数据转换异常问题
* fix 修复 dubbo 更改内部序列化方式 导致异常类无法反序列化问题
* fix 修复 客户端编辑时授权类型变更未保存的问题
* fix 修正 缺失 SysClientVoConvert 导致转换异常(感谢 Michelle.Chung)
* fix 修正 auth 模块缺失引用导致解密异常(感谢 Michelle.Chung)
* fix 修复 demo 与 stream-mq 模块缺少 security 依赖问题
* fix 修复 导入用户数据 变量使用错误问题
* fix 修复 验证码开关未动态刷新问题
* fix 修复 自动填充数据 loginUser 为 null(感谢 charles !pr108)
* fix 修复 修复树模板父级编码变量错误
* fix 修复 部署部分系统出现乱码问题
* fix 修复 一级菜单无法显示问题
* fix 修复 新建用户可能会存在的越权行为
* fix 修复 代码生成页面参数缺少逗号问题

### 移除功能

* remove 移除原有短信功能(建议使用sms4j)
* remove 移除xxljob功能(建议使用powerjob)


## v1.8.0 - 2023-07-11

### 重大更新

* [重大更新] 新增 sms4j 短信融合框架整合(支持数十种短信厂商接入、发送限制、负载均衡等功能)
* [不兼容更新] 移除 原短信功能(建议使用新 sms4j 功能)
* [重要迁移] 迁移 vue3 前端到主仓库统一维护

### 依赖升级

* update springboot 2.7.11 => 2.7.13
* update spring-cloud 2021.0.7 => 2021.0.8
* update satoken 1.34.0 => 1.35.0.RC
* update easyexcel 3.2.1 => 3.3.1
* update sms4j 2.2.0
* update element 2.15.12 => 2.15.13

### 功能更新

* update 优化 StreamUtils 方法过滤null值
* update 优化 页签在Firefox浏览器被遮挡
* update 优化 在全局异常拦截器中增加两类异常处理
* update 优化 下载zip方法增加遮罩层(感谢@梁剑锋)
* update 优化 用户昵称非空校验
* update 优化 修改角色如果未绑定用户则无需清理
* update 优化 RepeatSubmitAspect 逻辑避免并发请求问题
* update 优化 satoken 过期配置 支持多端token自定义有效期
* update 优化 加密注解注释错误
* update 优化 切换 maven 仓库到华为云(aliyun 不可用)
* update 优化 excel 导出存在合并项时在初始化类时进行数据的处理避免多次调用(感谢@yueye)
* update 优化 重构 CellMergeStrategy 支持多级表头修复一些小问题 整理代码结构
* update 补全 SysLogininforMapper.xml 缺失字段
* update 优化 demo 模块 路径适配统一前端
* update 调整 gateway 访问日志输出等级

### 新增功能

* add 新增 RedisUtils.setObjectIfAbsent 不存在则设置方法
* add 新增 Excel 导出附带有下拉框(字典自动导出为下拉框) 可自定义多级下拉框(感谢@Emil.Zhang)
* add 新增 OssClient File 文件上传方法
* add 增加 RedisUtils 批量删除 hash key 方法

### 问题修复

* fix 修复 sa-token.check-same-token 开关对网关鉴权无效问题
* fix 修复 服务未添加 common-security 模块导致异常拦截器不生效问题
* fix 修复 删除 skywalking dubbo 2.X 插件避免与 3.X 出现兼容性问题
* fix 修复 excel 枚举反向解析失败问题
* fix 修复 字典缓存注解使用错误问题
* fix 修复 新增角色使用内置管理员标识符问题
* fix 修复 缓存监控图表 支持跟随屏幕大小自适应调整(感谢@抓蛙师)
* fix 修复 防重组件 错删注解问题
* fix 修复 CacheName 缓存key存储错误问题
* fix 修复 字典缓存注解使用错误问题
* fix 修复 用户篡改管理员角色标识符越权问题
* fix 修复 登录校验错误次数未达到上限时 错误次数缓存未设置有效时间问题
* fix 修复 OssClient 切换服务 实例不正确问题
* fix 修复 element ui 因版本而未被工具识别问题(感谢@梁剑锋)
* fix 修复 admin监控 切换tab页需要重复登录问题
* fix 修复 个人中心tab栏关闭页面内容压缩问题

## v2.0.0 - 2023-06-15

**重点说明: 由于 SpringCloudAlibaba 一直未发布正式版 导致系统底层组件可能存在些许问题 故而不建议生产使用 框架也将直接开启后续 2.1.0 的开发工作**

### 重大更新

* [不兼容升级] java 版本从 jdk 8 升级到 jdk 17 且需要使用 graalvm 运行(暂时未解决原生jdk存在的问题)
* [不兼容升级] springboot 升级 3.0 版本
* [不兼容升级] 重构 项目模块结构 采用插件化结构 易扩展易解耦
* [不兼容升级] com.sun.mail 更改为 jakarta.mail 修改最新写法
* [不兼容升级] javax.servlet 替换为 jakarta.servlet 更新所有代码
* [简化性升级] 默认开启复杂结构 resultMap 自动映射 简化xml编码(多结构实体需带上主键id) 
* [数据库改动] 更新 create_by update_by 字段类型 (保存用户id)
* [数据库改动] 新增 create_dept 字段 (保存创建部门id)
* [不兼容更新] system 模块 所有实体类均使用 bo|vo 规范化
* [重大更新] 新增 多租户功能设计 整体框架代码结构与数据库更改
* [重大更新] 新增 mapstruct-plus 替换 BeanUtil 与 BeanCopyUtils 工具
* [不兼容更新] 重构 登录注解接口与cloud版本统一接口路径
* [不兼容更新] 重构 BaseMapperPlus接口 去除 `@param <M> Mapper` 泛型
* [不兼容更新] 移除 vue2 前端工程 全面启用 vue3
* [重大更新] 新增 vue3 + TS 版本前端(独立仓库后续与Cloud版本共用)
* [重大更新] 增加 websocket 模块 支持token鉴权 支持分布式集群消息同步
* [重大更新] 框架文档全面翻新 https://plus-doc.dromara.org
* [不兼容更新] 代码生成 支持代码生成多数据源统一存储(主库存储子库的表 无需子库加gen表了)
* [不兼容更新] 重构 将系统内置配置放置到common包内独立加载 不允许用户随意修改

### 依赖升级

* update java 1.8 => 17
* update springboot 2.7.7 => 3.0.7
* update springcloud 2021.0.6 => 2022.0.2
* update springcloud-alibaba 2022.0.0.0-RC2
* update springboot-admin 2.7.10 => 3.0.4
* update springdoc 1.6.14 => 2.1.0
* udpate dubbo 3.1.8 => 3.2.2
* update lock4j 2.2.3 => 2.2.4
* update dynamic-ds 3.5.2 => 3.6.1
* update easyexcel 3.1.5 => 3.2.1
* update hutool 5.8.11 => 5.8.18
* update redisson 3.19.2 => 3.20.1
* update lombok 1.18.24 => 1.18.26
* update spring-boot.mybatis 2.2.2 => 3.0.1
* update mapstruct-plus 1.2.3
* update maven-compiler-plugin 3.10.1 => 3.11.0
* update maven-surefire-plugin 3.0.0-M7 => 3.0.0
* update docker mysql 8.0.31 => 8.0.33
* update docker nginx 1.22.1 => 1.32.4
* update docker redis 6.2.7 => 6.2.12
* update docker minio RELEASE.2023-04-13T03-08-07Z

### 功能更新

* update 适配 AsyncConfig 替换过期继承类改为实现 AsyncConfigurer 接口
* update 适配 redis 新版本配置文件写法
* update 适配 获取redis 监控参数接口 替换过期语法
* update 适配 sa-token 替换新依赖 sa-token-spring-boot3-starter
* update 适配 springboot-admin 改为最新 spring-security 写法
* update 适配 springdoc 新版本配置方式
* update 适配 ServletUtils 更换继承 JakartaServletUtil
* update 适配 新序列化注解
* update 优化 利用 resultMap 自动映射配置 简化 xml (非嵌套)
* update 优化 调整 system entity 实体与 controller 包结构
* update 优化 实体类中校验注解的提示信息
* update 优化 使用 jdk17 语法优化代码
* update 优化 所有 properties 文件改为注解启用
* update 更新 docker 基础镜像 graalvm java17
* update 优化 用户头像 改为存储 ossId 使用转换模块转为 url 展示
* update 优化 重构 CellMergeStrategy 支持多级表头修复一些小问题 整理代码结构
* update 优化 登录流程代码注释
* update 优化 将框架内的swagger命名更改为springdoc命名避免误解

### 新增功能

* add 新增 flatten-maven-plugin 插件统一版本号管理
* add 新增 ip2region 实现离线IP地址定位库

### 移除功能

* remove 移除 BeanCopyUtils 工具类 与 JDK17 不兼容
* remove 移除 devtools 依赖 并不好用(建议直接用idea自带的热更)
* remove 移除 vue2 前端工程 统一使用 vue3 工程

### 修复功能

* fix 修复 根据 seata 官方提交记录 临时修复 seata 关于jdk17代理的bug
* fix 修复 登录校验错误次数未达到上限时 错误次数缓存未设置有效时间问题
* fix 修复 common-core 包使用aop注解 但未添加aop实现类导致单独使用报错问题

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