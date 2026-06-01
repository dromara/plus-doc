# 通用方法
- - -

前端通用能力主要放在 `src/plugins` 与 `src/utils`。页面里优先使用显式 `import`，这样类型更清晰，也更方便重构。

当前仍会在 `src/plugins/index.ts` 挂载 `$tab`、`$modal`、`$cache`、`$download`、`$auth` 到 `app.config.globalProperties`，但组合式页面建议直接导入对应模块。

## 页签操作

源码位置：`src/plugins/tab.ts`

```typescript
import tab from '@/plugins/tab';

// 打开页签
await tab.openPage('/system/user');

// 打开页签并传入标题和 query
await tab.openPage('/system/user', '用户管理', { deptId: 100 });

// 刷新当前页签
await tab.refreshPage();

// 关闭当前页签
await tab.closePage();

// 关闭所有页签
await tab.closeAllPage();
```

常用方法：

| 方法 | 说明 |
| --- | --- |
| `openPage(url, title?, query?)` | 跳转到指定路由 |
| `refreshPage(route?)` | 刷新当前或指定页签 |
| `closePage(route?)` | 关闭当前或指定页签 |
| `closeOpenPage(route)` | 关闭当前页签并打开新路由 |
| `closeAllPage()` | 关闭所有页签 |
| `closeLeftPage(route?)` | 关闭左侧页签 |
| `closeRightPage(route?)` | 关闭右侧页签 |
| `closeOtherPage(route?)` | 关闭其他页签 |
| `updatePage(route)` | 更新已访问页签 |

## 消息与弹窗

源码位置：`src/plugins/modal.ts`

```typescript
import modal from '@/plugins/modal';

modal.msg('默认提示');
modal.msgSuccess('操作成功');
modal.msgWarning('请检查输入');
modal.msgError('操作失败');

await modal.confirm('确认删除当前数据？');
modal.loading('正在处理，请稍候...');
modal.closeLoading();
```

页面提交示例：

```typescript
const submitForm = () => {
  formRef.value?.validate(async (valid: boolean) => {
    if (!valid) return;
    await addConfig(form.value);
    modal.msgSuccess('操作成功');
    closeDialog();
    await getList();
  });
};
```

## 权限判断

源码位置：`src/plugins/auth.ts`

```typescript
import auth from '@/plugins/auth';

auth.hasPermi('system:user:add');
auth.hasPermiOr(['system:user:add', 'system:user:edit']);
auth.hasPermiAnd(['system:user:add', 'system:user:edit']);

auth.hasRole('admin');
auth.hasRoleOr(['admin', 'common']);
auth.hasRoleAnd(['admin', 'common']);
```

模板显隐优先使用权限指令，复杂插槽或延迟渲染组件再使用 `checkPermi`、`checkRole`。详见 [权限使用](/6.X/plus-ui/permissions_use.md)。

## 缓存

源码位置：`src/plugins/cache.ts`

```typescript
import cache from '@/plugins/cache';

cache.local.set('key', 'local value');
cache.local.get('key');
cache.local.setJSON('jsonKey', { value: 1 });
cache.local.getJSON('jsonKey');
cache.local.remove('key');

cache.session.set('key', 'session value');
cache.session.get('key');
cache.session.setJSON('jsonKey', { value: 1 });
cache.session.getJSON('jsonKey');
cache.session.remove('key');
```

## 文件下载

OSS 与代码生成 zip 下载在 `src/plugins/download.ts`：

```typescript
import download from '@/plugins/download';

await download.oss(ossId);
await download.zip('/tool/gen/batchGenCode?tables=' + tableNames, 'ruoyi.zip');
```

普通业务导出使用 `src/utils/request.ts` 中的 `download`：

```typescript
import { download as requestDownload } from '@/utils/request';

requestDownload(
  'system/config/export',
  { ...queryParams.value },
  `config_${new Date().getTime()}.xlsx`
);
```

## 常用工具

`src/utils/ruoyi.ts` 提供常用工具函数：

```typescript
import { addDateRange, parseTime, parseStrEmpty, tansParams } from '@/utils/ruoyi';
```

常见用法：

```typescript
parseTime(row.createTime);
parseStrEmpty(userId);
addDateRange(queryParams.value, dateRange.value);
```
