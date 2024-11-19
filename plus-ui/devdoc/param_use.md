# 使用参数

- - -

参数设置是提供开发人员、实施人员的动态系统配置参数，不需要去频繁修改后台配置文件，也无需重启服务器即可生效。

1. 使用参数

```typescript
// 导入 api
import {getConfigKey} from '@/api/system/config';

const res = getConfigKey('参数键名');
```

res.data 即为数据库中 sys_config 表中 config_key 对应的 config_value 的值