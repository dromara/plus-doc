# 使用参数

- - -

参数设置是提供开发人员、实施人员的动态系统配置参数，不需要去频繁修改后台配置文件，也无需重启服务器即可生效。

1. 使用参数

```typescript
// 导入 api
import {getConfigKey} from '@/api/system/config';

const res = await getConfigKey('参数键名');
```

`res.data` 即为数据库中 `sys_config` 表里 `config_key` 对应的 `config_value`。

也可以通过全局方法使用：

```typescript
const value = await proxy?.getConfigKey('sys.account.registerUser');
```

补充说明：
- 这个接口返回的一般是字符串值，前端需要按业务自行转换成 `boolean`、`number` 或其他类型
- 不建议在高频渲染函数里反复请求参数，通常在页面初始化时读取一次即可
- 如果后台刚修改了参数但前端未生效，先确认后端是否已刷新参数缓存
