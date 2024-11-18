# 页签缓存

- - -

框架的页签缓存机制是利用 Vue 的 `<keep-alive>` 组件来实现的。`<keep-alive>` 是 Vue 提供的一个抽象组件，用于缓存不活动的组件实例，而不是每次切换时都销毁它们。这样，当用户切换回之前访问过的标签页时，可以避免重新渲染，从而提高应用的性能。
以下是如何在这个框架中实现页签缓存的步骤：
1. **路由和组件命名一致**：
   - 路由配置和对应的视图组件必须有一个相同的 `name` 属性。这是因为 `<keep-alive>` 默认是根据组件的 `name` 来决定哪些组件需要被缓存的。
2. **路由配置**：
   - 在路由配置中，每个路由对象都有一个 `name` 属性，这个属性对应于其视图组件的 `name`。
   ```typescript
   {
     path: 'config',
     component: () => import('@/views/system/config/index'),
     name: 'Config',
     meta: { title: '参数设置', icon: 'edit' }
   }
   ```
3. **视图组件**：
   - 视图组件也必须有一个 `name` 属性，且其值必须与路由配置中的 `name` 属性相同。
   ```typescript
   // system/config/index.vue
   export default {
     name: 'Config'
   }
   ```
4. **使用 `<keep-alive>`**：
   - 在应用的根组件或路由视图组件中，使用 `<keep-alive>` 包裹 `<router-view>`，如下所示：
   ```html
   <template>
     <keep-alive>
       <router-view></router-view>
     </keep-alive>
   </template>
   ```
5. **配置页签缓存**：
   - 根据提示，系统管理-菜单管理中可以配置菜单页签是否缓存。这意味着框架可能允许管理员通过配置来决定哪些页签应该被缓存。
6. **动态缓存**：
   - 如果需要更细粒度的控制，可以使用 `<keep-alive>` 的 `include` 或 `exclude` 属性来动态指定哪些组件应该被缓存。
   ```html
   <keep-alive :include="cachedViews">
     <router-view></router-view>
   </keep-alive>
   ```
   在这个例子中，`cachedViews` 是一个包含所有应该被缓存的组件名称的数组。
总结来说，页签缓存机制依赖于 Vue 的 `<keep-alive>` 组件，通过确保路由和组件的 `name` 属性一致，以及通过配置来控制哪些页签应该被缓存。这种方法可以提高用户体验，减少不必要的页面加载时间。<br>
> 具体实现可阅读源码：`src/layout/components/AppMain.vue`