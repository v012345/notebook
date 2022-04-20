## 操作系统
Rocky 8
## 安装
不说了,推荐用包管理工具
## 启动
现在是学习,就不要用什么集群,哨兵之类了,也不要用密码了
```console
systemctl start redis.service
```
## redis-cli
```console
reids-cli
```

## 数据类型
### 字符串
String 是一组字节。在 Redis 数据库中，字符串是二进制安全的。这意味着它们具有已知长度，并且不受任何特殊终止字符的影响。可以在一个字符串中存储最多 512 兆字节的内容。
