# 网关路由与放行
- - -

## 新增路由

在 `ruoyi-gateway.yml` 中新增 `routers` 配置。

路径格式：`/服务路径/controller路径/接口方法路径`  
`*` 表示任意一级，`**` 表示任意多级。

示例：`resource/**` 将所有以 `resource` 开头的路径路由到 `ruoyi-resource`。

![输入图片说明](https://foruda.gitee.com/images/1669623462957266512/c282932b_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1669623527799049459/201a52db_1766278.png "屏幕截图")

## 放行配置

在 Nacos 中的 `ruoyi-gateway.yml` 配置白名单路径。

路径格式：`/服务路径/controller路径/接口方法路径`  
`*` 表示任意一级，`**` 表示任意多级。

示例：`/resource/sms/code` 代表 `ruoyi-resource` 服务的 `sms` 控制器下 `code` 接口。

![输入图片说明](https://foruda.gitee.com/images/1660622672461635175/屏幕截图.png "屏幕截图.png")

## 注意事项

放行后接口无需 token 即可访问。  
但无法获取用户信息，也不会进行鉴权。

## 建议处理

- 移除接口上的鉴权注解
- 移除接口内获取用户信息的逻辑
- 若实体类自动注入 `createBy` / `updateBy`，需避免依赖用户信息
