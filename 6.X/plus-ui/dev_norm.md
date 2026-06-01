# 开发规范
- - -

新页面尽量贴近现有 `src/views/system/config/index.vue`、`src/views/system/user/index.vue` 的组织方式：typed API、组合式 hooks、显式导入插件对象、页面内聚样式。

## 页面目录

业务页面放在 `src/views` 下，一个菜单页面对应一个目录或一个 `.vue` 文件。

```text
src/views/
  system/
    config/
      index.vue
    user/
      index.vue
      components/
        DeptTree.vue
```

建议：

- 页面组件使用 `<script setup name="Config" lang="ts">`
- `name` 与路由 `name` 保持一致
- 页面专属组件放到当前业务目录的 `components`
- 页面专属工具放到当前业务目录的 `utils` 或 `hooks`
- 可跨模块复用的能力再放入 `src/components`、`src/hooks`、`src/utils`

## API 目录

接口放在 `src/api/模块/index.ts`，类型放在同级 `types.ts`。

```text
src/api/system/config/
  index.ts
  types.ts
```

接口函数示例：

```typescript
import type { PageResult } from '@/api/types';
import type { AxiosPromise } from '@/utils/api-types';
import request from '@/utils/request';
import type { ConfigQuery, ConfigVO } from './types';

export function listConfig(query: ConfigQuery): AxiosPromise<PageResult<ConfigVO>> {
  return request({
    url: '/system/config/list',
    method: 'get',
    params: query
  });
}
```

类型命名建议：

| 后缀 | 用途 |
| --- | --- |
| `VO` | 后端返回对象 |
| `Query` | 查询参数 |
| `Form` | 表单提交对象 |

## 列表页结构

列表页建议统一保留这些命名，方便生成代码和人工维护：

```typescript
const list = ref<ConfigVO[]>([]);
const total = ref(0);
const queryFormRef = ref<ElFormInstance>();
const formRef = ref<ElFormInstance>();

const data = reactive<PageData<ConfigForm, ConfigQuery>>({
  form: { ...initFormData },
  queryParams: {
    pageNum: 1,
    pageSize: 10
  },
  rules: {}
});

const { queryParams, form, rules } = toRefs(data);
```

常用 hooks：

```typescript
const { loading, withLoading } = useLoading(true);
const { showSearch } = useSearchToggle();
const { dateRange, applyDateRange, resetDateRange } = useDateRangeQuery();
const { ids, single, multiple, handleSelectionChange } = useTableSelection<ConfigVO>(item => item.configId);
```

查询方法：

```typescript
const getList = async () => {
  await withLoading(async () => {
    const res = await listConfig(applyDateRange(queryParams.value));
    list.value = res.data?.rows ?? [];
    total.value = res.data?.total ?? 0;
  });
};
```

## 插件和工具

组合式页面中优先显式导入：

```typescript
import modal from '@/plugins/modal';
import auth from '@/plugins/auth';
import tab from '@/plugins/tab';
import { useDict } from '@/utils/dict';
import { download as requestDownload } from '@/utils/request';
import { parseTime } from '@/utils/ruoyi';
```

不要继续新增依赖 `proxy` 的写法。

## 样式

页面样式优先使用当前项目已有的页面 mixin：

```vue
<style lang="scss" scoped>
@use '@/assets/styles/components/page-shell' as pageShell;

@include pageShell.table-crud-page;
</style>
```

说明：

- 普通页面样式放在当前 `.vue` 文件中
- 通用页面结构抽到 `src/assets/styles/components`
- 覆盖第三方组件内部结构时使用局部 `:deep()`
- 不要把业务页面样式直接写成全局覆盖

## 组件

通用组件放在 `src/components`，业务组件放在当前业务目录。

当前项目会自动导入大量 Element Plus 组件和图标，但业务组件是否可直接使用取决于项目配置。写业务页面时，优先参考现有页面的导入方式。
