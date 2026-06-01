# 权限使用

- - -

前端封装了权限指令与权限判断函数，可快速实现按钮级别的显隐控制。

### 使用权限字符串 `v-hasPermi`

```html

<el-button v-hasPermi="['system:user:add']">存在权限字符串才能看到</el-button>
<el-button v-hasPermi="['system:user:add', 'system:user:edit']">包含权限字符串才能看到</el-button>
```

### 使用角色字符串 `v-hasRoles`

```html

<el-button v-hasRoles="['admin']">管理员才能看到</el-button>
<el-button v-hasRoles="['role1', 'role2']">包含角色才能看到</el-button>
```

补充说明：
- 当前项目注册的指令是 `v-hasPermi` 与 `v-hasRoles`
- 指令本质上会在无权限时直接移除对应 DOM 元素
- 超级权限会按前端权限工具内置规则直接放行

### 使用全局权限函数

在某些情况下不适合直接使用指令，例如 `el-tab-pane`、动态列、复杂渲染片段等场景，此时更适合配合 `v-if` 使用全局权限函数。

```html
<el-tabs>
    <el-tab-pane v-if="checkPermi(['system:user:add'])" label="用户管理" name="user">用户管理</el-tab-pane>
    <el-tab-pane v-if="checkPermi(['system:user:add', 'system:user:edit'])" label="参数管理" name="menu">参数管理</el-tab-pane>
    <el-tab-pane v-if="checkRole(['admin'])" label="角色管理" name="role">角色管理</el-tab-pane>
    <el-tab-pane v-if="checkRole(['admin','common'])" label="定时任务" name="job">定时任务</el-tab-pane>
</el-tabs>
```

补充说明：
- `checkPermi` / `checkRole` 是前端辅助函数，通常用于模板里的条件判断
- 指令和函数都依赖当前登录用户返回的 `permissions`、`roles` 数据

> **前端有了鉴权后端还需要鉴权吗？**:<br>
> 前端的鉴权只是一个辅助功能，对于专业人员这些限制都是可以轻松绕过的，为保证服务器安全，无论前端是否进行了权限校验，后端接口都需要对会话请求再次进行权限校验！
