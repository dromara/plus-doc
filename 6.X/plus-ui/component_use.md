# 组件使用
- - -

当前项目通过 Vite 插件自动导入 Vue API、Vue Router、Pinia、VueUse、Element Plus 组件和 Element Plus 相关函数。

## 自动导入配置

Vue API 自动导入配置位于 `vite/plugins/auto-import.ts`：

```typescript
AutoImport({
  imports: ['vue', 'vue-router', '@vueuse/core', 'pinia'],
  resolvers: [
    ElementPlusResolver({
      importStyle: false
    })
  ],
  vueTemplate: true,
  dts: resolve(import.meta.dirname, '../../src/types/auto-imports.d.ts')
});
```

Element Plus 组件自动导入配置位于 `vite/plugins/components.ts`：

```typescript
Components({
  resolvers: [
    ElementPlusResolver({
      importStyle: false
    })
  ],
  dts: resolve(import.meta.dirname, '../../src/types/components.d.ts')
});
```

因此页面中可以直接使用：

```vue
<template>
  <el-button type="primary" icon="Search" @click="handleQuery">
    搜索
  </el-button>
</template>

<script setup name="Demo" lang="ts">
const keyword = ref('');
const router = useRouter();

const handleQuery = () => {
  router.push({ path: '/system/user', query: { keyword: keyword.value } });
};
</script>
```

## 业务组件

`src/components` 下的项目组件在现有页面中通常可直接使用，例如：

```vue
<pagination
  v-show="total > 0"
  v-model:page="queryParams.pageNum"
  v-model:limit="queryParams.pageSize"
  :total="total"
  @pagination="getList"
/>

<dict-tag :options="sys_yes_no" :value="scope.row.configType" />

<right-toolbar
  v-model:show-search="showSearch"
  :search="false"
  @query-table="getList"
/>
```

如果是当前业务目录下的组件，建议显式导入：

```vue
<script setup name="User" lang="ts">
import UserDetail from './components/UserDetail.vue';
</script>

<template>
  <user-detail v-model:visible="detailVisible" :user-id="currentUserId" />
</template>
```

## 全局插件

入口文件 `src/main.ts` 注册了这些插件和指令：

```typescript
app.use(HighLight);
app.use(ElementIcons);
app.use(router);
app.use(store);
app.use(i18n);
app.use(VXETable);
app.use(plugins);
directive(app);
```

`ElementIcons` 会注册 `@element-plus/icons-vue` 中的图标组件，所以按钮里可直接写：

```html
<el-button icon="Plus">新增</el-button>
<el-button icon="Download">导出</el-button>
```

自定义 SVG 图标使用 `svg-icon`：

```html
<svg-icon icon-class="user" />
```

## 样式与表格能力

- UnoCSS 由 `vite/plugins/unocss.ts` 接入，规则集中在 `uno.config.ts`，当前使用 `presetWind3`、`presetAttributify`、图标/排版相关预设与常用 transformer。
- VXETable 在 `src/main.ts` 中通过 `app.use(VXETable)` 全局注册，适合复杂表格、虚拟滚动、编辑表格等场景；普通后台列表页仍优先使用 Element Plus 表格与项目通用分页组件。

## 使用建议

- Vue API、Vue Router、Pinia、VueUse API 可以直接使用自动导入结果。
- Element Plus 组件和常用反馈函数可以直接使用。
- 业务组件如果不确定是否已自动注册，优先显式导入。
- 页面组件名使用 `<script setup name="Xxx" lang="ts">`，并与路由 `name` 保持一致。
