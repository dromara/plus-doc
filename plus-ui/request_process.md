# 请求流程
- - -

### 交互流程
一个完整的前端UI交互到服务器端处理流程是这样的：  

1. UI 组件交互操作；
2. 调用统一管理的 api service 请求函数；
3. 使用封装的 `request.ts` 发送请求；
4. 获取服务端返回；
5. 更新 data；

为了方便管理维护，统一的请求处理都放在`@/src/api`文件夹中，并且一般按照`model`维度进行拆分文件，如：
```
api/
  system/
    user/
      index.ts
      types.ts
    role/
      index.ts
      types.ts
  monitor/
    operlog/
      index.ts
      types.ts
    logininfor/
      index.ts
      types.ts
  ...
```
> **提示**  
> 其中`@/src/utils/request.ts`是基于 axios 的封装，便于统一处理 `GET`、`POST` 等请求参数、请求头、错误提示和下载能力。  
> 当前项目实际已经封装了：统一 `baseURL`、Token 注入、语言头透传、重复提交拦截、接口加解密、登录过期重定向、二进制下载等逻辑。

### 当前项目默认配置

- 默认 `baseURL` 读取自 `import.meta.env.VITE_APP_BASE_API`
- 默认请求头会附带 `Authorization` 与 `clientid`
- 当前前端项目使用的是 `Vite + TypeScript`，不是旧版 `Vue CLI`
- 本地开发代理默认将 `VITE_APP_BASE_API` 转发到 `http://localhost:8080`
- `RuoYi-Vue-Plus` 与 `RuoYi-Cloud-Plus` 共用这一套请求封装，Cloud 版差异主要在于 `8080` 一般对应网关

### 请求示例
```typescript
// @/api/system/user/index.ts
import request from '@/utils/request';
import { UserQuery, UserVO } from './types';

export const listUser = (query: UserQuery) => {
  return request({
    url: '/system/user/list',
    method: 'get',
    params: query
  });
};

// @/views/system/user/index.vue
import api from '@/api/system/user';
const res = await api.listUser(proxy?.addDateRange(queryParams.value, dateRange.value));
```
> **提示**  
> 如果有不同的`baseURL`，直接通过覆盖的方式，让它具有不同的`baseURL`。
> ```typescript
> export const listUser = (query: UserQuery) => {
>   return request({
>     url: '/system/user/list',
>     method: 'get',
>     params: query,
>     baseURL: import.meta.env.VITE_APP_BASE_API
>   });
> };
> ```

### 常用请求头约定

- `isToken: false`：本次请求不携带登录 Token
- `repeatSubmit: false`：关闭重复提交校验
- `isEncrypt: 'true'`：对当前请求体启用前端加密

### 下载接口说明

项目内统一下载方法位于 `@/src/utils/request.ts` 的 `download` 方法，适合导出 Excel、压缩包等二进制文件。  
如果后端返回的是业务错误而不是文件流，前端会自动转文本解析并提示错误信息。
