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

OSS 文件和代码生成 zip 下载使用 `src/plugins/download.ts`，详见 [通用方法](/6.X/plus-ui/common_func.md)。
