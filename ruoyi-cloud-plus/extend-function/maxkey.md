# 对接 MaxKey 单点登录
- - -

# 安装 MaxKey 应用服务

参考 MaxKey 官方文档安装 [MaxKey安装部署](https://www.maxkey.top/doc/docs/overview/intro)

# 配置应用 OAuth2.0 认证注册

![输入图片说明](https://foruda.gitee.com/images/1693377802128677240/0927270a_1766278.png "屏幕截图")

# 配置后端服务

找到 `Nacos` 内的 `ruoyi-auth.yml` 配置文件

修改 `maxkey` 对应的 `client-id` 与 `client-secret`

![输入图片说明](https://foruda.gitee.com/images/1693378118762354596/2f02c8a3_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1693378168538263792/24476d2a_1766278.png "屏幕截图")