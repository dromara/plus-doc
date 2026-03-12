# 对接 TOPIAM 单点登录
- - -

## 1. 安装 TOPIAM

参考官方文档：

- https://eiam.topiam.cn/docs/deployment/

## 2. 创建 OIDC 应用

![创建 OIDC 应用](https://foruda.gitee.com/images/1734349076820315742/ccc3002d_5601833.png "创建 OIDC 应用")

## 3. 配置 OIDC 应用

![配置 OIDC 应用](https://foruda.gitee.com/images/1734349233857850169/74f96f61_5601833.png "配置 OIDC 应用")

登录 Redirect URI：

`{justauth.address}/social-callback?source=topiam`

示例：`http://localhost:80/social-callback?source=topiam`

## 4. 配置后端

获取 OIDC 参数信息：

![OIDC 参数信息](https://foruda.gitee.com/images/1734349496777724682/bd775f79_5601833.png "OIDC 参数信息")

在 `application-环境.yml` 中配置：

```yaml
justauth:
  address: http://localhost:80
  type:
    topiam:
      server-url: http://localhost:1898/api/v1/authorize/nsml9fu7jwlzwkxnrrsrnqesswrq4xua
      client-id: 61ff33a6092c91bd1813765f8f42b316
      client-secret: 397676e2fdb7ca8e57abe364267ffcdc
      redirect-uri: ${justauth.address}/social-callback?source=topiam
      scopes: [openid, email, phone, profile]
```
