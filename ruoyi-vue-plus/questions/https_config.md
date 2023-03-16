### 后端 HTTPS 改造

将申请的 `https` 证书放置到 `nginx` 对应目录内<br>
根据框架 `nginx https` 示例 更改后端代理为 `https`<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/133009_fe894cb4_1766278.png "屏幕截图.png")

### 监控中心 与 任务调度中心 改造

`监控中心` 与 `任务调度中心` 属于系统管控服务<br>
应在内网使用 不应该暴漏到外网 也无需配置 `https`

更改 `系统 -> 菜单管理 -> 监控中心 与 任务调度中心` 菜单配置<br>
将其改为 `外链访问` 访问路径为 **注意: 如果是外网使用 url需配置为 http://外网ip:端口**

![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/133815_bd7d83d3_1766278.png "屏幕截图.png")
![输入图片说明](https://images.gitee.com/uploads/images/2022/0224/133830_8e740661_1766278.png "屏幕截图.png")

`nginx` 配置 `独立的端口` 进行反向代理即可访问(代理编写方式参考后端反向代理)

### Minio https 改造

下方链接包含 minio+nginx 与 minio本身配置https 两种方案<br>
[终极版minio配置https教程](https://blog.csdn.net/Michelle_Zhong/article/details/126484358)