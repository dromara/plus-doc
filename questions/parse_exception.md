# ParseException SQL解析异常
- - -
## 异常内容

`net.sf.jsqlparser.parser.ParseException: Encountered unexpected token:`

![输入图片说明](https://images.gitee.com/uploads/images/2021/1217/181222_efc6cea0_1766278.png "屏幕截图.png")

此异常为 SQL 解析异常, 应检查 SQL 语句内是否包含 SQL 关键字

异常通常都会提供坐标

![输入图片说明](https://images.gitee.com/uploads/images/2021/1217/181332_5b5889c3_1766278.png "屏幕截图.png")

检查报错 SQL 相关坐标位置

![输入图片说明](https://images.gitee.com/uploads/images/2021/1217/181524_1c57e5ab_1766278.png "屏幕截图.png")

## 异常由来
由 Mybatis-Plus 拦截器进行 SQL 解析导致<br>
常见拦截器导致问题 `TenantLineInnerInterceptor` `DataPermissionInterceptor`

## 解决方案

> 将关键字增加标识符区别开

1.实体类字段处理(以下仅限于mysql 其他数据库方法各不相同)

![输入图片说明](https://images.gitee.com/uploads/images/2021/1217/181712_469ece25_1766278.png "屏幕截图.png")

2.自定义 SQL 或 XML 处理

![输入图片说明](https://images.gitee.com/uploads/images/2022/0505/144536_2263477f_1766278.png "屏幕截图.png")

3.Mapper排除
> 查看具体使用了哪些拦截器导致问题 使用忽略注解依次进行排除即可

![输入图片说明](https://images.gitee.com/uploads/images/2021/1217/182228_a630436c_1766278.png "屏幕截图.png")


