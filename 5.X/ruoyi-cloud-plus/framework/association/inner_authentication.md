# 内网鉴权
- - -

## 功能说明

该功能用于防止外部请求直接访问内部服务。

流程：

- 请求经过 `gateway` 时生成 `id-token`
- 后续服务校验 `id-token`
- 未经过网关的请求将出现 `id-token` 无效

## 开启/关闭

修改 `application-common.yml` 中 `sa-token.check-id-token`：

![输入图片说明](https://foruda.gitee.com/images/1678980608778275681/9a2c1054_1766278.png "屏幕截图")

## 放行配置

在 `ruoyi-common-security` 的 `SecurityConfiguration` 中增加排除路径：

![输入图片说明](https://foruda.gitee.com/images/1678980612657326393/cea32a8c_1766278.png "屏幕截图")
