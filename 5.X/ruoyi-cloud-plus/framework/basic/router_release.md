# 网关路由与放行
- - -

## 新增路由

在网关配置中新增 `routers` 配置。

常见位置：
- WebFlux 网关：`script/config/nacos/ruoyi-gateway.yml`
- MVC 网关：`script/config/nacos/ruoyi-gateway-mvc.yml`

根据你实际启用的网关版本修改其中一个即可，不要两个一起生效。

路径格式：`/服务路径/controller路径/接口方法路径`  
`*` 表示任意一级，`**` 表示任意多级。

示例：`resource/**` 将所有以 `resource` 开头的路径路由到 `ruoyi-resource`。

补充说明：
- 路由前缀是给网关识别用的，例如 `Path=/resource/**`
- 大部分服务都配置了 `StripPrefix=1`，所以外部请求 `/resource/oss/list` 转发到资源服务后，服务内部实际接收的是 `/oss/list`
- 也就是说 Controller 一般不需要再写一层 `/resource` 前缀

![输入图片说明](https://foruda.gitee.com/images/1669623462957266512/c282932b_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1669623527799049459/201a52db_1766278.png "屏幕截图")

## 放行配置

在 Nacos 中对应的网关配置文件里配置白名单路径。

路径格式：`/服务路径/controller路径/接口方法路径`  
`*` 表示任意一级，`**` 表示任意多级。

示例：`/resource/sms/code` 代表 `ruoyi-resource` 服务的 `sms` 控制器下 `code` 接口。

补充说明：
- 如果你使用的是 `ruoyi-gateway-mvc`，白名单也要写到 `ruoyi-gateway-mvc.yml`
- Cloud 版接口对外放行通常需要两层同时满足：
  - 服务内部允许匿名访问，例如 `@SaIgnore`
  - 网关白名单允许该路径直接进入服务
- 仅在服务里加 `@SaIgnore`，但没有加网关白名单时，请求通常还是会被网关拦截
- 服务内部接口放行注解的用法与 Vue 版一致，可直接参考 Vue 版“接口放行”

![输入图片说明](https://foruda.gitee.com/images/1660622672461635175/屏幕截图.png "屏幕截图.png")

## 注意事项

放行后接口无需 token 即可访问。  
但无法获取用户信息，也不会进行鉴权。

网关白名单属于真正的对外匿名入口，尽量按具体接口放行，避免直接写过大的 `/**` 范围。

## 建议处理

- 移除接口上的鉴权注解
- 移除接口内获取用户信息的逻辑
- 若实体类自动注入 `createBy` / `updateBy`，需避免依赖用户信息
