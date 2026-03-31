# 对接 MaxKey 单点登录
- - -

## 1. 安装 MaxKey

参考官方文档：

- https://www.maxkey.top/doc/docs/overview/intro

## 2. 配置 OAuth2 应用

在 MaxKey 中创建 OAuth2 应用并获取 `client-id` 与 `client-secret`。

![输入图片说明](https://foruda.gitee.com/images/1693377802128677240/0927270a_1766278.png "屏幕截图")

补充说明：

- 回调地址需要和前端访问地址保持一致，通常为 `前端域名/social-callback?source=maxkey`。
- 如果部署时前端不是根路径，还要把实际访问前缀一起带上。

## 3. 配置后端

在 Nacos 的 `ruoyi-auth.yml` 中配置：

- `client-id`
- `client-secret`

![输入图片说明](https://foruda.gitee.com/images/1693378118762354596/2f02c8a3_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1693378168538263792/24476d2a_1766278.png "屏幕截图")

补充说明：

- Cloud 版本的第三方登录配置统一维护在 `script/config/nacos/ruoyi-auth.yml` 的 `justauth.type.maxkey` 节点。
- 其中 `justauth.address` 表示前端对外访问地址，生产环境必须改成真实域名。
- 前端页面本身无需额外单独适配 MaxKey 协议，只要后端 JustAuth 配置正确即可走统一的社交登录回调流程。
- 如果功能和 Vue 版本一致的地方，可直接参考 [Vue 版本 MaxKey 对接说明](/ruoyi-vue-plus/framework/extend/maxkey.md)。
