# 组件使用
- - -

项目主要有两种组件使用方式：自动导入使用、手动导入使用。

补充说明：
- 项目已经通过 `unplugin-vue-components` 自动导入 `Element Plus` 组件
- `@/components` 下的业务组件是否能直接使用，取决于当前是否被自动扫描或是否手动引入
- 不确定时，优先显式 `import`，可读性更强，也更方便排查类型问题

### 局部注册

`script setup` 中直接导入后即可在模板使用：

```typescript
<script setup lang=ts>
import ComponentA from './ComponentA.vue'
</script>

<template>
  <ComponentA />
</template>
```

### 全局注册
可以使用 [Vue 应用实例](https://cn.vuejs.org/guide/essentials/application.html) 的 `.component()` 方法全局注册组件。

```typescript
import { createApp } from 'vue'

const app = createApp({})

app.component(
  // 注册的名字
  'MyComponent',
  // 组件的实现
  {
    /* ... */
  }
)
```
如果使用单文件组件，你可以注册被导入的 `.vue` 文件：
```typescript
import MyComponent from './App.vue'

app.component('MyComponent', MyComponent)
```
`.component()` 方法可以被链式调用：
```typescript
app
  .component('ComponentA', ComponentA)
  .component('ComponentB', ComponentB)
  .component('ComponentC', ComponentC)
```

项目中的常见现状：
- `Element Plus` 组件通常无需手写注册
- `@element-plus/icons-vue` 图标已在启动时全局注册
- 业务组件如 `SvgIcon`、`Pagination`、`DictTag` 等，使用前建议先确认项目中是否已有自动导入或统一导出约定

全局注册后的组件可以在任意模板中直接使用：

```Typescript
// 这在当前应用的任意组件中都可用
<ComponentA/>
<ComponentB/>
<ComponentC/>
```

所有子组件也都可以继续使用这些全局组件。
