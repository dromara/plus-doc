# 页签缓存

- - -

框架的页签缓存机制基于 Vue 的 `<keep-alive>` 实现。当前项目并不是简单地把整个 `<router-view>` 缓存，而是通过 `tagsViewStore.cachedViews` 动态控制哪些页面进入缓存列表。<br>
> 具体实现可阅读源码：`src/layout/components/AppMain.vue`

### 1. 缓存的核心条件

- 路由必须有唯一且非空的 `name`，否则页签缓存、刷新、关闭等行为都容易异常。
- 页面组件名必须和路由 `name` 保持一致，当前项目推荐写法是 `<script setup name="Config" lang="ts">`。
- 路由 `meta.noCache` 为 `true` 时，不会进入缓存列表。

```typescript
{
  path: 'config',
  component: () => import('@/views/system/config/index.vue'),
  name: 'Config',
  meta: { title: '参数设置', noCache: false }
}
```

```vue
<script setup name="Config" lang="ts">
// ...
</script>
```

### 2. 项目中的实际缓存方式

当前项目在 `AppMain.vue` 中使用的是下面这种模式：

```vue
<router-view v-slot="{ Component, route }">
  <keep-alive :include="tagsViewStore.cachedViews">
    <component :is="Component" v-if="!route.meta.link" :key="route.path" />
  </keep-alive>
</router-view>
```

补充说明：

- `cachedViews` 由 `src/store/modules/tagsView.ts` 维护。
- 页面首次进入并生成页签后，才会被加入缓存列表。
- 关闭页签、关闭左右页签、关闭其他页签时，会同步删除对应缓存。
- 固定页签 `affix` 只能固定标签，不代表一定缓存，是否缓存仍取决于 `noCache`。

### 3. 菜单缓存配置

- 后端菜单管理里可以配置“是否缓存”，最终会影响前端动态路由的 `meta.noCache`。
- 如果菜单设置为不缓存，即使页面组件名称正确，也不会进入 `<keep-alive>`。
- 页面调试时如果发现“切走再回来数据丢失”，先检查菜单缓存配置、路由 `name`、组件 `name` 这三处是否一致。

### 4. 常见注意事项

- 路由 `name` 重复，会导致不同页面共用同一份缓存，表现通常是页面内容串页。
- 不要再使用旧版 Vue2 的 `export default { name: 'xxx' }` 作为本文示例理解当前项目，当前项目主流写法是 `script setup + name`。
- 带 `meta.link` 的外链页面走的是 `iframeViews` 逻辑，不属于普通 `keep-alive` 缓存。
