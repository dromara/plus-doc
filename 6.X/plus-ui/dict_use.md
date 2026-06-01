# 使用字典
- - -

字典方法位于 `src/utils/dict.ts`，页面中显式导入 `useDict` 使用。

```typescript
import { useDict } from '@/utils/dict';

const { sys_normal_disable } = toRefs<any>(useDict('sys_normal_disable'));
```

一次获取多个字典：

```typescript
import { useDict } from '@/utils/dict';

const { sys_normal_disable, sys_user_sex } = toRefs<any>(
  useDict('sys_normal_disable', 'sys_user_sex')
);
```

`useDict` 的行为：

- 首次读取时调用 `getDicts(dictType)` 请求后端字典接口
- 请求完成后写入 `useDictStore()` 的 Pinia 缓存
- 同一个字典类型的并发请求会复用同一个 pending promise
- 返回项结构为 `DictDataOption`：`label`、`value`、`elTagType`、`elTagClass`

## Select

```html
<el-select v-model="queryParams.status" clearable placeholder="用户状态">
  <el-option
    v-for="dict in sys_normal_disable"
    :key="dict.value"
    :label="dict.label"
    :value="dict.value"
  />
</el-select>
```

## Radio

```html
<el-radio-group v-model="form.status">
  <el-radio v-for="dict in sys_normal_disable" :key="dict.value" :value="dict.value">
    {{ dict.label }}
  </el-radio>
</el-radio-group>
```

## Switch

```html
<el-switch
  v-model="scope.row.status"
  active-value="0"
  inactive-value="1"
  @change="handleStatusChange(scope.row)"
/>
```

## DictTag

只读展示使用 `dict-tag`，组件源码位于 `src/components/DictTag/index.vue`。

```html
<dict-tag :options="sys_normal_disable" :value="scope.row.status" />
```

完整列表页示例：

```vue
<template>
  <el-table-column label="系统内置" align="center" prop="configType">
    <template #default="scope">
      <dict-tag :options="sys_yes_no" :value="scope.row.configType" />
    </template>
  </el-table-column>
</template>

<script setup name="Config" lang="ts">
import { useDict } from '@/utils/dict';

const { sys_yes_no } = toRefs<any>(useDict('sys_yes_no'));
</script>
```

字典值通常是字符串，表单默认值也建议保持字符串类型。类型不一致时，最常见的问题是组件无法回显。
