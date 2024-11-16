# 使用字典
- - -

### 在对应页面中导入需要使用的字典

``` typescript
const { sys_normal_disable } = toRefs<any>(proxy?.useDict('sys_normal_disable'));
```

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

### Form中以`radio`形式使用

``` html
<el-radio-group v-model="form.status">
    <el-radio v-for="dict in sys_normal_disable" :key="dict.value" :value="dict.value">
        {{ dict.label }}
    </el-radio>
</el-radio-group>
```

