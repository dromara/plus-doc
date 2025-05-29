# 更新日志
- - -

## v5.4.0 - 2025-05-29

### 新增成员项目

* 基于soybean前端 ruoyi-plus-soybean https://gitee.com/xlsea/ruoyi-plus-soybean
* 删除多租户与工作流后端 RuoYi-Vue-Plus-Single https://gitee.com/ColorDreams/RuoYi-Vue-Plus-Single

### 依赖升级

* update springboot 3.4.4 => 3.4.6
* update mybatis-plus 3.5.11 => 3.5.12
* update springboot-admin 3.4.5 => 3.4.7
* update warm-flow 1.6.8 => 1.7.2(感谢 May)
* update EasyExcel 升级原作者 FastExcel 1.2.0(感谢 这夏天依然平凡)
* update snailjob 1.4.0 => 1.5.0(感谢 AprilWind)
* update springdoc 2.8.5 => 2.8.8
* update bouncycastle 1.76 => 1.80
* update mapstruct-plus 1.4.6 => 1.4.8
* update docker mysql建议版本升级到8.0.42
* update docker redis建议版本升级到7.2.8
* update docker minio建议版本升级到RELEASE.2025-05-24T17-08-30Z
* update satoken 1.40.0 => 1.42.0 适配所有升级项(改动较多)
> satoken改动如下:<br>
> SaLoginModel -> SaLoginParameter<br>
> device -> deviceType satoken<br>
> BCrypt -> hutool BCrypt(satoken不维护了)<br>
> SaTokenDao -> SaTokenDaoBySessionFollowObject(satoken做了重构封装)<br>
> sse 适配新satoken版本拦截器变化

### 功能更新

* update 优化 删除退回任务bo关于驳回的节点的非空校验(感谢 晓华)
* update 优化 权限获取 增加用户登录了但是查询的loginId是别人的场景
* update 优化 调整流程监听(感谢 May)
* update 优化 代码生成ServiceImpl层增加日志注解(感谢 AprilWind)
* update 优化 新增发号器工具类方法(感谢 AprilWind)
* update 优化 nginx代理snail-job websocket参数 解决部署到服务器后 查看日志会显示ws连接失败(感谢 qxy)
* update 优化 动态路由迁移到菜单管理
* update 优化 统一请假日期字段格式处理(感谢 AprilWind)
* update 优化 工作流创建事件 将状态交给业务方处理
* update 优化 JustAuth的钉钉和微信第三方登录使用最新实现类(感谢 AprilWind)
* update 优化 工作流自定义条件注解注释(感谢 AprilWind)
* update 优化 工作流模块下一个节点指定办理人、角色和部门转具体用户、抄送人和消息推送，改到通过全局分派监听器和完成监听器处理
* update 优化 假分页方法(感谢 AprilWind)
* update 优化 重构办理人接口(感谢 AprilWind)
* update 优化 调整获取申请人节点接口(感谢 May)
* update 优化 调整流程撤销 删除无用代码(感谢 May)
* update 优化 EncryptUtils加解密注释(感谢 AprilWind)
* update 优化 docker-compose编排增加snailjob端口防止集群冲突
* update 优化 多租户忽略表判断支持忽略大小写
* update 优化 直接从ClassPath加载ip2region数据库文件(感谢 秋辞未寒)
* update 优化 查询系统菜单列表新增菜单类型与父级ID查询条件(感谢 马铃薯头)
* update 优化 放开申请人附件与抄送限制 附件改为按钮权限控制(感谢 May)
* update 优化 获取地址支持IPv6判断而不是抛异常(感谢 秋辞未寒)
* update 优化 日期与字符串工具类(感谢 AprilWind)
* update 优化 枚举类型注释(感谢 AprilWind)
* update 优化 返回任务指派的列表增加时间查询条件(感谢 AprilWind)
* update 优化 getNextNodeList 只获取中间节点用于审批 过滤其他无用节点
* update 优化 缓存注解支持关闭本地缓存
* update 优化 实体类统一使用包装类型
* update 优化 Mybatis异常处理器(感谢 AprilWind)
* update 优化 工作流用户查询构建(感谢 May)
* update 优化 工作流权限按钮获取，若需要扩展更多按钮权限，只需在 sources 中新增对应的枚举类或字典类型(感谢 AprilWind)
* update 优化 统一流程demo 权限人分隔符
* update 优化 工作流获取流程变量(感谢 AprilWind)
* update 优化 统一工作流FlowParams构造方式为建造者模式 提升代码可读性(感谢 AprilWind)
* update 优化 调整监听器事件参数代码
* update 优化 工作流流程监听增加节点信息(感谢 AprilWind)
* update 优化 工作流办理人权限处理器(感谢 AprilWind)
* update 优化 Dockerfile 构建文件新增暴露 snail job 客户端端口 用于定时任务调度中心通信(感谢 Binary)
* update 优化 使用 record 简化vo代码
* update 优化 FlwNodeExtServiceImpl 代码实现
* update 优化 sse 删除之后 手动触发完成 防止内存泄漏
* update 优化 支持excel方法抛出json异常

### 功能新增

* add 新增 工作流api审批简化方法
* add 新增 批量级联删除菜单接口(感谢 马铃薯头)
* add 新增 自定义字典值校验器(感谢 AprilWind)
* add 新增 对接 gitea 三方单点登录(感谢 lcry)
* add 新增 自定义 Date 类型反序列化处理器（支持多种格式）(感谢 AprilWind)
* add 新增 请求体读取异常处理(感谢 AprilWind)
* add 新增 一大堆snailjob的demo案例(感谢 老马)

### 问题修复

* fix 修复 解决通过loginId查询角色和菜单权限 而非当前用户时 报错问题
* fix 修复 退回申请人无法发送消息问题(感谢 songgaoshuai)
* fix 修复 查询办理人错误使用(感谢 AprilWind)
* fix 修复 snailjob http basic验证判断错误
* fix 修复 excel 合并单元格在导出在最后一行无法合并时 之前的数据合并失效问题(感谢 马铃薯头)
* fix 修复 临时解决sa-token使用秒 redis是毫秒导致1秒的精度问题 手动补偿(等satoken官方修复)
* fix 修复 选择弹窗会签人员后 会签审批出现每个任务的审批人都是选择的多人(感谢 May)
* fix 修复 在线用户设置过期时间与客户端不同步问题
* fix 修复 excel模板导出多个字段下拉值超过100个异常 采用多个sheet的方案解决(感谢 velenooo)

### 前端改动

* update element-plus 2.9.8
* update pinia 3.0.2
* update vue-router 4.5.0
* update vue-types 6.0.0
* update vxe-table 4.13.7
* update sass 1.87.0
* update typescript 5.8.3
* update vite 6.3.2
* add 新增 工作流流程预览 使用logicflow前端渲染(感谢 May)
* add 新增 批量级联删除菜单接口(感谢 马铃薯头)
* update 优化 添加页签图标显示开关功能
* update 优化 表格增加border(感谢 May)
* update 优化 动态路由迁移到菜单管理
* update 优化 审批按钮 封装成公共组件(感谢 May)
* update 优化 执行eslint:fix优化代码
* update 优化 修改navbar中消息图标样式与同行元素保持一致(感谢 愿丶)
* update 更新 readme 增加新成员项目
* update 优化 工作流分类与流程设计新增联动(感谢 MoMyles)
* update 优化 增加oss站点与域名 默认前缀避免填错
* update 优化 登出之后清理tabs
* update 优化 角色禁用不允许分配
* update 优化 删除无用组件
* fix 修复 请假时间 时间组件没法和rule规则联动问题(ele的bug手动设置必填)
* fix 修复 请假提交未取消按钮loading问题
* fix 修复 前端download方法响应json异常问题

## v5.3.1 - 2025-03-27

### 依赖升级

* update springboot 3.4.1 => 3.4.4
* update springdoc 2.8.3 => 2.8.5
* update satoken 1.39.0 => 1.40.0
* update redisson 3.43.0 => 3.45.1
* update springboot-admin 3.4.1 => 3.4.5 修复重新登录404问题
* update warm-flow 1.6.6 => 1.6.8
* update mybatis-plus 3.5.10 => 3.5.11
* update snailjob 1.3.0 => 1.4.0
* update springboot-admin 3.4.2 => 3.4.5
* update sms4j 3.3.3 => 3.3.4

### 功能更新

* update 优化 nginx开启静态资源压缩 增加静态文件传输效率
* update 优化 根部门祖级列表常量和备注，以避免歧义(感谢 秋辞未寒)
* update 优化 部门下岗位名称重复(感谢 AprilWind)
* update 优化 ProcessTaskEvent 改名为 ProcessCreateTaskEvent 避免错误理解
* update 优化 租户表企业名与部门表长度保持一致 防止长度不一致报错
* update 优化 删除无用配置类
* update 优化 工作流设计器获取任务执行人查询正常状态
* update 优化 流程设计器-节点扩展属性注释(感谢 AprilWind)
* update 优化 根据字典类型查询信息增加一级缓存(感谢 AprilWind)
* update 优化 校验框架配置类加载顺序，确保优先于默认的验证配置(感谢 AprilWind)
* update 优化 sys_oss 表增加扩展字段 ext1
* update 优化 调整获取下一节点，增加用户分页查询参数
* update 优化 text 设置默认值某些版本可能有问题 改为默认null
* update 优化 重构将 WorkflowUtils 工具类改为 FlwCommonService 更通用的业务处理
* update 优化 getLoginUser 方法 支持返回多种类型登陆实体
* update 优化 权限标识符支持通配符 '*'
* update 优化 将s3 crt客户端替换为Netty客户端 节约17M打包大小
* update 优化 函数注释以准确描述SSE会话(感谢 洛小风)
* update 优化 获取节点扩展属性 简化节点编码(感谢 AprilWind)
* update 优化 工作流办理人标识符解析(感谢 AprilWind)
* update 优化 修改oss枚举包名与其他模块统一
* update 优化 打包默认跳过测试 减少心智难度
* update 优化 简化 SysTaskAssigneeServiceImpl 代码实现
* update 优化 excel导出 下拉框支持顺序
* update 优化 兼容老版本数据权限用户写法
* update 优化 统一用户密码校验长度

### 功能新增

* add 增加 工作流按钮权限相关配置与代码(感谢 May)
* add 增加 获取节点数据接口(感谢 May)
* add 增加 工作流案例流程支持动态设置下一节点审批人(感谢 May)

### 问题修复

* fix 修复 sse关闭 用户id或token为空报错问题
* fix 修复 splitTo 转换后的list包含null问题
* fix 修复 结束监听器 flowParam 可能为null问题
* fix 修复 Caffeine缓存未清空导致的部门创建显示延迟问题(感谢 QianRj)
* fix 修复 oracle 表别名不能写as关键字
* fix 修复 oracle 新建租户工作流部分报错问题
* fix 修复 oracle 同步字典报错问题
* fix 修复 获取下一环节排他网关出现条件错误(感谢 May)
* fix 修复 关闭验证码后 限流注解仍然生效问题
* fix 修复 pg数据库 强类型转换报错(感谢 guo83551218)
* fix 修复 跨域未设置请求头问题(cloud版本不需要 vue版本需要)
* fix 修复 excel模板导出数据被覆盖的问题

### 前端改动

* update vueuse 11.3 => 12.7
* update 优化 调整客户端管理 label长度
* update 优化 删除已经没有实际作用的依赖
* update 优化 更改版权信息2025
* update 优化 升级部分依赖，优化eslint语法以及scss语法
* update 优化 文件上传增加禁用按钮 增加文件类型
* update 优化 优化前端树结构拼接性能
* update 优化 前端处理路由函数代码
* update 优化 顶部菜单搜索栏为多层级显示
* update 优化 标注node与npm版本
* update 优化 上传组件添加accept属性(感谢 can)
* update 优化 vite-plugin-svg-icons插件为vite-plugin-svg-icons-ng 以修复依赖警告、安全漏洞警告(感谢 yangxu52)
* update 优化 增加自动导入函数
* update 优化 调整选人警告
* update 优化 标准化tsconfig postcss配置，并修改错误的$schema(感谢 yangxu52)
* update 优化 代码 统一store用法
* update 优化 统一流程定义编码，增加流程分类标识(感谢 AprilWind)
* update 优化 树组件如果不存在属性 则做兼容
* update 优化 登录与注册页面表头从配置文件内导入
* update 优化 findPathNum 方法 更高效
* update 优化 删除无用组件
* add 增加 弹窗选人(感谢 May)
* add 增加 设置下一审批人(感谢 May)
* add 增加 示例 调整提交组件(感谢 May)
* fix 修复 消息弹框内容过长不换行(感谢 zst_2001)
* fix 修复 路由守卫白名单通配符正则覆盖问题(感谢 QianRj)
* fix 修复【表单路径】prop错误(感谢 JiaoYue)
* fix 修复 代码生成 下拉框选项没法清空问题
* fix 修复 el-dropdown-item 标签无法使用 v-has-permi自定义标签 问题
* fix 修复 图片组件变量错误
* fix 修复 漏洞扫描出现yui2.9.0版本无关紧要的漏洞 (感谢 dxldxl)

## v5.3.0 - 2025-01-24

### 重大更新

* 重构数据权限实现逻辑 支持任意mapper方法标注注解 无需再找真实mapper标注
* 重写工作流模块 接入warm-flow工作流 移除flowable工作流(过于复杂 用不明白的人太多)

### 依赖升级

* update springboot 3.2.11 => 3.4.1
* update springboot-admin 3.2.3 => 3.4.1
* update mybatis-plus 3.5.8 => 3.5.9
* update snailjob 1.1.2 => 1.3.0(感谢 dhb52)
* update springdoc 2.6.0 => 2.8.3
* update redisson 3.37.0 => 3.43.0
* update justauth 1.16.6 => 1.16.7 支持多种登录方式 不限于三方登录
* update mybatis-plus 3.5.9 => 3.5.10
* update hutool 5.8.31 => 5.8.35
* update mapstruct-plus 1.4.5 => 1.4.6
* update lombok 1.18.34 => 1.18.36
* update anyline 20241022 => 20250101

### 功能更新

* update 优化 查询oss图片url接口改为query标识符
* update 优化 绑定三方与解绑三方校验token是否存在
* update 优化 OSS私有桶的临时URL获取方法(感谢 秋辞未寒)
* update 优化 ws模块替换session的时候关闭session连接
* update 优化 数据权限 判断当前注解不满足模板则跳过
* update 优化 使用request存储动态租户 避免单请求多次查询redis获取
* update 优化 修改部门信息增加事务(感谢 AprilWind)
* update 优化 增加菜单选择拓展参数(感谢 玲娜贝er)
* update 优化 jdk21环境开启虚拟线程时的定时任务池(感谢 秋辞未寒)
* update 优化 sse 如果获取token列表为空 删除userid对应的存储
* update 优化 数据权限处理器 增加默认值处理 针对于表达式变量与注解不对应或者表达式变量为null的情况
* update 优化 关闭sse后 使用工具报错
* update 优化 增加mybatis-plus一键开启/关闭逻辑删除功能
* update 优化 修改日志时间展示颜色(感谢 疯狂的牛子Li)
* update 适配 TOPIAM 2.0 单点登录(感谢 马铃薯头)
* update 优化 完善微信小程序登录接口逻辑
* update 优化 重构DateUtils工具类 更加实用
* update 优化 为部门角色岗位用户增加一些常用查询方法
* update 优化 登录用户增加岗位数据
* update 优化 去除部门查询状态校验 改为前端过滤 便于查看禁用部门下的其他数据
* update 优化 部门树增加禁用标志位
* update 优化 workflow 模块增加接口文档生成功能
* update 优化 代码生成 增加buildQueryWrapper默认排序规则
* update 优化 代码生成 创建更新时间被覆盖问题
* update 优化 代码生成排序问题(感谢 AprilWind)
* update 优化 在线用户查询 优先查询租户下数据 减少数据量
* update 优化 租户域名使用忽略大小写匹配
* update 优化 代码生成器 将数据库字段默认转为小写 避免某些数据库大写出现的问题
* update 优化 由于sse重试机制导致经常输出认证失败日志过多 将sse失败改为debug
* update 优化 有界队列销毁方式 应该使用特殊销毁方法
* update 优化 redis序列化 支持更快的apache二进制跨语言序列化方案
* update 优化 租户日志模块名
* update 优化 增加默认数据权限 "部门及以下或本人数据权限" 选项
* update 优化 代码生成器 pg数据库 主键获取不精确问题
* update 优化 代码生成器类型获取
* update 优化 个人中心强退设备接口路径
* update 优化 Dockerfile 消除warn警告
* update 优化 补充客户端工具类注释(感谢 AprilWind)
* update 优化 补充Undertow自定义配置信息注释(感谢 AprilWind)
* update 优化 拦截爬虫跟踪等垃圾请求
* update 优化 将Log记录异常长度改为5000
* update 优化 将Log记录参数长度扩充为5000更符合实际需求
* update 优化 xss包装器 Parameter 处理 兼容某些容器不允许改参数的情况
* update 优化 支持脱敏传多角色多权限标识
* update 优化 角色删除清理缓存
* update 优化 使用ObjectUtils新增方法封装代码
* update 优化 数据权限查询增加缓存
* update 优化 代码生成器数字类别判断
* update 优化 逻辑删除状态改为1 避免误解
* update 重构 将UserConstants改为SystemConstants 统一常量使用 降低使用难度避免误解
* update 优化 封装部门基于父id查询方法
* update 优化 不传用户id不校验数据权限
* update 优化 部门树多基点展示问题 支持相同名称节点并排展示
* update 优化 去除OSS桶检测 桶不存在自然会报错无需额外检测
* update 优化 限流注解增加固定清理时间
* update 优化 sys_social表 租户id增加默认值
* update 优化 jackson 过期方法
* update 优化 多租户插件初始化流程
* update 优化 去除GenUtils设置createby逻辑 统一走自动注入设置
* update 优化 替换RedisUtils中的废弃方法getKeysStreamByPattern及trySetRate(感谢 Lucien_Lu)
* update 优化 删除桶自动创建代码逻辑(云厂商限制不允许操作桶)
* update 优化 角色清理在线用户代码逻辑

### 功能新增

* add 新增 导出模板必填、备注注解实现(感谢 liyang)
* add 新增 基于Redisson的发号器工具(感谢 秋辞未寒)
* add 新增 validation支持枚举校验(感谢 秋辞未寒)
* add 新增 validation支持枚举校验(感谢 秋辞未寒)
* add 新增 对象工具类(感谢 秋辞未寒)
* add 增加 邮件多附件demo

### 问题修复

* fix 修复 文件下载 设置content-length无效问题
* fix 修复 satoken dao层获取timeout为秒导致丢失毫秒进度问题(临时修复 等satoken官方解决)
* fix 修复 postgresql的表元数据没有创建时间这个东西(好奇葩) 只能new Date代替
* fix 修复 数据权限 多角色多注解包含忽略权限标识符逻辑不正确问题
* fix 修复 未开启sse 找不到bean问题
* fix 修复 数据权限导致的个人中心的修改头像和修改密码接口错误(感谢 QianRj)
* fix 修复 部门数据权限缓存错误(感谢 QianRj)
* fix 修复 三方授权工具部分网站授权缺失参数问题
* fix 修复 代码生成 表名中间带有特殊字符被过滤问题 改为开头过滤
* fix 修复 字段长度超出数据库限制问题
* fix 修复 过滤器正则错误
* fix 修复 monitor 设置 context-path 导致退出重新登录404问题
* fix 修复 数据权限多角色与权限标识符共用导致的问题 https://gitee.com/dromara/RuoYi-Vue-Plus/issues/IB4CS4
* fix 修复 排除websocket包内包含的tomcat依赖(导致一些问题)
* fix 修复 PageQuery 转json报错问题
* fix 修复 sse 关闭接口无法断连问题
* fix 修复 PlusSmsDao#clean 方法书写错误
* fix 修复 excel级联下拉框数据错误(感谢 Emil.Zhang)
* fix 修复 某些模块不存在 mp 依赖导致方法报错问题
* fix 修复 新版本mp默认使用最新 sqlserver 语法导致代码生成分页报错问题
* fix 修复 OssClient 回滚错误修改
* fix 修复 注册日志记录状态错误

### 前端改动

* update typescript 5.4.5 => 5.7.2
* update vite 5.2.12 => 5.4.11
* update vue 3.4.34 => 3.5.13
* update element-plus 2.7.8 => 2.8.8
* update eslint 升级v9版本(感谢 玲娜贝er)
* update vue-i18n 10.0.5
* update 优化 parseTime 提示报错问题
* update 优化 国际化 变量提示
* update 优化 重写工作流相关页面
* update 优化 主题色在深色模式下显示亮度(感谢 LiuHao)
* update 优化 hasRoles 方法增加超管判断
* update 优化 用户页面 增加导入到处权限标识
* update 优化 TopNav内链菜单点击没有高亮
* update 优化 新增编辑用户 过滤禁用的部门
* update 优化 白名单增加正则匹配示例
* update 优化 白名单支持对通配符路径匹配
* update 优化 i18n $t方法支持ts类型提示(感谢 玲娜贝er)
* update 优化 登录页多语言按钮样式
* update 优化 补充登录页与注册页的国际化内容并添加切换语言按钮(感谢 QianRj)
* update 优化 eslint升级v9版本 & 更新一些不符合校验规则的代码(感谢 玲娜贝er)
* update 优化 全代码规范化处理
* update 优化 代码生成导入下拉框默认值处理
* update 优化 菜单面包屑导航支持多层级显示
* update 优化 参数键值更换为多行文本
* update 优化 增加默认数据权限 "部门及以下或本人数据权限" 选项
* update 优化 permission loadView避免整个modules循环 允许view中间有views文件夹(感谢 admin_lijinfu)
* update 优化 个人中心强退设备接口路径
* update 优化 直接从@/lang/*.ts后缀的i18n文件中读取各国语言包信息(感谢 QianRj)
* update 优化 将同步字典功能迁移到租户管理内
* update 优化 重构操作日志详情样式(感谢 玲娜贝er)
* update 优化 字典缓存使用Map代替Array更高效(感谢 月夜)
* update 优化 校检文件名是否包含特殊字符
* update 优化 getTenantList 接口动态决定是否传token
* fix 修复 切换租户 tabs过多导致卡住问题
* fix 修复 用户管理界面修改按钮权限字符串错误(感谢 QianRj)
* fix 修复 oss配置页 展示配置key 隐藏主键id
* fix 修复 页面api过期警告
* fix 修复 代码生成列表加载问题你
* fix 修复 修复默认关闭Tags-Views时，内链页面打不开
* fix 修复 用户选择组件 id类型不统一问题
* fix 修复 代码生成 编辑之后查两遍列表的问题
* fix 修复 登录无redirect参数404问题
* fix 修复 monitor 设置 context-path 导致退出重新登录404问题
* fix 修复 手动登出与token过期登出跳转行为不一致问题
* fix 修复 关闭sse功能 登出还是会发送sse关闭请求导致报错问题
* fix 修复 内嵌页面数据缓存导致与外部页面不一致问题

## v5.2.3 - 2024-10-25

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


## v5.2.2 - 2024-08-26

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


## v5.2.1 - 2024-07-09

### 功能更新

* update 优化 更改prod环境 snailjob状态 默认启用
* update 优化 替换过期方法
* update 优化 租户列表接口 避免登录之后列表被域名过滤
* update 优化 获取用户账户方法 LoginHelper#getUsername(感谢 AprilWind)
* update 优化 用户ID查询角色列表代码实现(感谢 AprilWind)
* update 优化 大数据量下join卡顿问题 使用子查询提高性能
* update 优化 修改路由name命名规则 防止重复路由覆盖问题(感谢 玲娜贝er)
* update 优化 修改 snailjob 默认端口 避免与系统内置端口冲突问题
* update 优化 isTenantAdmin 空校验
* update 优化 webscoket 配置与异常拦截
* update 优化 更新 redis 密码策略(密码必填 升级需注意)
* update 优化 更新使用 Spring 官方推荐 JDK
* update 优化 StreamUtils 抽取 findFirst findAny 方法
* update 优化 工作流相关代码方法

### 问题修复

* fix 修复 postgres flowable sql 缺失字段问题
* fix 修复 新版上传未设置acl问题
* fix 修复 get路径特殊规则 导致 actuator 泄漏问题 [issue#4f9ceb0a](https://gitee.com/dromara/RuoYi-Vue-Plus/commit/4f9ceb0a8057284a0d9d69da58df630d8bc2e84f)
* fix 修复 pg数据库 用户查询报错问题
* fix 修复 isLogin 方法抛异常无法正常返回值问题

### 前端改动

* update 优化 工作流选人改为懒加载窗口
* update 优化 路由name重复检查
* update 优化 eslint 语法
* update 优化 动态创建组件实例时, 设置路由name为组件名 解决缓存问题
* fix 修复 由于没有await 导致执行顺序不可控
* fix 修复 富文本编辑器 添加之后内容未清理问题

## v5.2.0 - 2024-06-20

### 重大改动

* 集成 flowable 增加工作流相关功能(感谢 May)
* 集成 snailjob 移除 powerjob(投诉的人太多使用成本太高)(感谢 dhb52)
* 升级 aws s3 升级到 2.X 性能大幅提升
* 优化 数据权限 数据加密 使用预扫描mapper注解提升代码性能(感谢 老马)
* 新增 caffeine 减少将近90%的redis查询提高性能

### 依赖升级

* update springboot 3.1.7 => 3.2.6 支持虚拟线程
* update springboot-admin 3.1.8 => 3.2.3
* update mybatis-plus 3.5.4 => 3.5.7 适配更改代码
* update springdoc 2.2.0 => 2.5.0
* update easyexcel 3.3.3 => 3.3.4
* update redisson 3.24.3 => 3.31.0
* update lombok 1.18.30 => 1.18.32
* update sms4j 2.2.0 => 3.2.1 支持自定义配置key 可用于多厂商多租户等
* update satoken 1.37.0 -> 1.38.0
* update hutool 5.8.22 => 5.8.26
* update mapstruct-plus 1.3.5 => 1.3.6
* update lock4j 2.2.5 => 2.2.7
* update dynamic-ds 4.2.0 => 4.3.1

### 功能更新

* update 优化 三方登录不同域名问题 采用新方案
* update 优化 获取aop代理的方式 减少与其他使用aop的功能冲突的概率
* update 优化 token无效时关闭ws连接(感谢 AprilWind)
* update 优化 移除表单构建菜单(没有可用组件 用处不大以后再考虑)
* update 优化 切换动态租户 默认线程内切换(如需全局 手动传参)
* update 优化 代码生成注释，删除无用引入(感谢 AprilWind)
* update 优化 代码生成 el-radio 标签过期属性
* update 优化 异常处理器自动配置
* update 优化 文件下载使用对流下载降低内存使用(感谢 PhoenixL)
* update 优化 去除gc日志参数(有需要自己加)
* update 优化 拆分异常处理器
* update 优化 常规web异常状态码
* update 优化 设置静态资源路径防止所有请求都可以访问静态资源
* update 优化 redis 对Long值的存储类型不同问题
* update 优化 去除加密请求类型限制
* update 优化 mp多租户插件注入逻辑
* update 优化 RedisUtils 支持忽略租户
* update 优化 更新ip地址xdb文件
* update 优化 验证码背景色改为浅灰色
* update 优化 mybatis依赖设置为可选依赖 避免出现不应该注入的情况
* update 优化 GET 方法响应体支持加密
* update 优化 excel插件合并策略 去除被合并单元格的非首行内容(感谢 司猫子)
* update 优化 下拉选接口数据权限
* update 优化 OssFactory 获取实例锁性能
* update 优化 使用翻译注解简化用户查询 调整用户查询逻辑
* update 优化 框架整体提高查询性能
* update 优化 将p6spy配置文件统一放置到 common-mybatis 插件包内

### 新增功能

* add 新增 分布式锁Lock4j异常拦截器
* add 新增 个人中心-在线设备管理
* add 新增 岗位编码与部门编码并将岗位调整到部门下(感谢 AprilWind)
* add 新增 BaseMapperPlus提供可选是否抛异常selectVoOne方法(感谢 秋辞未寒)
* add 新增 用户、部门、角色、岗位 下拉选接口与代码实现优化
* add 增加 StringUtils.isVirtual 方法
* add 增加 JustAuth 整合 TopIam 单点登录

### 问题修复

* fix 修复 websocket clientid 参数不走mvc拦截器 无法生效问题
* fix 修复 oss未使用租户 拼接租户id null问题
* fix 修复 用户昵称修改后未清除对应缓存问题(感谢 zhuweitung)
* fix 修复 图片预览问题(感谢 AprilWind)
* fix 修复 三方账号可以绑定多平台账号问题
* fix 修复 主建错别字(感谢 good)
* fix 修复 兼容redis5.0出现的问题
* fix 修复 部分浏览器无法获取加密响应头问题
* fix 修复 用户未设置部门 登录报错问题
* fix 修复 excel 表达式字典 下拉框导出格式错误
* fix 修复 提升锁的作用域 并采用双重校验锁(感谢 fanc)
* fix 修复 用户登录查询部门缓存无法获取租户id问题
* fix 修复 关闭租户功能 三方登录报错问题


### 前端改动

* update element-plus 2.7.5
* update vite 5.2.10
* update vue 3.4.25
* update vue-router 4.3.2
* update nodejs 升级到最低 18.18.0
* update 优化 跟密码相关的默认前端关闭防重功能
* update 优化 点击左边菜单时页面空白或者刷新整个页面的问题
* update 优化 el-select 与 el-input 全局样式
* update 优化 首页打开topNav不展开菜单问题
* update 优化 支持全局开启或关闭接口加密功能
* update 优化 密码校验策略增加非法字符限制
* update 优化 图片上传组件增加压缩功能支持 可自行开关(感谢 fengheguai)
* update 优化 request请求类判断请求头方式
* update 优化 更改客户端状态接口 使用clientId传参
* update 优化 ws开关改为常开(vite5修复了崩溃bug)
* fix 修复 移动端下 无法展开菜单问题
* fix 修复 面板因为min width原因收缩不全
* fix 修复 文件预览大写后缀不展示的问题(感谢 北桥)
* fix 修复 i18n无感刷新问题
* fix 修复 websocket 非index页面刷新无法重连问题

## v5.1.2 - 2023-12-22

### 依赖升级

* update springboot 3.1.5 => 3.1.7
* update mybatis-boot 3.0.2 => 3.0.3 优化依赖传递
* update powerjob 4.3.3 => 4.3.6
* update easyexcel 3.3.2 => 3.3.3
* update transmittable-thread-local 2.14.2 => 2.14.4
* update justauth 1.16.5 => 1.16.6
* update redisson 3.24.1 => 3.24.3 修复订阅重启连接超时问题

### 功能更新

* update 优化 为 admin 模块 单独增加 ratelimiter 模块
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
* update 优化 租户插件 ignoreTable 方法支持动态租户

### 新增功能

* add 新增 RedisUtils.setObjectIfExists 如果存在则设置方法
* add 新增 丰富RedisUtils对List Set类型的操作
* add 新增 翻译组件 用户昵称翻译实现
* add 新增 响应加密功能 支持注解强制加密接口数据 (感谢 MichelleChung)

### 问题修复

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

## v4.8.2 - 2023-11-27

### 依赖升级

* update springboot 2.7.17 => 2.7.18 升级到2.X最终版本(官方停更)
* update mybatis-plus 3.5.3.2 => 3.5.4
* update springboot 2.7.14 => 2.7.17
* update satoken 1.36.0 => 1.37.0
* update aws-java-sdk-s3 1.12.400 => 1.12.540
* update vue-quill 1.1.0 => 1.2.0

### 功能更新

* update 优化 页面关于权限标识符说明
* update 优化 数据权限拦截器优先判断方法是否有效 提高性能减少无用sql解析
* update 优化 部门数据权限使用默认兜底方案
* update 优化 更改默认日志等级为info 避免日志过多(按需开启debug)
* update 优化 补全代码生成 columnList 接口参数注解缺失
* update 优化 操作日志 部门信息完善 vue3页面
* update 优化 AddressUtils 兼容linux系统本地ip
* update 优化 操作日志 部门信息完善 (感谢 柏竹)
* update 优化 数据权限 减少二次校验查询
* update 优化 vue3 版本用户初始密码从字典查询
* update 优化 富文本Editor组件检验图片格式
* update 优化 操作日志列表新增IP地址查询
* update 优化 全局数据存储用户编号
* update 优化 菜单管理类型为按钮状态可选

### 问题修复

* fix 修复 OssFactory 并发多创建实例问题
* fix 修复 demo的form字段有误 (感谢 dhb52)
* fix 修复 延迟队列在投递消息未到达时间的时候 服务死机导致重启收不到消息
* fix 修复 数据权限优化后 update delete 报null问题
* fix 修复 五级路由缓存无效问题
* fix 修复 oss服务无法连接 导致业务异常问题 查询不应该影响业务
* fix 修复 内链iframe没有传递参数问题
* fix 修复 外链带端口出现的异常
* fix 修复 普通角色编辑使用内置管理员code越权问题
* fix 修复 代码生成 是否必填与数据库不匹配问题
* fix 修复 HeaderSearch组件跳转query参数丢失问题
* fix 修复 树结构代码生成新增方法赋值错误 (感谢 这夏天依然平凡)

## v5.1.1 - 2023-11-14

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

### 功能更新

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

### 问题修复

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

## v4.8.1 - 2023-09-25

### 依赖升级

* update springboot 2.7.15 => 2.7.16
* update springboot-admin 2.7.10 => 2.7.11
* update satoken 1.35.0.RC => 1.36.0
* update lombok 1.18.26 =. 1.18.30
* update mybatis-plus 3.5.3.1 => 3.5.3.2
* update easyexcel 3.3.1 => 3.3.2
* update hutool 5.8.18 => 5.8.20

### 功能更新

* update 优化 重置密码注释参数中文解释错误
* update 优化 getTokenActivityTimeout => getTokenActiveTimeout
* update 优化字典标签支持传分隔符分隔的字符串和数组，优化渲染效果
* update 优化 控制台debuger位置错误问题
* update 优化 TopNav 菜单样式
* update 优化 全局异常处理器 业务异常不输出具体堆栈信息 减少无用日志存储
* update 优化 用户管理 只查询未禁用的部门角色岗位数据
* update 优化 岗位如果绑定了用户则不允许禁用
* update 优化 部门与角色如果绑定了用户则不允许禁用
* update 优化 加密实现 使用 EncryptUtils 统一处理
* update 优化 excel导出字典转下拉框 无需标记index自动处理
* update 优化 excel 导出字典默认转为下拉框
* update  优化 删除一些跟 swagger 有关的字眼 避免误解
* update 优化 角色权限支持仅本人权限查看 解决无法查看自己创建的角色问题
* update 优化 RedisCacheController 注释错误
* update 优化 xxljob 端口随着主应用端口飘逸 避免集群冲突
* update 优化 powerjob 端口随着主应用端口飘逸 避免集群冲突

### 问题修复

* fix 修复 代码生成后 vo 定义 'serialVersionUID' 字段的不可序列化类
* fix 修复 自定义字典样式不生效的问题
* fix 修复 布局配置失效问题
* fix 修复 新建用户可能会存在的越权行为
* fix 修复 字典缓存删除方法参数错误问题
* fix 修复 修复树模板父级编码变量错误
* fix 修复 有界队列与优先队列 错误使用问题
* fix 修复 升级 mp 版本导致的问题
* fix 修复 vue3 版本注册页验证码不显示问题
* fix 修复 加密模块数据转换异常问题
* fix 修复 动态设置 token 有效期不生效问题
* fix 修复 token 过期登出无法清理在线用户问题


## v5.1.0 - 2023-09-05

# 开发历程

* 2023年5月 开始 5.1.0 计划 历经1个月的设计与讨论
* 2023年6月 开始着手开发 历经2个多月的开发 特别感谢团队的小伙伴与一些热心的粉丝 参与功能开发与测试
* 2023年8月 开始公测 历经将近1个月的公测与修复工作(期间成功支持多位使用者生产使用)
* 2023年9月初 正式发布(经过多个小伙伴的生产实践 已基本可尝试生产使用)
> 关于4.X的说明 由于SpringBoot2.X与vue2.X均在11月底停止维护<br>
> 故而咱们vue版本4.X也无法再继续更新<br>
> 介于4.X的用户量特别庞大 功能也非常的稳定<br>
> 计划于11月底同Boot2.X一同停止更新但还会持续维护修复bug(修复的形式为直接提交到4.X分支停止发版)<br>

# 视频介绍

为了更好的让大家了解 5.1.0 作者录制了相关的视频 供大家快速了解上手

* 5.1.0 新功能与变更介绍: https://www.bilibili.com/video/BV1fj411y71X/
* 搭建与运行: https://www.bilibili.com/video/BV1Fg4y137JK/
* 生产环境搭建部署: https://www.bilibili.com/video/BV1mL411e7ha/

# 更新日志

### 重大更新

* [重大更新] 优化 相关代码 完成代码生成多数据源统一存储(感谢 WangBQ !pr349)
* [不兼容更新] 移除 原短信功能 集成更强大的 sms4j 短信工具包(感谢 友杰 !pr367)
* [不兼容更新] 对接 powerjob 实现分布式任务调度 删除原有 xxljob 原因为社区不更新功能太少只支持mysql(感谢 yhan219 !pr359)
* [重大更新] 新增 三方授权绑定登录功能 基于 justauth 支持市面上大部分三方登录(感谢 三个三 !pr370)
* [不兼容更新] 新增 客户端授权功能 不需要更改任何代码即可完成多端动态对接(感谢 Michelle.Chung !pr379)
* [重大更新] 新增 前后端接口请求加密传输 基于AES+RSA动态高强度加密(感谢 wdhcr !pr377)
* [重大更新] 新增 三方授权登录 对接 maxkey 单点登录
* [不兼容更新] 优化 redis序列化配置 更改为通用格式(升级需清除redis所有数据)

### 依赖升级

* update springboot 3.0.7 => 3.1.3
* update springboot-admin 3.1.3 => 3.1.5
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

### 功能更新

* update 优化 excel 导出合并 在初始化类时进行数据的处理
* update 优化 简化 flatten 插件语法写法
* update 优化 支持本地虚拟域名调试(感谢 代星登 !pr363)
* update 重构 将框架内的 swagger 命名更改为 springdoc 命名避免误解
* update 重构 将系统内置配置放置到 common 包内独立加载 不允许用户随意修改
* update 优化 切换 maven 仓库到 华为云(aliyun依赖不更新拉取不到)
* update 优化 升级 satoken 支持多端 token 自定义有效期功能
* update 优化 RepeatSubmitAspect 逻辑避免并发请求问题
* update 优化 在全局异常拦截器中增加两类异常处理
* update 优化 提供powerjob完整sql脚本 降低用户使用难度
* update 优化 StreamUtils 其他方法过滤null值(感谢 bleachtred !pr390)
* update 优化 powerjob 端口随着主应用端口飘逸 避免集群冲突
* update 优化 角色权限支持仅本人权限查看 解决无法查看自己创建的角色问题
* update 修改代码生成模版，日期范围统一采用addDateRange方法(感谢 LiuHao !pr397)
* update 优化 树表生成前端缺少 children 字段
* update 优化 CryptoFilter null判断工具
* update 优化 websocket 路径与 cloud 版本保持一致
* update 优化 更新登录策略返回值(感谢 zlyx)
* update 修改代码生成模板，调整列表打开对话框和接口请求顺序
* update 优化 SaInterceptor 拦截器判断 token 客户端id是否有效(感谢 zlyx !pr402)
* update 优化 excel 导出字典默认转为下拉框
* update 优化 兼容 clientid 通过 param 传输
* update 优化 excel导出字典转下拉框 无需标记index自动处理(感谢 一夏coco)
* update 优化 简化线程池配置
* update 优化 屏蔽 powerjob 无用的心跳日志
* update 优化 适配 mysql 8.0.34 升级连接机制
* update 优化 加密实现 使用 EncryptUtils 统一处理
* update 优化 删除字典无用状态字段(基本用不上 禁用后还会导致回显问题)
* update 优化 部门与角色如果绑定了用户则不允许禁用
* update 优化 岗位如果绑定了用户则不允许禁用
* update 优化 用户管理 只查询未禁用的部门角色岗位数据
* update 优化 登录用户增加昵称返回
* update 优化 将部门管理 负责人选项改为下拉框选择(感谢 Lionel !pr410)
* update 优化 全局异常处理器 业务异常不输出具体堆栈信息 减少无用日志存储
* update 优化 登录用户缓存 去除冗余统一存储
* update 优化 放宽菜单权限 角色关联菜单无需管理员

### 新增功能

* add 增加 RedisUtils 批量删除 hash key 方法
* add 新增 Oss 上传 File 文件方法(感谢 jenn !pr362)
* add 增加 excel 导出下拉框功能
* add 新增 RedisUtils.setObjectIfAbsent 如果不存在则设置方法

### 修复问题

* fix 修复 脱敏注解标记位置错误
* fix 修复 OssClient 实例多租户相同key缓存覆盖问题
* fix 修复 关闭多租户 脱敏判断问题
* fix 修复 OssClient 切换服务 实例不正确问题(感谢 jenn !pr360)
* fix 修复 传参类型不正确导致 postgreSql 同步套餐报错问题
* fix 修复 参数类型修改 未修改校验注解
* fix 修复 登录校验错误次数未达到上限时 错误次数缓存未设置有效时间问题(感谢 konbai !pr366)
* fix 修复 common-core 包使用aop注解 但未添加aop实现类导致单独使用报错问题
* fix 修复 Mapper 多参数未加 @Param 注解问题
* fix 修复 邮箱登录 查询值错误问题
* fix 修复 用户篡改管理员角色标识符越权问题
* fix 修复 字典缓存注解使用错误问题
* fix 修复 查询部门下拉树未过滤数据权限问题
* fix 修复 CacheName 缓存key存储错误问题
* fix 修复 代码生成 前端添加或修改表单修改列生成问题
* fix 修复 新增角色使用内置管理员标识符问题
* fix 修复 代码生成 前端添加或修改表单修改列生成问题
* fix 修复 token 过期登出无法清理在线用户问题
* fix 修复 加密模块数据转换异常问题
* fix 修复 可能导致异常类无法反序列化问题
* fix 修复 代码生成 编辑按钮刷新列表问题
* fix 修复 客户端编辑时授权类型变更未保存的问题(感谢 David Wei !pr400)
* fix 修复 有界队列与优先队列 错误使用问题
* fix 修复 修复树模板父级编码变量错误
* fix 修复 部署部分系统出现乱码问题
* fix 修复 一级菜单无法显示问题
* fix 修复 可能会存在的越权行为(感谢 丶Stone !pr416)
* fix 修复 代码生成页面参数缺少逗号问题

### 移除功能

* remove 移除原有短信功能(建议使用sms4j)
* remove 移除xxljob功能(建议使用powerjob)


## v4.8.0 - 2023-07-10

### 重大更新

* [重大更新] 新增 sms4j 短信融合框架整合(支持数十种短信厂商接入、发送限制、负载均衡等功能)
* [不兼容更新] 移除 原短信功能(建议使用新 sms4j 功能)
* [重要迁移] 迁移 vue3 前端到主仓库统一维护

### 依赖升级

* update springboot 2.7.11 => 2.7.13
* update satoken 1.34.0 => 1.35.0.RC
* update easyexcel 3.2.1 => 3.3.1
* update sms4j 2.2.0

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

### 新增功能

* add 新增 RedisUtils.setObjectIfAbsent 不存在则设置方法
* add 新增 Excel 导出附带有下拉框(字典自动导出为下拉框) 可自定义多级下拉框(感谢@Emil.Zhang)
* add 新增 OssClient File 文件上传方法
* add 增加 RedisUtils 批量删除 hash key 方法

### 问题修复

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

## v5.0.0 - 2023-05-19

# 开发历程

* 2022年11月 开始5.X计划 历经2个月的设计与讨论
* 2023年1月 开始着手开发 历经3个月的开发 特别感谢团队的小伙伴与一些热心的粉丝 参与功能开发与测试
* 2023年4月 开始公测 历经将近2个月的公测与修复工作(期间成功支持多位使用者生产使用)
* 2023年5月底 正式发布 虽然已经有生产实践 但是springboot3.0与jdk17使用者还处于少数 另外5.X后续还有一些不兼容更新 求稳者建议在等一等
* 关于4.X的说明 由于springboot2.X 与 vue2.X 匀在年底停止维护 故此4.X也将于年底同boot2一同停止维护

# 视频介绍

为了更好的让大家了解 5.X 作者录制了相关的视频 供大家快速了解上手

* 搭建与运行: https://www.bilibili.com/video/BV1Fg4y137JK/
* 新功能与变更介绍: https://www.bilibili.com/video/BV1Us4y1m7ky/
* 生产环境搭建部署: https://www.bilibili.com/video/BV1mL411e7ha/

# 更新日志

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

### 依赖升级

* update java 1.8 => 17
* update springboot 2.7.7 => 3.0.7
* update springboot-admin 2.7.10 => 3.0.4
* update springdoc 1.6.14 => 2.1.0
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

### 新增功能

* add 新增 flatten-maven-plugin 插件统一版本号管理
* add 新增 ip2region 实现离线IP地址定位库

### 移除功能

* remove 移除 BeanCopyUtils 工具类 与 JDK17 不兼容
* remove 移除 devtools 依赖 并不好用(建议直接用idea自带的热更)
* remove 移除 vue2 前端工程 统一使用 vue3 工程

## v4.7.0 - 2023-05-08
## v4.6.0 - 2023-03-13
## v4.5.0 - 2023-01-12
## v4.4.0 - 2022-11-28
## v4.3.1 - 2022-10-24
## v4.3.0 - 2022-09-14
## v4.2.0 - 2022-06-28
## v4.1.0 - 2022-04-24
## v4.0.1 - 2022-03-01
## v4.0.0 - 2022-02-18
## v3.5.0 - 2021-12-28
## v3.4.0 - 2021-11-29
## v3.3.0 - 2021-10-29
## v3.2.0 - 2021-9-28
## v3.1.0 - 2021-9-7
## v3.0.0 - 2021-8-18
## v2.6.0 - 2021-7-28
## v2.5.2 - 2021-7-19
## v2.5.1 - 2021-7-13
## v2.5.0 - 2021-7-12
## v2.4.0 - 2021-6-24
## v2.3.2 - 2021-6-11
## v2.3.1 - 2021-6-4
## v2.3.0 - 2021-6-1
## v2.2.1 - 2021-5-29
## v2.2.0 - 2021-5-25
## v2.1.2 - 2021-5-21
## v2.1.1 - 2021-5-19
## v2.1.0 - 2021-5-17
## v2.0.0 - 2021-5-15
## v1.5.0 - 2021-4-16
## v1.4.0 - 2021-2-24
## v1.3.0 - 2020-12-12
## v1.2.0 - 2020-10-22
## v1.1.0 - 2020-9-12
## v1.0.2 - 2020-7-13
## v1.0.1 - 2020-3-19
## v1.0.0 - 2020-2-14
* 基于 ruoyi-vue 3.4.0 发布 v1.0.0 稳定版