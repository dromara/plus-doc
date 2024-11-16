# 权限使用

- - -

封装了一个指令权限，能简单快速的实现按钮级别的权限判断。`v-permission`

### 使用权限字符串 `v-hasPermi`

```html

<el-button v-hasPermi="['system:user:add']">存在权限字符串才能看到</el-button>
<el-button v-hasPermi="['system:user:add', 'system:user:edit']">包含权限字符串才能看到</el-button>
```

### 使用角色字符串 `v-hasRole`

```html

<el-button v-hasRole="['admin']">管理员才能看到</el-button>
<el-button v-hasRole="['role1', 'role2']">包含角色才能看到</el-button>
```

### 使用自定义权限字符串 `v-hasPermiCustom`

```html

<el-button type="primary" v-hasPermiCustom="['system:user:add']">添加</el-button>
<el-button type="danger" v-hasPermiCustom="['system:user:remove']">删除</el-button>
```

> **提示**:<br>
> 在某些情况下，它是不适合使用 v-hasPermi <br> 
> 如元素标签组件，只能通过手动设置v-if。<br>
> 可以使用全局权限判断函数，用法和指令 v-hasPermi 类似。

```html
<el-tabs>
    <el-tab-pane v-if="checkPermi(['system:user:add'])" label="用户管理" name="user">用户管理</el-tab-pane>
    <el-tab-pane v-if="checkPermi(['system:user:add', 'system:user:edit'])" label="参数管理" name="menu">参数管理</el-tab-pane>
    <el-tab-pane v-if="checkRole(['admin'])" label="角色管理" name="role">角色管理</el-tab-pane>
    <el-tab-pane v-if="checkRole(['admin','common'])" label="定时任务" name="job">定时任务</el-tab-pane>
</el-tabs>
```
> **前端有了鉴权后端还需要鉴权吗？**:<br>
> 前端的鉴权只是一个辅助功能，对于专业人员这些限制都是可以轻松绕过的，为保证服务器安全，无论前端是否进行了权限校验，后端接口都需要对会话请求再次进行权限校验！