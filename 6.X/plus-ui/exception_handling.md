# 异常处理
- - -

前端异常处理集中在 `src/utils/request.ts`，不建议在每个页面单独处理通用 HTTP 异常。

## 处理范围

当前请求封装会统一处理：

- 网络连接异常
- 请求超时
- HTTP 状态异常
- 后端业务状态码
- 登录态过期
- 加密响应解密失败
- Blob 错误响应解析
- 下载失败提示

## 错误消息解析

`extractErrorMessage` 会优先解析响应体：

```typescript
export async function extractErrorMessage(error: any): Promise<string | undefined>
```

支持：

- JSON 响应中的 `code`
- JSON 响应中的 `msg`
- JSON 响应中的 `message`
- Blob / ArrayBuffer 中的错误文本
- Axios 原始错误消息

## 登录过期

当后端返回 `401` 时，前端会弹出确认框。用户确认后执行：

```typescript
useUserStore().logout()
router.replace({
  path: '/login',
  query: {
    redirect: encodeURIComponent(router.currentRoute.value.fullPath || '/')
  }
});
```

## 业务状态码

状态码枚举位于：

```text
src/enums/RespEnum.ts
```

错误码文案位于：

```text
src/utils/errorCode.ts
```

如果后端新增业务状态码，需要同步维护前端错误码映射。

## 页面级处理建议

通用错误交给 `request.ts`。页面只处理业务分支：

```typescript
try {
  await submitForm(data);
  modal.msgSuccess('保存成功');
} finally {
  setLoading(false);
}
```

需要静默处理的接口，可以在业务层捕获并自行决定是否提示。

## 下载异常

下载使用：

```typescript
import { download as requestDownload } from '@/utils/request';

requestDownload(url, params, fileName);
```

下载响应如果不是合法 Blob 文件，前端会读取响应文本并按业务错误提示。
