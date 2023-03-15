## 目录结构
v4.3.0
~~~
RuoYi-Vue-Plus
├─ ruoyi-admin          // 管理模块 [8080,9101]
│  └─ RuoYiApplication                 // 启动类
│  └─ RuoYiServletInitializer          // 容器部署初始化类
│  └─ resources                        // 资源文件
│      └─ i18n/messages.properties     // 国际化配置文件
│      └─ application.yml              // 框架总配置文件
│      └─ application-dev.yml          // 开发环境配置文件
│      └─ application-prod.yml         // 生产环境配置文件
│      └─ banner.txt                   // 框架启动图标
│      └─ logback.xml                  // 日志配置文件
│      └─ spy.properties               // p6spy配置文件
├─ ruoyi-common         // 通用模块
│  └─ annotation                       // 通用注解
│      └─ Anonymous                    // 匿名访问不鉴权注解
│      └─ CellMerge                    // excel列合并
│      └─ DataColumn                   // 数据权限字段绑定
│      └─ DataPermission               // 数据权限组
│      └─ ExcelDictFormat              // 字典格式化
│      └─ Log                          // 自定义操作日志记录注解
│      └─ RateLimiter                  // 自定义限流注解
│      └─ RepeatSubmit                 // 自定义注解防止表单重复提交
│      └─ Sensitive                    // 数据脱敏注解
│  └─ captcha                          // 验证码相关
│  └─ config                           // 通用配置
│  └─ constant                         // 通用常量
│  └─ convert                          // 转换器
│  └─ core                             // 通用核心代码
│      └─ controller                   // web层通用数据处理
│      └─ domain                       // 通用实体
│      └─ page                         // 分页实体
│      └─ mapper                       // 通用mapper
│      └─ validate                     // 通用校验类
│      └─ service                      // 通用接口
│  └─ enums                            // 枚举包    
│  └─ exception                        // 异常包
│  └─ excel                            // 异常包
│  └─ filter                           // 过滤器包
│  └─ helper
│      └─ DataBaseHelper               // 数据库助手
│      └─ DataPermissionHelper         // 数据权限助手
│      └─ LoginHelper                  // 登录鉴权助手
│  └─ jackson                          // json序列化工具
│  └─ xss                              // xss过滤拦截
│  └─ utils                            // 工具类包
│      └─ email/MailUtils              // 邮件工具
│      └─ file/FileUtils               // 文件处理工具类
│      └─ ip/AddressUtils              // 获取地址类
│      └─ poi/ExcelUtil                // Excel相关处理
│      └─ redis/CacheUtils             // 缓存操作工具类
│      └─ redis/QueueUtils             // 分布式队列工具
│      └─ redis/RedisUtils             // redis 工具类
│      └─ reflect/ReflectUtils         // 反射工具类
│      └─ spring/SpringUtils           // spring工具类
│      └─ sql/SqlUtil                  // sql操作工具类
│      └─ BeanCopyUtils                // bean深拷贝工具
│      └─ DateUtils                    // 时间工具类
│      └─ JsonUtils                    // JSON 工具类
│      └─ MessageUtils                 // 获取i18n资源文件
│      └─ ServletUtils                 // 客户端工具类
│      └─ StreamUtils                  // stream 流工具类
│      └─ StringUtils                  // 自定义字符串工具
│      └─ Threads                      // 线程相关工具类
│      └─ TreeBuildUtils               // 封装系统树构建
│      └─ ValidatorUtils               // 校验框架工具
├─ ruoyi-demo           // 演示模块
│  └─ controller        // 演示controller
│      └─ queue         // 队列演示案例
│          └─ BoundedQueueController   // 有界队列 演示案例
│          └─ DelayedQueueController   // 延迟队列 演示案例
│          └─ PriorityDemo             // 优先队列 实体类
│          └─ PriorityQueueController  // 优先队列 演示案例
│      └─ MailController               // 邮件发送案例
│      └─ RedisCacheController         // spring-cache 演示案例
│      └─ RedisLockController          // Redis锁演示类
│      └─ RedisPubSubController        // Redis 发布订阅 演示案例
│      └─ RedisRateLimiterController   // Redis 测试分布式限流样例
│      └─ SmsController                // 短信演示案例
│      └─ Swagger3DemoController       // swagger3 用法示例
│      └─ TestExcelController          // 测试Excel功能
│      └─ TestBatchController          // 测试批量方法
│      └─ TestI18nController           // 测试国际化
│      └─ TestSensitiveController      // 测试数据脱敏控制器
│      └─ TestDemoController           // 测试crud数据权限类
│      └─ TestTreeController           // 测试树表数据权限类
├─ ruoyi-extend         // 扩展模块
│  └─ ruoyi-monitor-admin              // admin监控模块 [9090]
│  └─ ruoyi-xxl-job-admin              // 任务调度中心模块 [9100]
├─ ruoyi-framework      // 核心配置模块
│  └─ aspectj                          // aop相关处理
│  └─ config                           // 系统配置相关
│      └─ properties                   // 配置映射包
│      └─ ApplicationConfig            // 框架配置
│      └─ AsyncConfig                  // 异步配置
│      └─ CaptchaConfig                // 验证码配置
│      └─ DruidConfig                  // druid 配置多数据源
│      └─ FilterConfig                 // filter 配置
│      └─ I18nConfig                   // 国际化配置
│      └─ JacksonConfig                // jackson 序列化配置
│      └─ MailConfig                   // JavaMail 配置
│      └─ MybatisPlusConfig            // mybatis-plus 配置
│      └─ RedisConfig                  // redis 配置
│      └─ ResourcesConfig              // 通用资源配置
│      └─ SaTokenConfig                // sa-token 配置
│      └─ SwaggerConfig                // Swagger 文档配置
│      └─ ThreadPoolConfig             // 线程池配置
│      └─ TLogConfig                   // TLog 分布式日志配置
│      └─ UndertowConfig               // Undertow 自定义配置
│      └─ ValidatorConfig              // 校验框架配置
│  └─ jackson                          // jackson相关
│  └─ manager                          // 管理器相关
│  └─ handler                          // 处理器相关
│  └─ Interceptor                      // 拦截器相关
│  └─ satoken                          // 权限鉴权相关
│  └─ web                              // 全局异常处理器
├─ ruoyi-generator      // 代码生成模块
│  └─ util                             // 工具类
│      └─ GenUtils                     // 代码生成器 工具类
│      └─ VelocityInitializer          // 模板初始化工厂
│      └─ VelocityUtils                // 模板处理工具类
│  └─ resources                        // 资源文件
│      └─ vm/java
│          └─ bo.java.vm               // 业务bo对象模板
│          └─ domain.java.vm           // 数据实体对象模板
│          └─ vo.java.vm               // 视图vo对象模板
│          └─ controller.java.vm       // 控制器模板
│          └─ service.java.vm          // 业务接口模板
│          └─ serviceImpl.java.vm      // 业务实现模板
│          └─ mapper.java.vm           // mapper接口模板
│      └─ vm/xml
│          └─ mapper.xml.vm            // mapper XML 模板
│      └─ vm/js/api.js.vm              // 页面 js api 模板
│      └─ vm/vue
│          └─ v3                       // vue3版本页面生成模板
│              └─ index.vue.vm         // crud 页面模板
│              └─ index-tree.vue.vm    // 树表 页面模板
│          └─ index.vue.vm             // crud 页面模板
│          └─ index-tree.vue.vm        // 树表 页面模板
│      └─ vm/sql
│          └─ oracle/sql.vm            // oracle页面菜单 sql 模板
│          └─ postgres/sql.vm          // postgres页面菜单 sql 模板
│          └─ sqlserver/sql.vm         // sqlserver页面菜单 sql 模板
│          └─ sql.vm                   // 页面菜单 sql 模板
│      └─ generator.yml                // 生成器默认配置文件
├─ ruoyi-oss            // OSS对象存储模块
├─ ruoyi-sms            // 短信模块
├─ ruoyi-job            // 任务调度服务
├─ ruoyi-system         // 业务模块
│  └─ domain                           // 系统数据对象
│  └─ mapper                           // 系统mapper
│  └─ service                          // 系统业务接口
│      └─ impl                         // 系统业务接口实现类
│  └─ resources
│      └─ mapper/system                // 系统业务XML
├─ ruoyi-ui             // 前端框架 [80]
│  └─ build                            // 打包配置
│  └─ public                           // 公共文件
│  └─ package.json                     // 公共依赖
│  └─ vue.config.js                    // vue配置
│  └─ src                              // 源代码
├─ script                // 系统脚本包
│  └─ bin                              // 运行脚本包
│  └─ docker                           // docker相关脚本
│  └─ sql                              // sql脚本
├─ .editorconfig        // 编辑器编码格式配置
├─ LICENSE              // 开源协议
├─ pom.xml              // 公共依赖
├─ README.md            // 框架说明文件
~~~