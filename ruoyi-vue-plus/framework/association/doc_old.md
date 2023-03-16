# (旧)接口文档
- - -
## 访问方式

### 前端访问 `系统工具 -> 系统接口`
![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/100233_7308b4b5_1766278.png "屏幕截图.png")

### 后端访问 `后端ip:端口/doc.html`
注意 由于文档框架与前端整合使用 <br>
纯后端使用需去除配置文件中的 `swagger.pathMapping` VUE代理路径 <br>
![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/100514_e402ae24_1766278.png "屏幕截图.png")

## 文档配置

![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/100741_f1ce664b_1766278.png "屏幕截图.png") <br>
![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/100747_e285bac7_1766278.png "屏幕截图.png")

`swagger` 前缀配置为基础配置 <br>
`knife4j` 前缀配置为增强配置 增强配置可以查看 [knife4j文档](https://doc.xiaominfo.com/) 框架文档

## 重点配置介绍

`groups` 为分组配置 需配置组名与包名

![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/101836_767546d7_1766278.png "屏幕截图.png")
![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/101952_fd9d9a74_1766278.png "屏幕截图.png")

不分组使用 把所有组合并成一个 扫描最顶层的包即可

![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/102124_26cb156f_1766278.png "屏幕截图.png")

`knife4j.production` 生产保护 开启生产保护 `prod` 环境则接口文档无法访问

![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/102221_1a19ab8d_1766278.png "屏幕截图.png") <br>
![输入图片说明](https://images.gitee.com/uploads/images/2021/1221/102243_b4c7bcd1_1766278.png "屏幕截图.png")



