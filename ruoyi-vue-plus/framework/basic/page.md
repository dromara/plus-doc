# 分页功能
- - -

## 适用版本

- 3.5.0 版本

## 功能说明

- 基于 `MyBatis-Plus` 分页插件实现
- 已开启分页合理化：页码溢出会返回第一页
- 用法与 MP 一致，可直接复用 MP 经验

参考文档：[MP分页文档](https://baomidou.com/pages/97710a/)

![输入图片说明](https://foruda.gitee.com/images/1678977804058241635/b5cb362d_1766278.png "屏幕截图")

## 使用步骤

### 1. Controller 接收分页参数

使用 `PageQuery` 接收分页参数，具体字段可参考 `PageQuery` 类。

![输入图片说明](https://foruda.gitee.com/images/1678977844048821356/1f994221_1766278.png "屏幕截图")

### 2. 构建 MP 分页对象

使用 `PageQuery#build()` 基于当前对象快速构建 MP 分页对象。

![输入图片说明](https://foruda.gitee.com/images/1678977862816976499/b82c1638_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678977876194578744/eaa7b854_1766278.png "屏幕截图")

### 3. 自定义 SQL 分页

自定义 SQL 需要在 Mapper 方法**第一个参数**传入分页对象，返回值为分页结果。

![输入图片说明](https://foruda.gitee.com/images/1678977898181729571/6e102731_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1678977906788451483/70979292_1766278.png "屏幕截图")

## 示例参数

- `pageNum=1`
- `pageSize=10`
