# 权限控制
- - -

本文采用 `Sa-Token` 框架实现权限控制。[官方文档传送门](https://sa-token.cc/doc.html#/)

## 权限校验
权限校验指的是校验用户是否拥有访问某个 API 的能力。

通常情况下，一个 API 对应一个权限码，如果用户具备当前 API 的权限码，即代表有能力访问该 API。

### 1. 权限标识
在本系统中，每一个菜单功能都有对应的权限标识，可以在菜单管理中进行设置。

> 注：
> 1. 前后端的权限标识要保持一致。
> 2. 权限标识可以使用通配符`*`。
> 3. 前端按钮显隐可配合 `v-has-permi` / `v-has-roles` 使用，但这只是界面控制，不能替代后端接口鉴权。

![输入图片说明](https://foruda.gitee.com/images/1701086497939145368/133fb327_4959041.png "屏幕截图")


### 2. 校验方法
#### 2.1 使用 `@SaCheckPermission` 注解校验
`@SaCheckPermission` 注解是由 `Sa-Token` 框架提供的权限校验注解，可以标注在方法上或类上。

- 单个权限校验：

```Java
@SaCheckPermission("system:user:list")
```

- 多个权限校验（或模式，满足任意一个权限即可）：

```Java
@SaCheckPermission(
    value = {
        "system:user:list", 
        "system:user:query"
    }, 
    mode = SaMode.OR
)
```

- 多个权限校验（与模式，必须满足所有权限）：

```Java
@SaCheckPermission(
    value = {
        "system:user:list", 
        "system:user:query"
    }, 
    mode = SaMode.AND
)
```

#### 2.2 使用 `StpUtil` 工具类校验
`StpUtil` 工具类是由 `Sa-Token` 框架提供的权限工具类，提供了常用的校验方法。

- 判断当前用户是否拥有某个权限（返回 `boolean`）：

```Java
StpUtil.hasPermission("system:user:list");
```

- 单个权限校验：

```Java
StpUtil.checkPermission("system:user:list");
```
如果验证未通过，则抛出异常: `NotPermissionException`

- 多个权限校验（或模式，满足任意一个权限即可）：

```Java
StpUtil.checkPermissionOr("system:user:list", "system:user:query");
```
如果验证未通过，则抛出异常: `NotPermissionException`

- 多个权限校验（与模式，必须满足所有权限）：

```Java
StpUtil.checkPermissionAnd("system:user:list", "system:user:query");
```
如果验证未通过，则抛出异常: `NotPermissionException`

## 完整 Controller 示例

以“客户管理”为例，后端接口建议同时写清楚菜单权限码，前端按钮权限也使用同一套标识。

```java
@Validated
@RequiredArgsConstructor
@RestController
@RequestMapping("/crm/customer")
public class CustomerController extends BaseController {

    private final ICustomerService customerService;

    /** 查询客户列表 */
    @SaCheckPermission("crm:customer:list")
    @GetMapping("/list")
    public TableDataInfo<CustomerVo> list(CustomerBo bo, PageQuery pageQuery) {
        return customerService.queryPageList(bo, pageQuery);
    }

    /** 查询客户详情 */
    @SaCheckPermission("crm:customer:query")
    @GetMapping("/{customerId}")
    public R<CustomerVo> getInfo(@NotNull(message = "主键不能为空") @PathVariable Long customerId) {
        return R.ok(customerService.queryById(customerId));
    }

    /** 新增客户 */
    @SaCheckPermission("crm:customer:add")
    @Log(title = "客户管理", businessType = BusinessType.INSERT)
    @RepeatSubmit
    @PostMapping
    public R<Void> add(@Validated(AddGroup.class) @RequestBody CustomerBo bo) {
        return toAjax(customerService.insertByBo(bo));
    }

    /** 修改客户 */
    @SaCheckPermission("crm:customer:edit")
    @Log(title = "客户管理", businessType = BusinessType.UPDATE)
    @RepeatSubmit
    @PutMapping
    public R<Void> edit(@Validated(EditGroup.class) @RequestBody CustomerBo bo) {
        return toAjax(customerService.updateByBo(bo));
    }

    /** 删除客户 */
    @SaCheckPermission("crm:customer:remove")
    @Log(title = "客户管理", businessType = BusinessType.DELETE)
    @DeleteMapping("/{customerIds}")
    public R<Void> remove(@PathVariable Long[] customerIds) {
        return toAjax(customerService.deleteWithValidByIds(Arrays.asList(customerIds), true));
    }
}
```

对应菜单按钮权限建议：

| 操作 | 权限标识 |
| --- | --- |
| 列表 | `crm:customer:list` |
| 详情 | `crm:customer:query` |
| 新增 | `crm:customer:add` |
| 修改 | `crm:customer:edit` |
| 删除 | `crm:customer:remove` |
| 导出 | `crm:customer:export` |

前端按钮示例：

```vue
<el-button v-hasPermi="['crm:customer:add']" type="primary" icon="Plus" @click="handleAdd">
  新增
</el-button>
```

注意：前端 `v-hasPermi` 只控制显隐，真正的安全控制必须以后端 `@SaCheckPermission` 为准。

## 角色校验
角色校验指的是校验用户是否拥有某个指定角色。

### 1. 角色标识
在本系统中，每个角色都拥有唯一的权限字符。

除了超级管理员角色外，其他角色的权限字符可以通过角色管理进行设置。

![输入图片说明](https://foruda.gitee.com/images/1701085080527279823/3255961d_4959041.png "屏幕截图")

### 2. 校验方法
#### 2.1 使用 `@SaCheckRole` 注解校验
`@SaCheckRole` 注解是由 `Sa-Token` 框架提供的角色校验注解，可以标注在方法上或类上。

- 单个角色校验

```Java
@SaCheckRole("superadmin")
```

- 多个角色校验（或模式，满足任意一个角色即可）：

```Java
@SaCheckRole(
    value = {
        "superadmin", 
        "admin"
    }, 
    mode = SaMode.OR
)
```

- 多个角色校验（与模式，必须满足所有角色）：

```Java
@SaCheckRole(
    value = {
        "superadmin", 
        "admin"
    }, 
    mode = SaMode.AND
)
```

#### 2.2 使用 `StpUtil` 工具类校验
`StpUtil` 工具类是由 `Sa-Token` 框架提供的权限工具类，提供了常用的校验方法。

- 判断当前用户是否拥有某个角色（返回 `boolean`）：

```Java
StpUtil.hasRole("superadmin")
```

- 单个角色校验：

```Java
StpUtil.checkRole("admin");
```
如果验证未通过，则抛出异常: `NotRoleException`

- 多个角色校验（或模式，满足任意一个角色即可）：

```Java
StpUtil.checkRoleOr("superadmin", "admin");
```
如果验证未通过，则抛出异常: `NotRoleException`

- 多个角色校验（与模式，必须满足所有角色）：

```Java
StpUtil.checkRoleAnd("superadmin", "admin");
```
如果验证未通过，则抛出异常: `NotRoleException`

## 角色权限双重 `OR` 校验
除了分开校验以外，权限和角色也可以进行组合，表示备选校验。

简单举个例子：

假设某个 API 的权限码为 `system:user:list`，角色 `admin` 可以调用，则可以这样写：

```Java
@SaCheckPermission(value = "system:user:list", orRole = "admin")
```

以上权限只需要满足任意一项即可。更多写法可以参考 `Sa-Token` [官方文档](https://sa-token.cc/doc.html#/use/at-check?id=_4%e3%80%81%e8%a7%92%e8%89%b2%e6%9d%83%e9%99%90%e5%8f%8c%e9%87%8d-or%e6%a0%a1%e9%aa%8c)。

## 当前用户的所有权限
本系统中实现了 `StpInterface` 接口，可以对用户的权限以及角色进行管理，并且可以根据不同的用户类型进行设置。

具体参考类：`org.dromara.common.satoken.core.service.SaPermissionImpl`

前端按钮控制默认也是基于当前登录用户返回的 `permissions`、`roles` 集合做判断。

## 忽略权限校验
请参考文档：[接口放行](/6.X/ruoyi-vue-plus/framework/basic/interface_release?id=接口放行)


