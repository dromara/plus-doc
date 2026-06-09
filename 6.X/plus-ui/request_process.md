# 请求流程
- - -

前端请求统一由 `src/utils/request.ts` 封装，业务接口集中放在 `src/api`。

## 调用链路

1. 页面调用 `src/api/**/index.ts` 中的接口函数。
2. 接口函数调用 `src/utils/request.ts` 导出的 axios 实例。
3. 请求拦截器注入 Token、客户端 ID、语言头，并处理 GET 参数、重复提交和加密。
4. 响应拦截器处理业务状态码、登录过期、解密和错误提示。
5. 页面只处理业务数据和业务分支。

## API 目录

```text
src/api/
  system/
    config/
      index.ts
      types.ts
    user/
      index.ts
      types.ts
  workflow/
    task/
      index.ts
      types.ts
```

`index.ts` 写接口函数，`types.ts` 写 `VO`、`Query`、`Form` 类型。

## 开发建议

- 新增业务接口时，建议按模块新建 `src/api/业务模块/功能/index.ts` 与 `types.ts`。
- `VO` 表示后端返回对象，`Query` 表示查询参数，`Form` 表示新增/修改表单。
- 接口路径只写后端业务路径，不要拼接 `VITE_APP_BASE_API`，代理前缀由 request 实例统一处理。
- 列表接口统一返回 `PageResult<T>`，页面只关心 `rows` 与 `total`。
- 新增、修改、删除接口建议保持后端 REST 风格，便于代码生成和权限配置统一。

## 新增一个业务 API 示例

以“客户管理”为例，推荐按下面结构新增接口文件：

```text
src/api/crm/customer/
  index.ts
  types.ts
```

`types.ts`：

```typescript
export interface CustomerVO {
  customerId: string | number;
  customerName: string;
  mobile?: string;
  status?: string;
  createTime?: string;
}

export interface CustomerQuery extends PageQuery {
  customerName?: string;
  mobile?: string;
  status?: string;
}

export interface CustomerForm {
  customerId?: string | number;
  customerName: string;
  mobile?: string;
  status?: string;
}
```

`index.ts`：

```typescript
import type { PageResult } from '@/api/types';
import type { AxiosPromise } from '@/utils/api-types';
import request from '@/utils/request';
import type { CustomerForm, CustomerQuery, CustomerVO } from './types';

export function listCustomer(query: CustomerQuery): AxiosPromise<PageResult<CustomerVO>> {
  return request({
    url: '/crm/customer/list',
    method: 'get',
    params: query
  });
}

export function getCustomer(customerId: string | number): AxiosPromise<CustomerVO> {
  return request({
    url: `/crm/customer/${customerId}`,
    method: 'get'
  });
}

export function addCustomer(data: CustomerForm) {
  return request({
    url: '/crm/customer',
    method: 'post',
    data
  });
}

export function updateCustomer(data: CustomerForm) {
  return request({
    url: '/crm/customer',
    method: 'put',
    data
  });
}

export function delCustomer(customerId: string | number | Array<string | number>) {
  return request({
    url: `/crm/customer/${customerId}`,
    method: 'delete'
  });
}
```

页面中使用：

```typescript
import { listCustomer, delCustomer } from '@/api/crm/customer';
import type { CustomerQuery, CustomerVO } from '@/api/crm/customer/types';

const customerList = ref<CustomerVO[]>([]);
const total = ref(0);
const queryParams = ref<CustomerQuery>({
  pageNum: 1,
  pageSize: 10,
  customerName: '',
  mobile: '',
  status: ''
});

const getList = async () => {
  const res = await listCustomer(queryParams.value);
  customerList.value = res.data?.rows ?? [];
  total.value = res.data?.total ?? 0;
};

const handleDelete = async (row: CustomerVO) => {
  await proxy?.$modal.confirm(`是否确认删除客户「${row.customerName}」？`);
  await delCustomer(row.customerId);
  proxy?.$modal.msgSuccess('删除成功');
  await getList();
};
```

## 类型约定

通用响应类型位于 `src/utils/api-types.ts`：

```typescript
export interface RuoYiAjaxResult<T = unknown> {
  code?: number;
  msg?: string;
  data?: T;
}

export type AxiosPromise<T = unknown> = Promise<RuoYiAjaxResult<T>>;
```

分页返回类型位于 `src/api/types.ts`：

```typescript
export interface PageResult<T = any> {
  total: number;
  rows: T[];
}
```

分页接口示例：

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

详情接口示例：

```typescript
import type { AxiosPromise } from '@/utils/api-types';
import request from '@/utils/request';
import type { ConfigVO } from './types';

export function getConfig(configId: string | number): AxiosPromise<ConfigVO> {
  return request({
    url: '/system/config/' + configId,
    method: 'get'
  });
}
```

新增、修改、删除示例：

```typescript
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

## 页面使用

当前列表页推荐搭配通用 hooks：

```typescript
import { listConfig } from '@/api/system/config';
import type { ConfigQuery, ConfigVO } from '@/api/system/config/types';
import { useLoading } from '@/hooks/async/useLoading';
import { useDateRangeQuery } from '@/hooks/form/useDateRangeQuery';

const configList = ref<ConfigVO[]>([]);
const total = ref(0);
const { loading, withLoading } = useLoading(true);
const { dateRange, applyDateRange } = useDateRangeQuery();

const queryParams = ref<ConfigQuery>({
  pageNum: 1,
  pageSize: 10,
  configName: '',
  configKey: '',
  configType: ''
});

const getList = async () => {
  await withLoading(async () => {
    const res = await listConfig(applyDateRange(queryParams.value));
    configList.value = res.data?.rows ?? [];
    total.value = res.data?.total ?? 0;
  });
};
```

## 请求头与环境变量

`.env.*` 中与请求流程相关的常用配置：

| 配置 | 说明 |
| --- | --- |
| `VITE_APP_BASE_API` | axios 基础代理前缀 |
| `VITE_APP_CLIENT_ID` | 客户端 ID，请求头会携带 |
| `VITE_APP_ENCRYPT` | 接口加密总开关，需与后端保持一致 |
| `VITE_APP_RSA_PUBLIC_KEY` | 请求体加密使用的 RSA 公钥 |
| `VITE_APP_RSA_PRIVATE_KEY` | 响应体解密使用的 RSA 私钥 |

`src/utils/request.ts` 中的 `globalHeaders()` 会统一生成 Token、客户端、语言等公共请求头，富文本/文件上传等非 axios 场景也复用该方法。

## 请求头开关

| Header | 说明 |
| --- | --- |
| `isToken: false` | 本次请求不携带 Token |
| `repeatSubmit: false` | 关闭 POST/PUT 重复提交拦截 |
| `isEncrypt: 'true'` | 开启 POST/PUT 请求体加密 |

示例：

```typescript
request({
  url: '/auth/code',
  method: 'get',
  headers: {
    isToken: false
  }
});
```

加密请求示例：

```typescript
request({
  url: '/system/user/resetPwd',
  method: 'put',
  headers: {
    isEncrypt: 'true',
    repeatSubmit: false
  },
  data
});
```

## 加密接口完整写法

后端接口如果标注了 `@ApiEncrypt`，前端对应请求需要开启加密头。示例：

```typescript
export function resetUserPwd(userId: string | number, password: string) {
  return request({
    url: '/system/user/resetPwd',
    method: 'put',
    headers: {
      isEncrypt: 'true',
      repeatSubmit: false
    },
    data: {
      userId,
      password
    }
  });
}
```

使用时无需手动 AES/RSA 加密，`src/utils/request.ts` 会根据 `isEncrypt` 与 `VITE_APP_ENCRYPT` 自动处理。

## 下载

普通导出使用 `src/utils/request.ts` 中的 `download`：

```typescript
import { download as requestDownload } from '@/utils/request';

requestDownload(
  'system/config/export',
  { ...queryParams.value },
  `config_${new Date().getTime()}.xlsx`
);
```

## 常见问题

| 现象 | 排查方向 |
| --- | --- |
| 请求 404 | 检查接口路径、后端 Controller 前缀、开发代理 `VITE_APP_BASE_API` |
| 请求 401 / 登录过期 | 检查 Token 是否存在、后端 Sa-Token 配置、客户端 ID 是否匹配 |
| POST/PUT 请求失败 | 如果接口使用 `@ApiEncrypt`，确认前端请求头 `isEncrypt` 与环境变量开关一致 |
| 文件下载为空 | 确认接口返回的是文件流，并使用 `download` 或 `src/plugins/download.ts` 的下载方法 |
| 国际化语言不生效 | 检查请求头中的语言值和前后端语言资源后缀是否一致 |

OSS 文件和代码生成 zip 下载使用 `src/plugins/download.ts`，详见 [通用方法](/6.X/plus-ui/common_func.md)。
