# Sharding-Proxy 搭建分库分表
- - -

## 使用示例

参考 `ruoyi-demo` 服务中的 `TestShardingController`：

![输入图片说明](https://foruda.gitee.com/images/1688014028842337522/cd26026a_1766278.png "屏幕截图")

## 1. 创建数据库与表

创建两个库：`data-center_0`、`data-center_1`。  
每个库分别执行以下 SQL：

```sql
CREATE TABLE `t_order_0` (
  `order_id` bigint(20) UNSIGNED NOT NULL COMMENT '主键ID',
  `user_id` bigint(20) UNSIGNED NOT NULL COMMENT '用户ID',
  `total_money` int(10) UNSIGNED NOT NULL COMMENT '订单总金额',
  PRIMARY KEY (`order_id`),
  KEY `idx_user_id` (`user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='订单总表';

CREATE TABLE `t_order_1` (
  `order_id` bigint(20) UNSIGNED NOT NULL COMMENT '主键ID',
  `user_id` bigint(20) UNSIGNED NOT NULL COMMENT '用户ID',
  `total_money` int(10) UNSIGNED NOT NULL COMMENT '订单总金额',
  PRIMARY KEY (`order_id`),
  KEY `idx_user_id` (`user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='订单总表';

CREATE TABLE `t_order_item_0` (
  `order_item_id` bigint(20) UNSIGNED NOT NULL COMMENT '子订单ID',
  `order_id` bigint(20) UNSIGNED NOT NULL COMMENT '主键ID',
  `user_id` bigint(20) UNSIGNED NOT NULL COMMENT '用户ID',
  `money` int(10) UNSIGNED NOT NULL COMMENT '子订单金额',
  PRIMARY KEY (`order_item_id`),
  KEY `idx_order_id` (`order_id`) USING BTREE,
  KEY `idx_user_id` (`user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='订单子表';

CREATE TABLE `t_order_item_1` (
  `order_item_id` bigint(20) UNSIGNED NOT NULL COMMENT '子订单ID',
  `order_id` bigint(20) UNSIGNED NOT NULL COMMENT '主键ID',
  `user_id` bigint(20) UNSIGNED NOT NULL COMMENT '用户ID',
  `money` int(10) UNSIGNED NOT NULL COMMENT '子订单金额',
  PRIMARY KEY (`order_item_id`),
  KEY `idx_order_id` (`order_id`) USING BTREE,
  KEY `idx_user_id` (`user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='订单子表';
```

## 2. 修改配置

修改 `config-sharding.yaml` 中的数据库连接、用户名、密码。

## 3. 服务搭建

上传 `docker` 目录，包含 `shardingproxy` 配置文件。

![输入图片说明](https://foruda.gitee.com/images/1688013921062151295/89652dda_1766278.png "屏幕截图")

框架内置 docker-compose 编排：

```shell
docker-compose up -d shardingproxy
```

## 4. 运行 Demo

启动 demo 并访问接口，检查数据库数据写入。

## 参考视频（略有不同）

- https://www.bilibili.com/video/BV1XN411A7Tv/
