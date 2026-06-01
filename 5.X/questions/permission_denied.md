# Redis 报错 Permission denied
- - -

## 常见原因

Redis 数据目录无写权限，RDB 或 AOF 无法落盘。


## 解决方案

1. 确认数据目录有写权限。
2. 在容器环境中授权挂载目录。

```bash
chmod 777 /docker/redis/data
```


## 补充建议

建议设置 Redis 密码（`requirepass`）并最小化文件夹权限范围。
