# 创建新服务
- - -

## 快速方式

复制已有服务（如 `ruoyi-system`）作为模板。

补充说明：

- Cloud 版本新增的是“微服务”时才建议走本页流程；如果只是普通业务扩展，优先评估是否直接放到现有服务中，避免过早拆分。
- 新服务通常可以参考 `ruoyi-system`、`ruoyi-gen` 或 `ruoyi-example/ruoyi-demo` 的结构。

## 必要改动

1. 修改 `pom` 名称

![输入图片说明](https://foruda.gitee.com/images/1678980168782983123/c717e9ba_1766278.png "屏幕截图")

2. 修改启动类名称

![输入图片说明](https://foruda.gitee.com/images/1678980179829877203/f89d5c18_1766278.png "屏幕截图")

3. 修改 `application.yml` 服务名

![输入图片说明](https://foruda.gitee.com/images/1678980184047648028/e4c6c6cc_1766278.png "屏幕截图")

4. 在 Nacos 新增对应服务配置

![输入图片说明](https://foruda.gitee.com/images/1678980188806372269/cfd9731a_1766278.png "屏幕截图")

5. 在 `ruoyi-gateway.yml` 增加路由

新服务访问路径：

`网关ip:端口/服务路径/controller路径/接口路径`

示例：`http://localhost:8080/system/user/list`

![输入图片说明](https://foruda.gitee.com/images/1666861595048863422/9e9755b3_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1666861629037264535/bdfd5484_1766278.png "屏幕截图")

补充说明：

1. 除了当前服务自己的 `pom` 外，通常还需要把新服务加入父工程模块列表。
2. `spring.application.name` 要和 Nacos 中的配置、注册中心服务名、网关路由保持一致。
3. 网关路由要同时检查 `ruoyi-gateway.yml` 和 `ruoyi-gateway-mvc.yml` 两份配置，按你实际使用的网关实现进行同步。
4. 新服务的对外访问路径最终是 `网关前缀 + 服务路由前缀 + Controller 路径`，前端接口地址也要跟着同步。
5. 如果服务间需要远程调用，再补充对应的 Dubbo 暴露与引用配置。

## 注意事项

- 不同包名的模块需同步修改配置

![输入图片说明](https://foruda.gitee.com/images/1719813861680271619/82435586_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1692006501957936219/059f8526_1766278.png "屏幕截图")

- 如需使用 `Seata` 分布式事务，请在 `seata-server.properties` 中增加服务组

![输入图片说明](https://foruda.gitee.com/images/1692006825427360840/5b9e410c_1766278.png "屏幕截图")
