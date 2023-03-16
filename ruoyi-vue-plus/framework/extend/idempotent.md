# 防重幂等
- - -
### 功能介绍

防重功能为防止两条相同的数据重复提交导致脏数据或业务错乱<br>
**注意: 重复提交属于小概率事件 请不要拿并发压测与之相提并论**<br>
框架防重功能参考 `美团GTIS防重系统` 使用 请求参数与用户Token或URL 生成全局业务ID<br>
有效防止 `同一个用户` 在 `限制时间` 内对 `同一个业务` 提交 `相同的数据`

框架防重处理 `支持业务失败或异常` 快速释放限制<br>
业务处理成功后 会在设置时间内 限制同一条数据的提交<br>
**注意: 只对同一个用户的同一个接口提交相同的数据有效**




### 美团GTIS系统流程图
[美团 分布式系统互斥性与幂等性问题的分析与解决](https://tech.meituan.com/2016/09/29/distributed-system-mutually-exclusive-idempotence-cerberus-gtis.html)

![输入图片说明](https://images.gitee.com/uploads/images/2022/0303/221926_94763cce_1766278.png "屏幕截图.png")

### 使用方法

在Controller标注 `@RepeatSubmit` 注解即可
![输入图片说明](https://images.gitee.com/uploads/images/2022/0303/223128_fe9cd8ab_1766278.png "屏幕截图.png")
![输入图片说明](https://images.gitee.com/uploads/images/2022/0303/222210_9d380a93_1766278.png "屏幕截图.png")