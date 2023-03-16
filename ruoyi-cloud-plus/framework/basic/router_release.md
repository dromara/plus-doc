# 网关路由与放行
- - -

## 新增路由
`ruoyi-gateway.yml` 配置文件 增加 `routers` 配置<br>
**注意: 路径格式为 `/服务路径/controller路径/接口方法路径` `*代表任意一级 **代表任意所有级`**<br>
下图代表 `resource/**` 将所有 `resource开头的路径` 都路由到 `ruoyi-resource` 服务<br>
例如: `/resource/sms/code` `resource路由到ruoyi-resource服务` `sms路由到对应的contrller` `code 路由到对应的接口`<br>
![输入图片说明](https://foruda.gitee.com/images/1669623462957266512/c282932b_1766278.png "屏幕截图")<br>
![输入图片说明](https://foruda.gitee.com/images/1669623527799049459/201a52db_1766278.png "屏幕截图")

## 放行使用方式
nacos 中 `ruoyi-gateway.yml` 白名单放行<br>
**注意: 放行路径格式为 `/服务路径/controller路径/接口方法路径` `*代表任意一级 **代表任意所有级`**<br>
示例: `/resource/sms/code` 代表 `ruoyi-resource服务 sms的controller code接口`<br>
![输入图片说明](https://foruda.gitee.com/images/1660622672461635175/屏幕截图.png "屏幕截图.png")