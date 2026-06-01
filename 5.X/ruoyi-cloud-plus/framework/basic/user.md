# 系统用户相关
- - -

## 功能概览

- 基于 `Sa-Token` 实现认证与权限控制
- 框架对 Sa-Token API 做了业务封装
- 登录数据来源不限制，只需构建 `LoginUser`

## 登录与 Token

完成登录后会返回 token，前端需在请求头携带：

`Authorization: Bearer token`

前端项目默认还会同时携带：

`clientid: 前端配置的客户端ID`

补充说明：
- Cloud 与 Vue 使用的是同一套 `LoginHelper` 思路，日常取用户信息、判断超管/租户管理员的写法一致
- 前端 `clientid` 需要和认证中心的客户端配置保持一致，否则网关或服务侧会判定 token 与客户端不匹配
- 如果是 `plus-ui` 默认工程，请同步检查 `VITE_APP_CLIENT_ID`

后端获取当前登录用户：

```java
LoginUser user = LoginHelper.getLoginUser();
```

基于 token 获取用户信息：

```java
LoginUser user = LoginHelper.getLoginUser(token);
```

## 常用 API

```java
// 获取登录用户 ID
Long userId = LoginHelper.getUserId();

// 获取登录用户账号
String username = LoginHelper.getUsername();

// 获取登录用户租户 ID
String tenantId = LoginHelper.getTenantId();

// 获取登录用户部门 ID
Long deptId = LoginHelper.getDeptId();

// 获取登录用户类型
UserType userType = LoginHelper.getUserType();
```

## 扩展属性

获取扩展属性：

```java
Object obj = LoginHelper.getExtra(key);
```

设置扩展属性示例（如登录时设置 `clientId`）：

![输入图片说明](https://foruda.gitee.com/images/1699591164562734430/42730add_1766278.png "屏幕截图")

框架默认已经把常见登录上下文写入 token 扩展信息，例如 `tenantId`、`userId`、`userName`、`deptId`、`deptName`、`deptCategory`、`clientid`。

## 权限判断

是否为超级管理员：

```java
boolean b = LoginHelper.isSuperAdmin();
boolean b = LoginHelper.isSuperAdmin(userId);
```

是否为租户管理员：

```java
boolean b = LoginHelper.isTenantAdmin();
// 示例：基于角色组判断
boolean b = LoginHelper.isSuperAdmin(rolePermission);
```

## 参考文档

更多登录认证相关能力请参考：[Sa-Token 官方文档 - 登录认证](https://sa-token.cc/doc.html#/use/login-auth)
