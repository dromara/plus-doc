# IntelliJ IDEA 环境配置
- - -

## 配置建议

- 建议使用官方推荐的 IDEA 版本（见项目初始化页）
- 推荐统一使用 UTF-8 编码
- 编译内存不足可能导致“找不到类”等构建问题

## 1. 配置项目编码

![输入图片说明](https://foruda.gitee.com/images/1662107706295343419/e27065a9_1766278.png "屏幕截图")

## 2. 配置编译内存

示例：可根据机器配置适当提升 `-Xms/-Xmx`。  
内存不足会导致编译异常或运行不稳定。

![输入图片说明](https://foruda.gitee.com/images/1764139559795286358/197fd546_1766278.png "屏幕截图")

## 3. 配置运行看板

![输入图片说明](https://foruda.gitee.com/images/1662108673306567278/8af97b47_1766278.png "屏幕截图")

### 3.1 配置 Spring 与 Docker 看板

![输入图片说明](https://foruda.gitee.com/images/1662111392476935892/6b6760fb_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1662108865191892425/3c045999_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1662108877322329668/ddb6d93d_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1662108894122798039/6a53a38c_1766278.png "屏幕截图")

## 4. 配置服务器 SSH 连接

进入 `Settings -> Tools -> SSH Configurations`，点击加号创建 SSH 配置。  
填写服务器地址、用户名、认证方式并测试连接。

示例配置（请替换为真实信息）：

| 项目   | 示例             |
|------|----------------|
| Host | 192.168.1.10   |
| Port | 22             |
| User | root           |
| Auth | Password / Key |

![输入图片说明](https://foruda.gitee.com/images/1662107776533098115/bd78467b_1766278.png "屏幕截图")

使用 `Terminal` 工具，选择已创建的 SSH 配置即可进入远程终端。

![输入图片说明](https://foruda.gitee.com/images/1662108010120640495/c70f9f9a_1766278.png "屏幕截图")

## 5. 配置服务器 SFTP 连接

进入 `Settings -> Build -> Deployment`，点击加号选择 SFTP，创建连接。  
选择前面创建的 SSH 配置并测试连接。

![输入图片说明](https://foruda.gitee.com/images/1662107899553257979/e2eeb7fd_1766278.png "屏幕截图")

在 IDEA 顶部菜单选择 `Tools -> Deployment -> Browse Remote Host` 打开远程目录窗口。  
切换到上方创建的 SFTP 配置即可浏览服务器文件。

![输入图片说明](https://foruda.gitee.com/images/1662107974682787233/b8a601fd_1766278.png "屏幕截图")

## 6. 配置 Docker 连接

支持远程 Docker 操作与镜像构建。推荐使用 SSH 方式连接。  
如果使用 TCP 方式，需要在服务器开放 `2375` 端口。

![输入图片说明](https://foruda.gitee.com/images/1662108188005932060/75872bf8_1766278.png "屏幕截图")

配置完成后运行窗口将出现 Docker 图标，可查看容器日志并执行启停等操作。

![输入图片说明](https://foruda.gitee.com/images/1662108250902891875/b82d022b_1766278.png "屏幕截图")
