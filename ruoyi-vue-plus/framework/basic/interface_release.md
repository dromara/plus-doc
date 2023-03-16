# 接口放行
- - -
## 使用方式

在配置文件填写路径放行<br>
![输入图片说明](https://images.gitee.com/uploads/images/2022/0528/231537_57baa4ac_1766278.png "屏幕截图.png")

### 注解放行
版本 4.3.1 以上 建议使用 `@SaIgnore` 忽略注解<br>
版本 4.2.0-4.3.0 使用 `@Anonymous` 注解(后续版本删除)

支持在类或方法上放行<br>
**注意: 动态路径会解析成通配符 请设计好接口路径避免问题**

**例如: `/get/{userId}` 会解析成 `/get/*`**<br>
![输入图片说明](https://foruda.gitee.com/images/1666595109409104199/5b7d75c7_1766278.png "屏幕截图")
![输入图片说明](https://images.gitee.com/uploads/images/2022/0528/231730_e1054ff5_1766278.png "屏幕截图.png")
![输入图片说明](https://images.gitee.com/uploads/images/2022/0528/231747_bac32888_1766278.png "屏幕截图.png")

## 注意事项

接口放行后不需要token即可访问<br>
但是没有token也就无法获取用户信息与鉴权

### 解决方案
删除接口上的鉴权注解<br>
删除接口内获取用户信息功能<br>
删除数据库实体类 自动注入 `createBy` `updateBy` 因为会获取用户数据