# 列表页写法
- - -

列表页建议按“API 类型、页面状态、hooks、查询、弹窗、提交”组织。下面示例贴近当前 `src/views/system/config/index.vue` 的写法。

## API 类型

接口类型放在 `src/api/system/config/types.ts`：

```typescript
export interface ConfigQuery extends PageQuery {
  configName?: string;
  configKey?: string;
  configType?: string;
}

export interface ConfigVO extends BaseEntity {
  configId: string | number;
  configName: string;
  configKey: string;
  configValue: string;
  configType: string;
  remark: string;
}

export interface ConfigForm {
  configId?: string | number;
  configName: string;
  configKey: string;
  configValue: string;
  configType: string;
  remark?: string;
}
```

接口函数放在 `src/api/system/config/index.ts`：

```typescript
import type { PageResult } from '@/api/types';
import type { AxiosPromise } from '@/utils/api-types';
import request from '@/utils/request';
import type { ConfigForm, ConfigQuery, ConfigVO } from './types';

export function listConfig(query: ConfigQuery): AxiosPromise<PageResult<ConfigVO>> {
  return request({
    url: '/system/config/list',
    method: 'get',
    params: query
  });
}

export function getConfig(configId: string | number): AxiosPromise<ConfigVO> {
  return request({
    url: '/system/config/' + configId,
    method: 'get'
  });
}

export function addConfig(data: ConfigForm) {
  return request({
    url: '/system/config',
    method: 'post',
    data
  });
}

export function updateConfig(data: ConfigForm) {
  return request({
    url: '/system/config',
    method: 'put',
    data
  });
}

export function delConfig(configId: string | number | Array<string | number>) {
  return request({
    url: '/system/config/' + configId,
    method: 'delete'
  });
}
```

## 页面状态

```typescript
import { addConfig, delConfig, getConfig, listConfig, updateConfig } from '@/api/system/config';
import type { ConfigForm, ConfigQuery, ConfigVO } from '@/api/system/config/types';
import { useLoading } from '@/hooks/async/useLoading';
import { useFormDialog } from '@/hooks/dialog/useFormDialog';
import { useDateRangeQuery } from '@/hooks/form/useDateRangeQuery';
import { useSearchReset } from '@/hooks/form/useSearchReset';
import { useSearchToggle } from '@/hooks/form/useSearchToggle';
import { useTableSelection } from '@/hooks/table/useTableSelection';
import modal from '@/plugins/modal';
import { useDict } from '@/utils/dict';
import { download as requestDownload } from '@/utils/request';

const { sys_yes_no } = toRefs<any>(useDict('sys_yes_no'));

const list = ref<ConfigVO[]>([]);
const total = ref(0);
const queryFormRef = ref<ElFormInstance>();
const formRef = ref<ElFormInstance>();

const { loading, withLoading } = useLoading(true);
const { showSearch } = useSearchToggle();
const { dateRange, applyDateRange, resetDateRange } = useDateRangeQuery();
const { ids, single, multiple, handleSelectionChange } = useTableSelection<ConfigVO>(item => item.configId);
```

## 表单数据

```typescript
const initFormData: ConfigForm = {
  configId: undefined,
  configName: '',
  configKey: '',
  configValue: '',
  configType: 'Y',
  remark: ''
};

const data = reactive<PageData<ConfigForm, ConfigQuery>>({
  form: { ...initFormData },
  queryParams: {
    pageNum: 1,
    pageSize: 10,
    configName: '',
    configKey: '',
    configType: ''
  },
  rules: {
    configName: [{ required: true, message: '参数名称不能为空', trigger: 'blur' }],
    configKey: [{ required: true, message: '参数键名不能为空', trigger: 'blur' }],
    configValue: [{ required: true, message: '参数键值不能为空', trigger: 'blur' }]
  }
});

const { queryParams, form, rules } = toRefs(data);
```

## 弹窗和重置

```typescript
const { dialog, resetForm, openDialog, showDialog, closeDialog } = useFormDialog({
  form,
  formRef,
  initialFormData: initFormData
});

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

## 查询和分页

```typescript
const getList = async () => {
  await withLoading(async () => {
    const res = await listConfig(applyDateRange(queryParams.value));
    list.value = res.data?.rows ?? [];
    total.value = res.data?.total ?? 0;
  });
};

const handleQuery = () => {
  queryParams.value.pageNum = 1;
  getList();
};
```

模板：

```html
<el-table
  v-loading="loading"
  border
  class="data-table"
  :data="list"
  @selection-change="handleSelectionChange"
>
  <el-table-column type="selection" width="55" align="center" />
</el-table>

<pagination
  v-show="total > 0"
  v-model:page="queryParams.pageNum"
  v-model:limit="queryParams.pageSize"
  :total="total"
  @pagination="getList"
/>
```

## 新增和修改

```typescript
const handleAdd = () => {
  openDialog('添加参数');
};

const handleUpdate = async (row?: ConfigVO) => {
  resetForm();
  const configId = row?.configId || ids.value[0];
  const res = await getConfig(configId);
  Object.assign(form.value, res.data);
  showDialog('修改参数');
};

const submitForm = () => {
  formRef.value?.validate(async (valid: boolean) => {
    if (!valid) return;
    form.value.configId ? await updateConfig(form.value) : await addConfig(form.value);
    modal.msgSuccess('操作成功');
    closeDialog();
    await getList();
  });
};
```

## 删除和导出

```typescript
const handleDelete = async (row?: ConfigVO) => {
  const configIds = row?.configId || ids.value;
  await modal.confirm('是否确认删除参数编号为"' + configIds + '"的数据项？');
  await delConfig(configIds);
  await getList();
  modal.msgSuccess('删除成功');
};

const handleExport = () => {
  requestDownload(
    'system/config/export',
    { ...queryParams.value },
    `config_${new Date().getTime()}.xlsx`
  );
};
```

## 初始化

```typescript
onMounted(() => {
  getList();
});
```

这个结构适合常规 CRUD 页面。树表格、左树右表、拖拽排序等页面可以在此基础上增加专用 hooks 或局部组件。
