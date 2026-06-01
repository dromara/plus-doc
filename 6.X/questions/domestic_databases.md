# 如何对接国产数据库
- - -

> 1. 框架采用 mybatis-plus 几乎支持大部分市面上的数据库且框架内几乎没有sql语句存在
<br>
主要需要关注 JDBC 驱动、SQL 关键字和数据库方言差异。
<br>
> 2. 国产数据库通常会参考主流数据库协议或语法
<br>
例如达梦、人大金仓、OceanBase 等都需要按实际模式选择脚本和方言。

# 对接方式

### 这里用 `达梦` 数据库为例

1. 首先增加 JDBC 依赖包。单体项目通常加在主应用模块，Cloud 项目通常加在 `ruoyi-common-mybatis` 模块。

![输入图片说明](https://foruda.gitee.com/images/1723288594335994875/216ae8e7_1766278.png "屏幕截图")

2.在配置文件yml内配置数据库连接

![输入图片说明](https://foruda.gitee.com/images/1723288760519808620/3db91ba5_1766278.png "屏幕截图")

3. SQL 脚本使用项目内自带脚本，根据目标数据库支持的模式选择，例如达梦可参考 Oracle 脚本。

![输入图片说明](https://foruda.gitee.com/images/1723289018873298537/4d95c892_1766278.png "屏幕截图")

4.在代码生成器内 增加对应的数据库生成器依赖 代码生成器使用 anyline 支持几百种数据库只需要增加对应的依赖即可

![输入图片说明](https://foruda.gitee.com/images/1723288974693848785/3e8fc61f_1766278.png "屏幕截图")

这样基本就完成了所有需要做的事可以尝试启动项目了

5.如果项目启或者运行动过程中有sql报错 不要慌基本上都是一些关键字引起的
<br>
例如 达梦内的`domain`就是关键字 在我们的`SysOssConfig`表内使用`domain`进行自定义的域名存储
<br>
我们只需要在`SysOssConfig`实体类的`domain`属性增加一个注解即可解决此问题
<br>
**注意: 各种数据库处理关键字的标识符不一样注意替换**

![输入图片说明](https://foruda.gitee.com/images/1723289232470339283/480d5172_1766278.png "屏幕截图")

6.人大金仓注意事项 由于此数据库系统表与业务表不隔离(恶心) 表 `sys_user`冲突

解决方案1 将表名 `sys_user` 改为 `sys_user_info` 代码实体类 `SysUser` 上的数据库表名注解也改为 `sys_user_info` 即可
<br>
解决方案2 修改连接串配置 jdbc:kingbase8://localhost:54321/test?currentSchema=ry-cloud,sys,sys_catalog,pg_catalog
