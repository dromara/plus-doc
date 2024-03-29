# 更新日志
- - -

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

### 依赖升级

* update springboot 2.7.9 => 2.7.11 修复 DoS 漏洞 修复CVE漏洞
* update springcloud 2021.0.6 => 2021.0.7
* update springcloud-alibaba 2021.0.4.0 => 2021.0.5.0
* update dubbo 3.1.7 => 3.1.10
* update nacos 2.2.0 => 2.2.1
* update xxljob 2.3.1 => 2.4.0
* update minio 升级至最新版 避免低版本信息泄漏问题
* update hutool 5.8.15 => 5.8.18
* update redisson 3.20.0 => 3.20.1
* update lombok 1.18.24 => 1.18.26

### 功能更新

* update 优化 更改 sys_oss_config 表注释 避免误解
* update 优化 sys_logininfor 丰富多种信息
* update 项目正式入驻 dromara 开源社区 更改项目地址
* update 全新 logo 全新背景图(设计师打造)
* update 优化 代码生成模块的数据同步功能
* update 修改多团队开发插件，支持多网卡
* update 修改controller中校验直接返回R.fail
* update 优化 角色sort值一样的排序问题
* update 更换默认用户头像
* update 优化 WebFluxUtils.getOriginalRequestUrl 方法获取空路径报错问题
* update 去除same-token有限期配置，使用默认配置（一天）
* update 优化固定头部页签滚动条被隐藏的问题
* update delete vue-multiselect style
* update 按代码规范补全重写注解
* update 优化 极端情况获取LoginUser可能为null问题
* update 优化 更改系统所有服务日志配置文件命名为 logback-plus.xml 避免与其他框架默认配置冲突
* update 优化 skywalking-agent 探针日志等级调整为 WARN 减少无用日志输出
* update 优化 加解密模块 将null判断下推防止任何可能的null出现
* update 优化 在线用户token获取方式
* update 优化 用户更改角色 踢掉角色相关所有在线用户

### 新功能

* add 集成 ip2region 实现离线IP地址定位库
* add 增加 邮箱验证码发送接口
* add 增加 邮箱登陆接口
* add 增加 EncryptUtils 加解密安全工具类 可以处理base64,aes,sm4,sm2,rsa,md5,sha256加解密
* add 增加 EncryptUtils 类中增加国密sm3的不可逆加密算法
* add 新增 忽略数据权限写法 防止异常不执行关闭问题

### 问题修复

* fix 修复 MybatisExceptionHandler 未自动装载问题
* fix 修复 代码生成 点选按钮不生效问题
* fix 修复 Nacos 服务 SpringBoot-admin 客户端功能失效问题
* fix 修复 findInSet 在mysql下方法搜索非数字字段时 无引号报错问题
* fix 修复 ruoyi-demo postgres 数据库用户名密码变量错误
* fix 修复 oracle postgres 数据库日志表索引创建错误
* fix 修复 无法注入 mailProperties 导致 resource 模块无法启动问题
* fix 修复tab栏”关闭其他“异常的问题
* fix 修复 加解密拦截器 对象属性为null问题
* fix 修复 取消oss预览状态修改 图标变化不正常问题
* fix 修复 nacos 新版本升级后 与 docker 基础镜像系统存在兼容性问题


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
