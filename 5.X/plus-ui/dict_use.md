# 使用字典
- - -

### 在对应页面中导入需要使用的字典

``` typescript
const { sys_normal_disable } = toRefs<any>(proxy?.useDict('sys_normal_disable'));
```

也可以一次获取多个字典：

```typescript
const { sys_normal_disable, sys_user_sex } = toRefs<any>(proxy?.useDict('sys_normal_disable', 'sys_user_sex'));
```

补充说明：
- `useDict` 已经挂载到全局 `proxy` 上
- 首次获取会请求后端字典接口，之后会走 Pinia 字典缓存
- 返回的每项数据通常包含 `label`、`value`、`elTagType`、`elTagClass`

### Form中以`select`形式使用

``` html
<el-select v-model="queryParams.status" clearable placeholder="用户状态">
    <el-option v-for="dict in sys_normal_disable" :key="dict.value" :label="dict.label" :value="dict.value" />
</el-select>
```

### 表格中以`switch`形式使用

``` html
<template #default="scope">
    <el-switch v-model="scope.row.status" active-value="0" inactive-value="1" @change="handleStatusChange(scope.row)">
    </el-switch>
</template>
```

### 表格中以`tag`形式使用

``` html
<template #default="scope">
    <dict-tag :options="sys_normal_disable" :value="scope.row.status" />
</template>
```

组件详情参考 `src/components/DictTag/index.vue`

`dict-tag` 适合表格、详情页这类只读展示场景，可自动带出字典标签样式。

### Form中以`radio`形式使用

``` html
<el-radio-group v-model="form.status">
    <el-radio v-for="dict in sys_normal_disable" :key="dict.value" :value="dict.value">
        {{ dict.label }}
    </el-radio>
</el-radio-group>
```

补充说明：
- 如果后端返回值是字符串，表单组件里的 `value` 也建议保持字符串类型
- 字典值和表单默认值类型不一致时，最常见的问题就是“回显不出来”

