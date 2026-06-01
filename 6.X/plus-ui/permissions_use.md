# 权限使用
- - -

前端权限由指令、工具函数和 `auth` 插件共同提供，数据来自当前登录用户的 `permissions` 与 `roles`。

## 权限指令

指令注册位置：`src/directive/index.ts`

```typescript
app.directive('hasPermi', hasPermi);
app.directive('hasRoles', hasRoles);
```

模板中使用：

```html
<el-button v-hasPermi="['system:user:add']" type="primary" icon="Plus">
  新增
</el-button>

<el-button v-hasPermi="['system:user:edit']" type="success" icon="Edit">
  修改
</el-button>

<el-button v-hasRoles="['admin']" type="danger">
  管理员可见
</el-button>
```

无权限时，指令会直接移除当前 DOM 元素。权限指令适合普通按钮、普通链接这类立即渲染的元素。

## 条件判断函数

延迟渲染的组件或插槽中，指令可能无法稳定执行，例如 `el-dropdown-item`。这类场景使用 `checkPermi`、`checkRole`：

```typescript
import { checkPermi, checkRole } from '@/utils/permission';
```

```html
<el-dropdown-menu>
  <el-dropdown-item v-if="checkPermi(['system:user:import'])" icon="Top" @click="handleImport">
    导入数据
  </el-dropdown-item>
  <el-dropdown-item v-if="checkPermi(['system:user:export'])" icon="Download" @click="handleExport">
    导出数据
  </el-dropdown-item>
  <el-dropdown-item v-if="checkRole(['admin'])" icon="User">
    管理员操作
  </el-dropdown-item>
</el-dropdown-menu>
```

## 脚本中判断权限

源码位置：`src/plugins/auth.ts`

```typescript
import auth from '@/plugins/auth';

if (auth.hasPermi('system:user:add')) {
  // 有新增权限
}

if (auth.hasPermiOr(['system:user:add', 'system:user:edit'])) {
  // 拥有其中一个权限
}

if (auth.hasRole('admin')) {
  // 管理员角色
}
```

方法说明：

| 方法 | 说明 |
| --- | --- |
| `hasPermi(permission)` | 是否拥有指定权限 |
| `hasPermiOr(permissions)` | 是否拥有任一权限 |
| `hasPermiAnd(permissions)` | 是否拥有全部权限 |
| `hasRole(role)` | 是否拥有指定角色 |
| `hasRoleOr(roles)` | 是否拥有任一角色 |
| `hasRoleAnd(roles)` | 是否拥有全部角色 |

前端权限只负责界面显隐，后端接口仍必须做权限校验。
