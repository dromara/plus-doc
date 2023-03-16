# 内网鉴权
- - -
## 功能介绍

此功能用于防止外部请求访问内部服务应用<br>
在请求经过 `gateway网关` 会生成一个 `id-token` 携带到后续服务进行校验<br>
若未经过 `gateway网关` 调用内网服务 会出现 `id-token无效` 异常<br>
有效防止非法请求直接访问内网服务<br>

## 开启/关闭内网鉴权

更改 `application-common.yml` 配置文件的 `sa-token.check-id-token` 配置即可

![输入图片说明](https://images.gitee.com/uploads/images/2022/0615/163056_fe02a430_1766278.png "屏幕截图.png")

## 放行内网鉴权
进入 `ruoyi-common-security` 模块找到 `SecurityConfiguration` 类 增加排除路径即可

![输入图片说明](https://images.gitee.com/uploads/images/2022/0615/163400_fccb0f63_1766278.png "屏幕截图.png")
