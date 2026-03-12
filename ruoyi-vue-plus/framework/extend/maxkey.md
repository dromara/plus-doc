# 对接 MaxKey 单点登录
- - -

## 1. 安装 MaxKey

参考官方文档安装：

- https://www.maxkey.top/doc/docs/overview/intro

## 2. 配置 OAuth2 应用

在 MaxKey 中创建 OAuth2 应用并获取 `client-id` 与 `client-secret`。

![输入图片说明](https://foruda.gitee.com/images/1693377802128677240/0927270a_1766278.png "屏幕截图")

## 3. 配置后端

在 `application-环境.yml` 中配置 MaxKey：

- `client-id`
- `client-secret`

![输入图片说明](https://foruda.gitee.com/images/1693378118762354596/2f02c8a3_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1693378168538263792/24476d2a_1766278.png "屏幕截图")
