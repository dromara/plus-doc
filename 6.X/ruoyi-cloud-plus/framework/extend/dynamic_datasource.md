# 多数据源
- - -

## 配置位置

Cloud 的数据源统一维护在 Nacos：

```text
script/config/nacos/datasource.yml
```

默认示例数据源：

```text
system-master  系统服务主库
gen            代码生成数据源
job            SnailJob 数据源
workflow       工作流数据源
```

`spring.datasource.dynamic.strict: true` 已开启，`@DS` 指定的数据源不存在时会直接报错。`seata` 代理开关读取 `${seata.enabled}`。

## 模块位置

动态数据源依赖在公共 MyBatis 模块中引入：

```text
ruoyi-common/ruoyi-common-mybatis
```

如需新增 Oracle、PostgreSQL、SQL Server 等数据库驱动，在对应服务或公共 MyBatis 模块中补充 JDBC 驱动依赖，并在 `datasource.yml` 新增数据源配置。

## 使用方式

在 Service 或 Mapper 方法上使用 `@DS`：

```java
@DS("workflow")
public List<?> queryWorkflowData() {
    return mapper.selectList();
}
```

数据源匹配优先级为：

```text
方法注解 > 类注解 > 默认数据源
```

生成器使用 SpEL 动态切换数据源：

```java
@DS("#dataName")
public List<GenTable> selectDbTableListByNames(String[] tableNames, String dataName) {
    return genTableMapper.selectDbTableListByNames(tableNames);
}
```

对应源码：

```text
ruoyi-modules/ruoyi-gen/src/main/java/org/dromara/gen/service/GenTableServiceImpl.java
```

## 新增数据源步骤

1. 在 `datasource.yml` 顶部新增连接配置，例如 `report`。
2. 在 `spring.datasource.dynamic.datasource` 下引用或补齐该数据源。
3. 业务方法加 `@DS("report")`。
4. 如果该库也用于代码生成，前端生成页选择对应 `dataName` 后再导入表。

## 事务说明

普通单库事务仍使用 Spring `@Transactional`。跨数据源事务请结合当前项目的 Seata 配置，并参考：

[事务相关](/6.X/ruoyi-cloud-plus/framework/explain/transaction.md)

使用注意：

- `@DS` 和事务边界要放在同一个 AOP 可代理调用链上，避免同类内部直接调用导致注解不生效。
- `strict: true` 下数据源名称必须完全匹配。
- 不同数据库混用时，SQL 方言、字段类型、分页语法和驱动依赖都要单独确认。
