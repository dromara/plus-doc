# MP / MPJ 封装
- - -

框架在 `ruoyi-common-mybatis` 中对 MyBatis-Plus 和 MyBatis-Plus-Join 做了二次封装，业务代码优先使用这些入口，少写重复转换和空值判断。

核心源码位置：

```text
ruoyi-common/ruoyi-common-mybatis/src/main/java/org/dromara/common/mybatis
```

## Mapper 定义

普通 Mapper 继承 `BaseMapperPlus<Entity, Vo>`：

```java
public interface SysConfigMapper extends BaseMapperPlus<SysConfig, SysConfigVo> {
}
```

需要 MPJ 原生能力时，同时继承 `MPJBaseMapper<Entity>`：

```java
public interface SysUserMapper extends BaseMapperPlus<SysUser, SysUserVo>, MPJBaseMapper<SysUser> {
}
```

两个泛型的含义：

| 泛型 | 说明 |
| --- | --- |
| `Entity` | 数据库实体 |
| `Vo` | 默认返回对象 |

`BaseMapperPlus` 会基于泛型解析默认 VO 类型，所以泛型必须写完整。

## BaseMapperPlus

常用查询：

```java
SysUserVo user = userMapper.selectVoById(userId);

List<SysUserVo> users = userMapper.selectVoList(
    QueryBuilder.lambda(SysUser.class)
        .eqIfText(SysUser::getUserName, userName)
        .build()
);

Page<SysUserVo> page = userMapper.selectVoPage(
    pageQuery.build(),
    QueryBuilder.lambda(SysUser.class)
        .likeIfText(SysUser::getNickName, nickName)
        .build()
);
```

常用方法：

| 方法 | 说明 |
| --- | --- |
| `selectVoById(id)` | 按主键查询并转换为默认 VO |
| `selectVoByIds(ids)` | 按主键集合查询 VO |
| `selectVoOne(wrapper)` | 查询单条 VO，默认多条时抛异常 |
| `selectVoOne(wrapper, false)` | 查询单条 VO，多条时不抛异常 |
| `selectVoList(wrapper)` | 查询 VO 列表 |
| `selectVoPage(page, wrapper)` | 查询 VO 分页 |
| `insertBatch(list)` | 批量新增 |
| `updateBatchById(list)` | 批量按 ID 更新 |
| `insertOrUpdateBatch(list)` | 批量新增或更新 |

如果查询结果不是默认 VO，可传目标类型：

```java
List<UserOptionVo> list = userMapper.selectVoList(wrapper, UserOptionVo.class);
```

## mapper.lambda()

`BaseMapperPlus#lambda()` 返回 `LambdaCrudChainWrapper`，适合在当前 Mapper 上做链式 CRUD。

查询实体：

```java
SysConfig config = configMapper.lambda()
    .eq(SysConfig::getConfigKey, configKey)
    .one();
```

查询 VO：

```java
SysConfigVo config = configMapper.lambda()
    .eqIfText(SysConfig::getConfigKey, configKey)
    .voOne(false);
```

查询列表和分页：

```java
List<SysConfigVo> list = configMapper.lambda()
    .likeIfText(SysConfig::getConfigName, bo.getConfigName())
    .orderByAsc(SysConfig::getConfigId)
    .voList();

Page<SysConfigVo> page = configMapper.lambda()
    .likeIfText(SysConfig::getConfigName, bo.getConfigName())
    .voPage(pageQuery.build());
```

更新和删除：

```java
boolean updated = configMapper.lambda()
    .eq(SysConfig::getConfigId, bo.getConfigId())
    .setIfText(SysConfig::getConfigName, bo.getConfigName())
    .setIfPresent(SysConfig::getRemark, bo.getRemark())
    .update();

int rows = configMapper.lambda()
    .eq(SysConfig::getConfigId, configId)
    .deleteCount();
```

常用增强条件：

| 方法 | 说明 |
| --- | --- |
| `eqIfPresent` | 值不为 `null` 时追加等值条件 |
| `eqIfText` | 字符串不为空白时追加等值条件 |
| `likeIfText` | 字符串不为空白时追加模糊条件 |
| `betweenIfPresent` | 起止值都不为空时追加区间条件 |
| `betweenParams` | 从 `params` 中读取起止值追加区间条件 |
| `inIfNotEmpty` | 集合不为空时追加 `in` 条件 |
| `findInSetIfPresent` | 值不为空时追加 `find_in_set` 条件 |

## QueryBuilder.lambda()

`QueryBuilder.lambda(Entity.class)` 适合在 service 中构建可复用 Wrapper，最后调用 `.build()` 交给 Mapper。

```java
private LambdaQueryWrapper<SysConfig> buildQueryWrapper(SysConfigBo bo) {
    return QueryBuilder.lambda(SysConfig.class)
        .eqIfText(SysConfig::getConfigType, bo.getConfigType())
        .likeIfText(SysConfig::getConfigName, bo.getConfigName())
        .betweenParams(SysConfig::getCreateTime, bo.getParams(), "beginTime", "endTime")
        .orderByAsc(SysConfig::getConfigId)
        .build();
}
```

聚合查询：

```java
LambdaQueryWrapper<SysOperLog> wrapper = QueryBuilder.lambda(SysOperLog.class)
    .selectCountAll(OperLogStatVo::getTotal)
    .selectMax(SysOperLog::getOperTime, OperLogStatVo::getLastOperTime)
    .eqIfText(SysOperLog::getStatus, status)
    .build();
```

子查询：

```java
LambdaQueryWrapper<SysUser> wrapper = QueryBuilder.lambda(SysUser.class)
    .inSub(SysUser::getUserId, SysUserRole.class, sub -> sub
        .select(SysUserRole::getUserId)
        .eq(SysUserRole::getRoleId, roleId))
    .build();
```

如果封装没有覆盖到的 MP 原生能力，可以通过 `apply(wrapper -> ...)` 直接操作底层 `LambdaQueryWrapper`：

```java
QueryBuilder.lambda(SysUser.class)
    .apply(w -> w.last("limit 1"))
    .build();
```

## PageQuery

Controller 直接接收 `PageQuery`：

```java
@GetMapping("/list")
public R<PageResult<SysConfigVo>> list(SysConfigBo bo, PageQuery pageQuery) {
    return R.ok(configService.queryPageList(bo, pageQuery));
}
```

Service 中构建 MP 分页：

```java
Page<SysConfigVo> page = configMapper.selectVoPage(pageQuery.build(), wrapper);
return PageResult.build(page);
```

排序参数：

```text
pageNum=1
pageSize=10
orderByColumn=createTime
isAsc=desc
```

`orderByColumn` 支持多个字段，`isAsc` 可以传一个方向或多个方向：

```text
orderByColumn=id,createTime
isAsc=asc,desc
```

前端的 `ascending`、`descending` 会自动转换成 `asc`、`desc`。

## MPJ 联表查询

联表查询使用 `QueryBuilder.lambdaJoin(...)`。

```java
List<SysUserVo> list = QueryBuilder.lambdaJoin("u", SysUser.class)
    .selectAs("u", SysUser::getUserId, SysUserVo::getUserId)
    .selectAs("u", SysUser::getUserName, SysUserVo::getUserName)
    .selectAs("d", SysDept::getDeptName, SysUserVo::getDeptName)
    .leftJoin(SysDept.class, "d", SysDept::getDeptId, SysUser::getDeptId)
    .eqIfText("u", SysUser::getUserName, bo.getUserName())
    .likeIfText("d", SysDept::getDeptName, bo.getDeptName())
    .list(SysUserVo.class);
```

分页：

```java
Page<SysUserVo> page = QueryBuilder.lambdaJoin("u", SysUser.class)
    .selectAll(SysUser.class, "u")
    .selectAs("d", SysDept::getDeptName, SysUserVo::getDeptName)
    .leftJoin(SysDept.class, "d", SysDept::getDeptId, SysUser::getDeptId)
    .page(pageQuery.build(), SysUserVo.class);
```

常用 MPJ 方法：

| 方法 | 说明 |
| --- | --- |
| `select` | 选择字段 |
| `selectAll` | 选择实体全部字段 |
| `selectAs` | 字段映射到返回对象属性 |
| `leftJoin` | 左连接 |
| `eqIfPresent` / `eqIfText` | 条件不为空时追加等值条件 |
| `likeIfText` | 字符串不为空白时追加模糊条件 |
| `betweenParams` | 从参数 Map 读取区间条件 |
| `inIfNotEmpty` | 集合不为空时追加 `in` |
| `list(resultClass)` | 查询列表 |
| `page(page, resultClass)` | 分页查询 |
| `count()` | 查询数量 |
| `build()` | 返回底层 `MPJLambdaWrapper` |

MPJ 聚合和子查询：

```java
List<UserStatVo> list = QueryBuilder.lambdaJoin("u", SysUser.class)
    .selectAs("u", SysUser::getUserId, UserStatVo::getUserId)
    .selectCountAll(UserStatVo::getTotal)
    .selectSub(SysUserRole.class, sub -> sub
        .selectCountAll()
        .eqColumn(SysUserRole::getUserId, "u", SysUser::getUserId),
        UserStatVo::getRoleCount)
    .list(UserStatVo.class);
```

如果需要使用 MPJ 原生能力：

```java
QueryBuilder.lambdaJoin("u", SysUser.class)
    .apply(wrapper -> wrapper.last("limit 10"))
    .list(SysUserVo.class);
```

## 选型建议

- 单表普通查询优先用 `mapper.lambda()`
- 需要复用 Wrapper 或组合复杂条件时用 `QueryBuilder.lambda()`
- 返回 VO 时优先用 `selectVo*`、`voList()`、`voPage()`
- 多表查询用 `QueryBuilder.lambdaJoin()`，不要为了联表手写大量 XML
- 复杂 SQL、数据库特有语法、批量更新语句仍可保留 XML 或注解 SQL
