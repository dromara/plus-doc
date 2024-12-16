# 对接 TOPIAM 单点登录
- - -

# 安装 TOPIAM 应用服务

参考 TOPIAM 官方文档安装 [TOPIAM安装部署](https://eiam.topiam.cn/docs/deployment/)

# 创建 OIDC 应用

![创建 OIDC 应用](https://foruda.gitee.com/images/1734349076820315742/ccc3002d_5601833.png "创建 OIDC 应用")

# 配置 OIDC 应用

![配置 OIDC 应用](https://foruda.gitee.com/images/1734349233857850169/74f96f61_5601833.png "配置 OIDC 应用")

> 登录 Redirect URI 为 ${justauth.address}/social-callback?source=topiam, 例如 http://localhost:80/social-callback?source=topiam

# 配置后端服务

![OIDC 参数信息](https://foruda.gitee.com/images/1734349496777724682/bd775f79_5601833.png "OIDC 参数信息")

找到框架 `application-环境.yml` 配置文件

修改 `topiam` 对应的 `client-id` 与 `client-secret`

```yaml
justauth:
  # 前端外网访问地址
  address: http://localhost:80
  type:
    # topiam 应用配置信息，可在【应用详情】中找到
    topiam:
      # 应用编码
      server-url: http://localhost:1898/api/v1/authorize/nsml9fu7jwlzwkxnrrsrnqesswrq4xua
      # 客户端 ID
      client-id: 61ff33a6092c91bd1813765f8f42b316
      # 客户端秘钥
      client-secret: 397676e2fdb7ca8e57abe364267ffcdc
      # 登录 Redirect URI
      redirect-uri: ${justauth.address}/social-callback?source=topiam
      # 用户信息范围
      scopes: [openid, email, phone, profile]
```
