# 事务相关
- - -

## 参考资料

事务注解基础说明：

- https://doc.ruoyi.vip/ruoyi/document/htsc.html#%E4%BA%8B%E5%8A%A1%E7%AE%A1%E7%90%86

以下补充多数据源事务说明。

## 分布式事务（Seata）

框架已默认对接 Seata，直接使用其注解即可。  
参考文档：https://www.kancloud.cn/tracy5546/dynamic-datasource/2268607

## 本地多数据源事务

使用 `@DSTransactional` 注解，代理 `@DS` 切换的数据源事务。  
注解范围内任一环节异常，会触发全局回滚。

**说明：** B、C 方法上再次标注 `@DSTransactional` 不影响结果。

```java
// AService 调用 BService 与 CService，分别对应不同数据源

public class AService {

    @DS("a") // 如果 a 是默认数据源可省略
    @DSTransactional
    public void dosomething(){
        BService.dosomething();
        CService.dosomething();
    }
}

public class BService {

    @DS("b")
    public void dosomething(){
        // dosomething
    }
}

public class CService {

    @DS("c")
    public void dosomething(){
        // dosomething
    }
}
```
