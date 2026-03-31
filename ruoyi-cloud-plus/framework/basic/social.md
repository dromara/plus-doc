# 第三方授权功能
- - -

## 版本

- 2.X

## 前置说明

- 功能基于 `JustAuth`
- 示例以 `Gitee` 授权为例
- 其他平台配置请参考 [JustAuth 官方文档](https://www.justauth.cn/guide/)

![输入图片说明](https://foruda.gitee.com/images/1690937097426867003/91d80587_4959041.png "屏幕截图")

## 配置流程

### 1. 申请第三方应用

![输入图片说明](https://foruda.gitee.com/images/1700641775779304627/1cf1b56f_1766278.png "屏幕截图")

### 2. 修改后端配置

Cloud 版本通常在 Nacos 的 `ruoyi-auth.yml` 中配置 AppId/Secret 与回调地址。

`justauth.address` 需要填写前端对外可访问地址，回调地址会拼成 `${justauth.address}/social-callback?source=xxx`。

![输入图片说明](https://foruda.gitee.com/images/1690936741844431943/580f8998_4959041.png "屏幕截图")

**注意：内网地址无法回调，请使用公网可访问地址。**

![输入图片说明](https://foruda.gitee.com/images/1690940457570856867/ce22df18_4959041.png "屏幕截图")

### 3. 修改前端配置

编辑 `login.vue` 中的第三方登录入口配置。

如果使用默认 `plus-ui`，前端已经内置 `/social-callback` 路由与回调页面，主要确认图标入口和后端平台配置一致即可。

![输入图片说明](https://foruda.gitee.com/images/1690937306197173754/5c1ece29_4959041.png "屏幕截图")

## 授权登录（未绑定第三方平台）

1. 个人中心发起授权

![输入图片说明](https://foruda.gitee.com/images/1690938449386201097/ea375106_4959041.png "屏幕截图")

2. 同意授权并完成绑定

![输入图片说明](https://foruda.gitee.com/images/1690938522418523183/81b327bf_4959041.png "屏幕截图")

授权成功后会跳转系统首页：

![输入图片说明](https://foruda.gitee.com/images/1690938559178527841/563168e4_4959041.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1690938636375977741/8ceb77cf_4959041.png "屏幕截图")

在第三方应用可看到授权用户信息：

![输入图片说明](https://foruda.gitee.com/images/1690938725512311321/5532a2a9_4959041.png "屏幕截图")

## 授权登录（已绑定第三方平台）

1. 登录页点击第三方图标

![输入图片说明](https://foruda.gitee.com/images/1690938908352243992/fd044381_4959041.png "屏幕截图")

2. 同意授权

![输入图片说明](https://foruda.gitee.com/images/1690938522418523183/81b327bf_4959041.png "屏幕截图")

## 解除授权绑定

1. 个人中心点击解绑

![输入图片说明](https://foruda.gitee.com/images/1690939087877969002/4ef324e7_4959041.png "屏幕截图")

2. 确认解绑

![输入图片说明](https://foruda.gitee.com/images/1690939108017661775/7236088d_4959041.png "屏幕截图")
