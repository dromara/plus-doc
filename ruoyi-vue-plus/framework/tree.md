## 目录结构
v5.0.0
~~~
RuoYi-Vue-Plus
├─ ruoyi-admin                         // 管理模块 [8080,9101]
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
│      └─ ip2region.xdb                // IP区域地址库
├─ ruoyi-extend                        // 扩展模块
│  └─ ruoyi-monitor-admin              // admin监控模块 [9090]
│  └─ ruoyi-xxl-job-admin              // 任务调度中心模块 [9100]
├─ ruoyi-common                        // 通用模块
│  └─ ruoyi-common-bom                 // common依赖包管理
│  └─ ruoyi-common-core                // 核心模块
│  └─ ruoyi-common-doc                 // 系统接口模块
│  └─ ruoyi-common-encrypt             // 数据加解密模块
│  └─ ruoyi-common-excel               // excel模块
│  └─ ruoyi-common-idempotent          // 幂等功能模块
│  └─ ruoyi-common-job                 // 定时任务模块
│  └─ ruoyi-common-json                // 序列化模块
│  └─ ruoyi-common-log                 // 日志模块
│  └─ ruoyi-common-mail                // 邮件模块
│  └─ ruoyi-common-mybatis             // 数据库模块
│  └─ ruoyi-common-oss                 // oss服务模块
│  └─ ruoyi-common-ratelimiter         // 限流功能模块
│  └─ ruoyi-common-redis               // 缓存服务模块
│  └─ ruoyi-common-satoken             // satoken模块
│  └─ ruoyi-common-security            // 安全模块
│  └─ ruoyi-common-sensitive           // 脱敏模块
│  └─ ruoyi-common-sms                 // 短信模块
│  └─ ruoyi-common-tenant              // 租户模块
│  └─ ruoyi-common-translation         // 通用翻译模块
│  └─ ruoyi-common-web                 // web模块
├─ ruoyi-modules                       // 模块组
│  └─ ruoyi-demo                       // 演示模块
│    └─ controller                     // 演示controller
│      └─ queue                        // 队列演示案例
│        └─ BoundedQueueController     // 有界队列 演示案例
│        └─ DelayedQueueController     // 延迟队列 演示案例
│        └─ PriorityDemo               // 优先队列 实体类
│        └─ PriorityQueueController    // 优先队列 演示案例
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
│  └─ ruoyi-generator                  // 代码生成模块
│    └─ util                           // 工具类
│      └─ GenUtils                     // 代码生成器 工具类
│      └─ VelocityInitializer          // 模板初始化工厂
│      └─ VelocityUtils                // 模板处理工具类
│    └─ resources                      // 资源文件
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
│          └─ index.vue.vm             // crud 页面模板
│          └─ index-tree.vue.vm        // 树表 页面模板
│      └─ vm/sql
│          └─ oracle/sql.vm            // oracle页面菜单 sql 模板
│          └─ postgres/sql.vm          // postgres页面菜单 sql 模板
│          └─ sqlserver/sql.vm         // sqlserver页面菜单 sql 模板
│          └─ sql.vm                   // 页面菜单 sql 模板
│      └─ generator.yml                // 生成器默认配置文件
│  └─ ruoyi-job                        // 任务调度服务
│  └─ ruoyi-system                     // 业务模块
│    └─ domain                         // 系统数据对象
│    └─ mapper                         // 系统mapper
│    └─ service                        // 系统业务接口
│      └─ impl                         // 系统业务接口实现类
│    └─ resources
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