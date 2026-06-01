# 使用参数
- - -

系统参数通过 `src/api/system/config` 读取或修改，页面中直接导入接口函数。

## 读取参数

```typescript
import { getConfigKey } from '@/api/system/config';

const res = await getConfigKey('sys.account.registerUser');
const value = res.data;
```

`res.data` 是 `sys_config.config_key` 对应的 `config_value`，通常为字符串。需要布尔值、数字或对象时，在前端业务里自行转换。

```typescript
const enabled = res.data === 'true';
const maxCount = Number(res.data ?? 0);
```

## 修改参数

当前 API 提供按主键修改和按 key 修改两种方式。

```typescript
import { updateConfig, updateConfigByKey } from '@/api/system/config';

await updateConfig(form.value);
await updateConfigByKey('sys.index.skinName', 'skin-blue');
```

## 刷新缓存

后台参数缓存刷新接口：

```typescript
import { refreshCache } from '@/api/system/config';
import modal from '@/plugins/modal';

await refreshCache();
modal.msgSuccess('刷新缓存成功');
```

参数不适合在高频渲染函数里反复请求，通常在页面初始化或明确操作后读取一次。
