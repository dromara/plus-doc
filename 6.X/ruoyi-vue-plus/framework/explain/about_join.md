# 关于多表查询
- - -

## 建议单表优先

多表 Join 容易造成性能下降与结果集膨胀，建议优先拆分单表查询。

参考资料：

- [大连接查询分解好处](https://java.isture.com/db/mysql/mysql-x-optimize-decompose-connection.html)
- [如何用 MP 多表查询性能测试](https://developer.aliyun.com/article/858927)

![输入图片说明](https://foruda.gitee.com/images/1678979482724037085/1e74f3e1_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1666336728402711844/52788205_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1666336945935088277/f60e3288_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1666336954686520161/c6c83adc_1766278.png "屏幕截图")

**上图出自《高性能 MySQL》**
