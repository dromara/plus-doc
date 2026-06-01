# 路由使用
- - -

前端路由由 `src/router/index.ts`、`src/store/modules/permission.ts` 和后端菜单共同组成。

## 静态路由

静态路由位于 `src/router/index.ts` 的 `constantRoutes`，用于登录、注册、错误页、首页、个人中心等无需动态权限加载的页面。

```typescript
export const constantRoutes: RouteRecordRaw[] = [
  {
    path: '/login',
    component: () => import('@/views/login.vue'),
    hidden: true
  },
  {
    path: '',
    component: Layout,
    redirect: '/index',
    children: [
      {
        path: '/index',
        component: () => import('@/views/index.vue'),
        name: 'Index',
        meta: { title: '首页', icon: 'dashboard', affix: true }
      }
    ]
  }
];
```

路由历史模式使用：

```typescript
createWebHistory(import.meta.env.VITE_APP_CONTEXT_PATH)
```

部署到二级目录时，需要同步配置 `VITE_APP_CONTEXT_PATH`。

## 动态路由

动态菜单由后端返回，前端在 `src/store/modules/permission.ts` 中调用 `getRouters()`，再通过 `filterAsyncRouter` 转换为 Vue Router 可识别的路由。

动态菜单中的 `component` 字段使用字符串：

| component | 说明 |
| --- | --- |
| `Layout` | 主布局组件 |
| `ParentView` | 父级占位组件 |
| `InnerLink` | 内链 iframe 组件 |
| `system/user/index` | 对应 `src/views/system/user/index.vue` |

视图组件通过下面的方式预加载映射：

```typescript
const modules = import.meta.glob('./../../views/**/*.vue');
```

加载时会调用：

```typescript
loadView(route.component, route.name as string);
```

`loadView` 会通过 `createCustomNameComponent` 给动态组件补充组件名，所以后端菜单里的 `name` 必须唯一。

## 菜单字段

常用路由字段：

```typescript
{
  path: '/system/user',
  component: 'Layout',
  redirect: 'noRedirect',
  hidden: false,
  alwaysShow: true,
  name: 'System',
  meta: {
    title: '系统管理',
    icon: 'system',
    noCache: false,
    breadcrumb: true,
    affix: false,
    activeMenu: '/system/user'
  },
  children: [
    {
      path: 'index',
      component: 'system/user/index',
      name: 'User',
      meta: {
        title: '用户管理',
        icon: 'user',
        noCache: false
      }
    }
  ]
}
```

字段说明：

| 字段 | 说明 |
| --- | --- |
| `hidden` | 是否在侧边栏隐藏 |
| `alwaysShow` | 只有一个子路由时仍显示父级菜单 |
| `redirect: 'noRedirect'` | 面包屑不可点击 |
| `name` | 路由名称，必须唯一 |
| `query` | 默认 query 参数，通常为 JSON 字符串 |
| `roles` | 本地动态路由角色权限 |
| `permissions` | 本地动态路由权限字符串 |
| `meta.title` | 菜单、面包屑、页签标题 |
| `meta.icon` | 图标名，对应 `src/assets/icons/svg` |
| `meta.noCache` | 是否不缓存页面 |
| `meta.breadcrumb` | 是否显示面包屑 |
| `meta.affix` | 是否固定页签 |
| `meta.activeMenu` | 当前页面高亮的菜单路径 |

## 外链和内链

普通外链可直接配置完整 URL：

```typescript
{
  path: 'https://gitee.com/dromara/RuoYi-Vue-Plus',
  meta: { title: '项目地址', icon: 'guide' }
}
```

内链 iframe 使用 `InnerLink`，最终由 `AppMain.vue` 中的 `iframe-toggle` 处理。

## 跳转页面

页面中使用 Vue Router：

```typescript
const router = useRouter();

router.push({ path: '/system/user' });
router.push({ path: '/system/user', query: { id: '1', name: '若依' } });
```

如果跳转同时希望打开页签，也可以使用 `tab.openPage`：

```typescript
import tab from '@/plugins/tab';

await tab.openPage('/system/user', '用户管理', { deptId: 100 });
```

## 注意事项

- 路由 `name` 不能为空，也不能重复；项目启动后会检查重复名称并弹出错误提示。
- 页面缓存依赖路由 `name` 和组件名，详见 [页签缓存](/6.X/plus-ui/page_cache.md)。
- 后端菜单中的组件路径不要以 `@/views` 开头，填写 `system/user/index` 这类相对 `views` 的路径。
- 新增页面后，如果出现 404，优先检查菜单组件路径、路由名称重复、页面文件路径。
