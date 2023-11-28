# 权限控制
- - -

本文采用 `Sa-Token` 框架实现权限控制。[官方文档传送门](https://sa-token.cc/doc.html#/)

## 权限校验
权限校验指的是校验用户是否拥有访问某个 API 的能力。

通常情况下，一个 API 对应一个权限码，如果用户具备当前 API 的权限码，即代表有能力访问该 API。

### 1：权限标识
在本系统中，每一个菜单功能都有对应的权限标识，可以在菜单管理中进行设置。

> 注：
> 1. 前后端的权限标识要保持一致。
> 2. 权限标识可以使用通配符`*`。

![输入图片说明](https://foruda.gitee.com/images/1701086497939145368/133fb327_4959041.png "屏幕截图")


### 2：校验方法
#### 2.1：使用 `@SaCheckPermission` 注解进行校验
`@SaCheckPermission` 注解是由 `Sa-Token` 框架提供的角色校验注解，可以标注在方法上或类上。

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

#### 2.2：使用 `StpUtil` 工具类校验
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

## 角色校验
角色校验指的是校验用户是否拥有某个指定角色。

### 1：权限标识
在本系统中，每个角色都拥有唯一的权限字符。

除了超级管理员角色外，其他角色的权限字符可以通过角色管理进行设置。

![输入图片说明](https://foruda.gitee.com/images/1701085080527279823/3255961d_4959041.png "屏幕截图")

### 2：校验方法
#### 2.1：使用 `@SaCheckRole` 注解校验
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

#### 2.2：使用 `StpUtil` 工具类校验
`StpUtil` 工具类是由 `Sa-Token` 框架提供的权限工具类，提供了常用的校验方法。

- 判断当前用户是否拥有某个角色（返回 `boolean`）：

```Java
StpUtil.hasRole("superadmin")
```

- 单个权限校验：

```Java
StpUtil.checkRole("system:user:list");
```
如果验证未通过，则抛出异常: `NotRoleException`

- 多个权限校验（或模式，满足任意一个角色即可）：

```Java
StpUtil.checkRoleOr("system:user:list", "system:user:query");
```
如果验证未通过，则抛出异常: `NotRoleException`

- 多个权限校验（与模式，必须满足所有角色）：

```Java
StpUtil.checkRoleAnd("system:user:list", "system:user:query");
```
如果验证未通过，则抛出异常: `NotRoleException`

## 当前用户的所有权限
本系统中实现了 `StpInterface` 接口，可以对用户的权限以及角色进行管理，并且可以根据不同的用户类型进行设置。

具体参考类：`org.dromara.common.satoken.core.service.SaPermissionImpl`

## 忽略权限校验
请参考文档：[网关路由与放行](/ruoyi-cloud-plus/framework/basic/router_release?id=网关路由与放行)

## API 加密校验
### API 加密注解 `@ApiEncrypt`
1. 对于标注了 `@ApiEncrypt` 注解的接口，请求参数都必须进行加密。
2. 注解的参数 `response` 为响应加密标识，默认 `false` 不加密，为 `true` 表示响应加密。
3. 加密解密逻辑由过滤器实现，详情可参考 `org.dromara.common.encrypt.filter.CryptoFilter`。

### API 加密配置
`application-common.yml`

![输入图片说明](https://foruda.gitee.com/images/1701133628809355269/8979704a_4959041.png "屏幕截图")

`.env.development` / `.env.production`

![输入图片说明](https://foruda.gitee.com/images/1701131922417984949/7f91d943_4959041.png "屏幕截图")

> 注：
> 1. 注意修改 Nacos 配置。
> 2. 公私钥与前端配置文件互为配对，如果需要更换请一同更换。
> 3. 后端公钥对应前端私钥；后端私钥对应前端公钥。
