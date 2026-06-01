# 常用 Hooks
- - -

项目在 `src/hooks` 下封装了列表页、弹窗、加载状态、树表格等常用组合式函数。新页面建议优先复用这些 hooks，保持页面结构和现有代码一致。

## useLoading

源码位置：`src/hooks/async/useLoading.ts`

```typescript
import { useLoading } from '@/hooks/async/useLoading';

const { loading, setLoading, withLoading } = useLoading(true);

const getList = async () => {
  await withLoading(async () => {
    const res = await listConfig(queryParams.value);
    configList.value = res.data?.rows ?? [];
  });
};
```

`withLoading` 会在异步任务开始前置为 `true`，结束后自动恢复为 `false`。

## useSearchToggle

源码位置：`src/hooks/form/useSearchToggle.ts`

```typescript
import { useSearchToggle } from '@/hooks/form/useSearchToggle';

const { showSearch, toggleSearch, setShowSearch } = useSearchToggle();
```

常用于搜索面板显隐和 `right-toolbar`：

```html
<right-toolbar v-model:show-search="showSearch" :search="false" @query-table="getList" />
```

## useDateRangeQuery

源码位置：`src/hooks/form/useDateRangeQuery.ts`

```typescript
import { useDateRangeQuery } from '@/hooks/form/useDateRangeQuery';

const { dateRange, applyDateRange, resetDateRange } = useDateRangeQuery();

const getList = async () => {
  const res = await listConfig(applyDateRange(queryParams.value));
};
```

如果后端需要指定字段名：

```typescript
const { dateRange, applyDateRange } = useDateRangeQuery('createTime');
```

## useSearchReset

源码位置：`src/hooks/form/useSearchReset.ts`

```typescript
import { useSearchReset } from '@/hooks/form/useSearchReset';

const queryFormRef = ref<ElFormInstance>();

const { resetQuery } = useSearchReset({
  queryFormRef,
  queryParams,
  pageNumKey: 'pageNum',
  resetExtras: () => {
    resetDateRange();
  },
  afterReset: () => {
    handleQuery();
  }
});
```

## useTableSelection

源码位置：`src/hooks/table/useTableSelection.ts`

```typescript
import { useTableSelection } from '@/hooks/table/useTableSelection';

const { ids, selectedRows, single, multiple, handleSelectionChange, clearSelection } =
  useTableSelection<ConfigVO>(item => item.configId);
```

模板中绑定：

```html
<el-table :data="configList" @selection-change="handleSelectionChange">
  <el-table-column type="selection" width="55" align="center" />
</el-table>

<el-button :disabled="single">修改</el-button>
<el-button :disabled="multiple">删除</el-button>
```

## useTableSortQuery

源码位置：`src/hooks/table/useTableSortQuery.ts`

```typescript
import { useTableSortQuery } from '@/hooks/table/useTableSortQuery';

const tableRef = ref<ElTableInstance>();

const { defaultSort, handleSortChange, resetSort } = useTableSortQuery({
  queryParams,
  tableRef,
  defaultSort: { prop: 'createTime', order: 'descending' },
  onSortChange: getList
});
```

模板中绑定：

```html
<el-table
  ref="tableRef"
  :data="configList"
  :default-sort="defaultSort"
  @sort-change="handleSortChange"
/>
```

## useDialogState

源码位置：`src/hooks/dialog/useDialogState.ts`

```typescript
import { useDialogState } from '@/hooks/dialog/useDialogState';

const { dialog, openDialog, closeDialog, toggleDialog, setTitle } = useDialogState();

openDialog('新增参数');
closeDialog();
```

## useFormDialog

源码位置：`src/hooks/dialog/useFormDialog.ts`

```typescript
import { useFormDialog } from '@/hooks/dialog/useFormDialog';

const formRef = ref<ElFormInstance>();
const initFormData: ConfigForm = {
  configId: undefined,
  configName: '',
  configKey: '',
  configValue: '',
  configType: 'Y',
  remark: ''
};

const form = ref<ConfigForm>({ ...initFormData });

const { dialog, resetForm, openDialog, showDialog, closeDialog } = useFormDialog({
  form,
  formRef,
  initialFormData: initFormData
});
```

新增时重置并打开弹窗：

```typescript
const handleAdd = () => {
  openDialog('添加参数');
};
```

修改时先取详情，再显示弹窗：

```typescript
const handleUpdate = async (row: ConfigVO) => {
  resetForm();
  const res = await getConfig(row.configId);
  Object.assign(form.value, res.data);
  showDialog('修改参数');
};
```

## useTreeCollapsed

源码位置：`src/hooks/tree/useTreeCollapsed.ts`

```typescript
import { useTreeCollapsed } from '@/hooks/tree/useTreeCollapsed';

const { treeCollapsed, toggleCollapsed, setCollapsed } = useTreeCollapsed();
```

常用于左树右表布局，例如系统用户页面的部门树。

## useTreeTableExpand

源码位置：`src/hooks/tree/useTreeTableExpand.ts`

```typescript
import { useTreeTableExpand } from '@/hooks/tree/useTreeTableExpand';

const tableRef = ref<ElTableInstance>();
const deptList = ref<DeptVO[]>([]);

const { isExpandAll, setExpandAll, handleToggleExpandAll } = useTreeTableExpand({
  tableRef,
  data: deptList
});
```

适合部门、菜单等树表格页面统一控制展开和收起。
