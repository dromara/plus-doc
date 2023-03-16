# 分页功能

## 对应版本

> 3.5.0 版本

## 重点说明

> 项目使用 `mybatis-plus` 分页插件 实现分页功能 大致用法与 MP 一致 [MP分页文档](https://baomidou.com/pages/97710a/) <br>
项目已配置分页合理化 页数溢出 例如: 一共5页 查了第6页 默认返回第一页 <br>

![输入图片说明](https://images.gitee.com/uploads/images/2021/1223/150952_7e39ceb0_1766278.png "屏幕截图.png")

## 代码用法

> `Controller` 使用 `PageQuery` 接收分页参数 具体参数参考 `PageQuery`

![输入图片说明](https://images.gitee.com/uploads/images/2021/1223/151446_ba642595_1766278.png "屏幕截图.png")

> 构建 `Mybatis-Plus` 分页对象 <br>
使用 `PageQuery#build()` 方法 可快速(基于当前对象数据)构建 `MP` 分页对象

![输入图片说明](https://images.gitee.com/uploads/images/2021/1223/151558_cdb0e22c_1766278.png "屏幕截图.png")<br>
![输入图片说明](https://images.gitee.com/uploads/images/2021/1223/151616_80fd3ae8_1766278.png "屏幕截图.png")<br>
具体用法与 `MP` 一致

> 自定义 `SQL` 方法分页 <br>
只需在 `Mapper` 方法第一个参数和返回值 重点: 第一个参数 标注分页对象

![输入图片说明](https://images.gitee.com/uploads/images/2021/1223/151950_c1c2d57e_1766278.png "屏幕截图.png")<br>
![输入图片说明](https://images.gitee.com/uploads/images/2021/1223/151959_c3bc0cbb_1766278.png "屏幕截图.png")
