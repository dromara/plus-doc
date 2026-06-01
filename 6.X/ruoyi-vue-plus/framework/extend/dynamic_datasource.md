# 多数据源
- - -

## 配置位置

单体项目的数据源配置在环境配置文件中：

```text
ruoyi-admin/src/main/resources/application-dev.yml
ruoyi-admin/src/main/resources/application-prod.yml
```

核心节点：

```yaml
spring:
  datasource:
    dynamic:
      primary: master
      strict: true
      datasource:
        master:
          url: jdbc:mysql://localhost:3306/ry-vue
```

默认主数据源为 `master`。`strict: true` 已开启，`@DS` 指定的数据源不存在时会直接报错。

## 模块位置

动态数据源依赖在公共 MyBatis 模块中引入：

```text
ruoyi-common/ruoyi-common-mybatis
```

如需新增 Oracle、PostgreSQL、SQL Server 等数据库驱动，在 `ruoyi-admin` 或公共 MyBatis 模块中补充 JDBC 驱动依赖，并在 `application-*.yml` 新增数据源配置。

## 使用方式

在 Service 或 Mapper 方法上使用 `@DS`：

```java
@DS("slave")
public List<?> querySlaveData() {
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

1. 在 `spring.datasource.dynamic.datasource` 下新增数据源，例如 `slave`、`report`。
2. 确认驱动依赖已经引入。
3. 业务方法加 `@DS("slave")` 或对应数据源名。
4. 如果该库也用于代码生成，前端生成页选择对应 `dataName` 后再导入表。

## 事务说明

普通单库事务仍使用 Spring `@Transactional`。多数据源事务请参考：

[事务相关](/6.X/ruoyi-vue-plus/framework/explain/transaction.md)

使用注意：

- `@DS` 和事务边界要放在同一个 AOP 可代理调用链上，避免同类内部直接调用导致注解不生效。
- `strict: true` 下数据源名称必须完全匹配。
- 不同数据库混用时，SQL 方言、字段类型、分页语法和驱动依赖都要单独确认。
