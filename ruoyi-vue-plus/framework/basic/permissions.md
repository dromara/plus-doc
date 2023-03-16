# 关于数据权限
- - -
* 参考 demo 模块用法(需导入 test.sql 文件)

### 版本 >= 3.5.0 使用教程(由于 3.4.0 功能局限性太大 且有一定安全性问题 故重写实现)

### 新版数据权限功能:
1.支持自动注入 sql 数据过滤<br>
2.查询、更新、删除 限制<br>
3.支持自定义数据字段过滤<br>
4.模板支持 spel 语法实现动态 Bean 处理

### 数据权限相关代码

| 类                             | 说明              | 功能                                     |
|-------------------------------|-----------------|----------------------------------------|
| DataScopeType                 | 数据权限模板定义        | 用于定义数据权限模板                             |
| DataPermission                | 数据权限组注解         | 用于标注开启数据权限 (默认过滤部门权限)                  |
| DataColumn                    | 具体的数据权限字段标注     | 用于替换数据权限模板内的 key 变量                    |
| PlusDataPermissionInterceptor | 数据权限 sql 拦截器    | 用于拦截所有 sql 检查是否标注了 `DataPermission` 注解 |
| PlusDataPermissionHandler     | 数据权限处理器         | 用于处理被拦截到的 sql 为其添加数据权限过滤条件             |
| DataPermissionHelper          | 数据权限助手          | 操作数据权限上下文变量                            |
| SysDataScopeService           | 自定义 Bean 处理数据权限 | 用于自定义扩展                                |

### 使用方式 `参考demo模块`
数据权限体系 `用户 -> 多角色 => 角色 -> 单数据权限`
> 例子: 用户A 拥有两个角色
> 角色A 部门经理 可查看 本部门及以下部门的数据
> 角色B 兼职开发 可查看 仅自己的数据

### 创建角色 test1 为 本部门及以下
![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/221625_23e08a74_1766278.png "屏幕截图.png")

### 创建角色 test2 为 仅本人
![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/221649_f214b9ae_1766278.png "屏幕截图.png")

### 将其分配给用户 test
![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/221734_bd41cd78_1766278.png "屏幕截图.png")

### 编写列表查询(注意: 数据权限注解只能在 Mapper 层使用)
> 标注数据权限注解 `dept_id` 为过滤部门字段 `user_id` 为过滤创建用户

![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/220940_0178abed_1766278.png "屏幕截图.png")

**重点注意: 如下情况不生效**
有自定义实现方法 最终执行的mapper不是这个方法 所以无法生效
![输入图片说明](https://images.gitee.com/uploads/images/2022/0614/194854_60a79fc6_1766278.png "屏幕截图.png")

### 编写数据权限模板
![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/222207_9dbc87a7_1766278.png "屏幕截图.png")
1.`code` 为关联角色的数据权限 `code`<br>
2.`sqlTemplate` 为 sql 模板<br>
#{#deptName} 为模板变量 对应权限注解的 `key`<br>
#{@sdss} 为模板 Bean 调用 调用其 Bean 的处理方法<br>
3.`elseSql` 为兜底 sql 处理当前角色与标注的注解 无对应的情况<br>
例如 数据权限为仅本人 且 方法并未标注具体过滤注解 则 填充 `1 = 0` 使条件不满足 不允许查看<br>
更详细用法可以参考 `DataScopeType` 注释

### 测试代码

> 使用 `管理员` 用户优先测试

![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/223620_347b02ca_1766278.png "屏幕截图.png")

> 使用 `test` 用户测试

![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/225710_cc5562d1_1766278.png "屏幕截图.png")

> 使用 `test` 删除一条不属于自己的数据

![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/232419_ac0f1c74_1766278.png "屏幕截图.png")

![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/232506_e2e50e8b_1766278.png "屏幕截图.png")

sql执行为不满足条件 不允许删除

> 使用 `test` 修改与删除同理<br>
具体实现为 更新和删除方法 标注数据权限注解

![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/232652_263838f4_1766278.png "屏幕截图.png")

### 自定义SQL模板

> 1.首先在角色管理 数据权限下拉框 添加自定义模板<br>
> 为什么不放置到系统字典问题: 因数据权限与模板绑定 不应随意改动 最好事先定义好

![输入图片说明](https://images.gitee.com/uploads/images/2021/1217/222827_eede5737_1766278.png "屏幕截图.png")

> 2.代码 `DataScopeType` 自定义一个SQL模板

![输入图片说明](https://images.gitee.com/uploads/images/2021/1217/222256_35691be8_1766278.png "屏幕截图.png")

> 3.标注权限注解

![输入图片说明](https://images.gitee.com/uploads/images/2021/1217/220813_945489ca_1766278.png "屏幕截图.png")

> 4.设置数据权限变量

![输入图片说明](https://images.gitee.com/uploads/images/2021/1217/221345_8b9e46d2_1766278.png "屏幕截图.png")

> 5.测试

![输入图片说明](https://images.gitee.com/uploads/images/2021/1217/222634_1056e8f4_1766278.png "屏幕截图.png")

### mybatis-plus 原生方法 增加数据权限过滤

首先查看需要重写的方法源码 重点`方法源码` `方法源码` `方法源码`<br>
例如重写 `selectPage` 方法<br>

![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/232058_b1cd1d4a_1766278.png "屏幕截图.png")

复制源码到自己的 `Mapper` 并增加数据权限注解 注意左边出现重写图标 即为重写成功<br>

![输入图片说明](https://images.gitee.com/uploads/images/2021/1215/232229_eb3e6000_1766278.png "屏幕截图.png")

### 支持类标注
获取规则 `方法 > 类` 注意: 类标注后 所有方法(包括父类方法) 都会进行数据权限过滤

![输入图片说明](https://images.gitee.com/uploads/images/2021/1216/105904_410f5dae_1766278.png "屏幕截图.png")


## 3.4.0 使用教程

### 实体类需继承 `BaseEntity` 基类
![输入图片说明](https://images.gitee.com/uploads/images/2021/0928/150113_e8d4bf94_1766278.png "屏幕截图.png")
### 使用 Mybatis-Plus 注入
![输入图片说明](https://images.gitee.com/uploads/images/2021/0928/150215_6e475944_1766278.png "屏幕截图.png")
### 自定义 XML 注入
![输入图片说明](https://images.gitee.com/uploads/images/2021/0928/150332_134d028d_1766278.png "屏幕截图.png")