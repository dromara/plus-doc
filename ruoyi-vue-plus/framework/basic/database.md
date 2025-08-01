# 关于数据库设计
- - -

### 表设计必备字段

参考框架基础实体类`BaseEntity`内字段

* create_dept 创建部门 用于标记数据所属部门 为后续数据审计数据权限使用
* create_by 创建人 用于标记数据创建人 为后续数据审计数据权限使用
* create_time 创建时间 用于标记数据创建时间 为后续数据审计 数据排序 问题查找使用
* update_by 修改人 用于标记数据修改人 为后续数据审计 问题查找使用
* update_time 修改时间 用于标记数据修改时间 为后续数据审计 问题查找使用

### 可选字段

* tenant_id 租户ID 标记数据所属租户 如不需要租户可在yml关闭租户功能或者放行单表
* del_flag 删除标记 逻辑删除字段 用于标记数据的逻辑删除状态 如果不加为真实删除 注意必须在数据库设置默认值为0
* version 乐观锁字段 用于标记数据版本 注意标注默认值从什么版本开始 建议标注0

### 具体参考官方sql `test_demo` 表结构

![输入图片说明](https://foruda.gitee.com/images/1751508893832894882/860f08c2_1766278.png "屏幕截图")