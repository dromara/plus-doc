# 关于导入 Excel 实体类为空
- - -
* 禁止在导入实体使用 `lombok` 链式调用注解 `@Accessors(chain = true)`
* 会导致找不到 `set` 方法无法注入内容