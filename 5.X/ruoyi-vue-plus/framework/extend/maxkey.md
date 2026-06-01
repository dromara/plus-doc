# 对接 MaxKey 单点登录
- - -

## 1. 安装 MaxKey

参考官方文档安装：

- https://www.maxkey.top/doc/docs/overview/intro

## 2. 配置 OAuth2 应用

在 MaxKey 中创建 OAuth2 应用并获取 `client-id` 与 `client-secret`。

![输入图片说明](https://foruda.gitee.com/images/1693377802128677240/0927270a_1766278.png "屏幕截图")

补充说明：

- 回调地址通常配置为 `前端域名/social-callback?source=maxkey`。
- 如果前端部署在子路径下，需要把真实访问前缀一并带上。

## 3. 配置后端

在 `application-环境.yml` 中配置 MaxKey：

- `client-id`
- `client-secret`

![输入图片说明](https://foruda.gitee.com/images/1693378118762354596/2f02c8a3_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1693378168538263792/24476d2a_1766278.png "屏幕截图")

补充说明：

- Vue 版本的第三方登录配置位于各环境配置文件中的 `justauth.type.maxkey` 节点。
- `justauth.address` 要配置成前端对外访问地址，否则第三方登录回调通常会跳错地址。
- 前端登录页走的是统一社交登录回调页，不需要为 MaxKey 单独再写一套前端协议处理逻辑。
