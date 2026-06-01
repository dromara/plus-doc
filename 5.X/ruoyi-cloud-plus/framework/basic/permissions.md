# 关于数据权限
- - -

## 功能概览

- 自动注入 SQL 数据过滤
- 查询、更新、删除统一受限
- 支持自定义字段过滤
- 支持 SpEL 模板与 Bean 动态处理
- 支持与菜单权限标识符联合使用（2.2.X 新功能）

## 关键组件

| 类                             | 说明           | 功能                              |
|-------------------------------|--------------|---------------------------------|
| DataScopeType                 | 数据权限模板定义     | 定义数据权限模板                        |
| DataPermission                | 数据权限组注解      | 标注开启数据权限（默认过滤部门权限）              |
| DataColumn                    | 数据权限字段标注     | 替换数据权限模板内的 `key` 变量             |
| PlusDataPermissionInterceptor | 数据权限 SQL 拦截器 | 拦截 SQL 并判断是否标注 `DataPermission` |
| PlusDataPermissionHandler     | 数据权限处理器      | 为 SQL 添加数据权限过滤条件                |
| DataPermissionHelper          | 数据权限助手       | 操作数据权限上下文变量                     |
| SysDataScopeService           | 自定义 Bean 处理  | 自定义扩展处理逻辑                       |

## 使用流程（参考 demo 模块）

数据权限体系：`用户 -> 多角色 => 角色 -> 单数据权限`。

示例场景：

- 角色 A（部门经理）：可查看本部门及以下部门数据
- 角色 B（兼职开发）：仅可查看本人数据

步骤建议：

1. 在角色管理中创建数据权限角色

![输入图片说明](https://foruda.gitee.com/images/1678978669666831574/b51ed0a3_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1678978674159035056/69cf32ad_1766278.png "屏幕截图")

2. 将角色分配给用户

![输入图片说明](https://foruda.gitee.com/images/1678978680492570269/a47b6afc_1766278.png "屏幕截图")

3. 在 Mapper 层标注数据权限注解

**注意：数据权限注解只能在 Mapper 层生效。**

补充说明：
- 数据权限和接口权限是两套机制，前者控制“能看到哪些数据”，后者控制“能不能访问这个接口”
- 大多数列表、详情、更新、删除 SQL 都建议在对应 Mapper 方法显式标注，避免只靠调用链猜测是否生效

![输入图片说明](https://foruda.gitee.com/images/1678978687179608427/d6b83c30_1766278.png "屏幕截图")

## 忽略数据权限

如需对单条 SQL 忽略数据权限，可在 Mapper 接口添加：

```java
@InterceptorIgnore(dataPermission = "true")
```

如需在业务层临时忽略数据权限，可使用：

```java
// 无返回值
DataPermissionHelper.ignore(() -> { 业务代码 });

// 有返回值
Class result = DataPermissionHelper.ignore(() -> { return 业务代码 });
```

如果同一段逻辑还涉及多租户过滤，请分别评估是否还需要配合租户忽略能力；数据权限与租户隔离彼此独立。

## 数据权限模板说明

![输入图片说明](https://foruda.gitee.com/images/1678978697141183499/cfc1cb6a_1766278.png "屏幕截图")

字段说明：

- `code`：关联角色的数据权限 code
- `sqlTemplate`：SQL 模板
- `#{#deptName}`：模板变量，对应注解中的 `key`
- `#{@sdss}`：模板中调用 Bean 处理逻辑
- `elseSql`：兜底 SQL。若角色无匹配模板可使用 `1 = 0` 进行限制

更详细用法可参考 `DataScopeType` 的注释说明。

## 测试流程示例

建议优先使用管理员用户验证模板是否生效：

![输入图片说明](https://foruda.gitee.com/images/1678978703250082481/e93a68a5_1766278.png "屏幕截图")

使用普通用户验证数据权限效果：

![输入图片说明](https://foruda.gitee.com/images/1678978710644676604/d7f80487_1766278.png "屏幕截图")

删除或更新不属于本人的数据时应被限制：

![输入图片说明](https://foruda.gitee.com/images/1678978715711122947/441d61f7_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678978720298532619/a35b1147_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1678978725329242504/a70491a1_1766278.png "屏幕截图")

## 自定义 SQL 模板

步骤建议：

1. 在角色管理的数据权限下拉框中添加自定义模板

![输入图片说明](https://foruda.gitee.com/images/1678978730563169865/3459ee17_1766278.png "屏幕截图")

2. 在 `DataScopeType` 中新增模板

![输入图片说明](https://foruda.gitee.com/images/1678978735588305505/3f030c67_1766278.png "屏幕截图")

3. 标注权限注解

![输入图片说明](https://foruda.gitee.com/images/1678978742259837391/eabe5caa_1766278.png "屏幕截图")

4. 设置数据权限变量

![输入图片说明](https://foruda.gitee.com/images/1678978746778429543/e211201f_1766278.png "屏幕截图")

5. 执行测试

![输入图片说明](https://foruda.gitee.com/images/1678978751875467640/7d210cf4_1766278.png "屏幕截图")

## MyBatis-Plus 原生方法适配

从 **2.3.0** 开始无需重写底层最终方法。  
旧版本如需对 MP 原生方法生效，可在 Mapper 中新增 `default` 方法并调用 MP 原方法。

![输入图片说明](https://foruda.gitee.com/images/1751253016695554853/be854635_1766278.png "屏幕截图")

## 类级别注解支持

注解优先级：`方法 > 类`。  
类级别标注后，类及父类方法都会参与数据权限过滤。

![输入图片说明](https://foruda.gitee.com/images/1678978767336534896/fb13ee99_1766278.png "屏幕截图")
