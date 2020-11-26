# Redis.conf详解

启动的时候，就通过配置文件来启动

> ​	单位

![image-20201109194025310](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201109194025310.png)

1.配置文件unit单位对大小写不敏感

![image-20201109194149817](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201109194149817.png)

如同spring、import、include

导入多个config

> ​	网络

```bash
bind 127.0.0.1 # 绑定的ip
protected-mode yes #  保护模式
port 6379 # 端口设置
```

> ​	通用GENERAL

```bash
daemonize yes # 以守护进程的方式运行，默认是no，我们需要自己开启为yese
pidfile /var/run/redis_6379.pid # 如果以后台的方式运行，需要指定一个进程pid文件

# 日志
# Specify the server verbosity level.
# This can be one of:
# debug (a lot of information, useful for development/testing)
# verbose (many rarely useful info, but not a mess like the debug level)
# notice (moderately verbose, what you want in production probably)生产环境
# warning (only very important / critical messages are logged)

loglevel notice
logfile "" # 日志的文件位置
databases 16 # 数据库的数量，默认为16个数据库
always-show-logo yes # 是否总是显示LOGO
```

> ​	快照

持久化，在规定的时间内，执行了多少次操作，则会持久到文件：rdb.aof

redis是内存数据库，如果没有持久化，那么数据断电即失

```bash
#
# Save the DB on disk:
#
#   save <seconds> <changes>
#
#   Will save the DB if both the given number of seconds and the given
#   number of write operations against the DB occurred.
#
#   In the example below the behavior will be to save:
#   after 900 sec (15 min) if at least 1 key changed
#   after 300 sec (5 min) if at least 10 keys changed
#   after 60 sec if at least 10000 keys changed
#
#   Note: you can disable saving completely by commenting out all "save" lines.
#
#   It is also possible to remove all the previously configured save
#   points by adding a save directive with a single empty string argument
#   like in the following example:
#
#   save ""

save 900 1
save 300 10
save 60 10000
#如果900s内，如果至少有1个key进行了修改，就进行持久化操作
#如果300s内，如果至少有10个key进行了修改，就进行持久化操作
#如果60s内，如果至少有10000个key进行了修改，就进行持久化操作
#学习了持久化后，会自定义这个测试！

stop-writes-on-bgsave-error yes #持久化如果出错，是否还需要继续

rdbcompression yes # 是否压缩rdb文件，需要消耗一些cpu资源

rdbchecksum yes # 保存rdb文件的时候，是否进行校验

dir ./ # rdb 文件保存的目录！
```

> ​	REPLICATION 主从的复制

> ​	SECURITY

```bash
127.0.0.1:6379> config get requirepass
1) "requirepass"
2) ""
127.0.0.1:6379> config set requirepass "123456"
OK
127.0.0.1:6379> config get requirepass
1) "requirepass"
2) "123456"
127.0.0.1:6379> exit
[unexpect@localhost ~]$ redis-cli -p 6379
127.0.0.1:6379> config get requirepass
(error) NOAUTH Authentication required.
127.0.0.1:6379> auth 123456
OK

```

> ​	限制

```bash
maxclients 10000	# 设置能连接上redis的最大客户端的数量
maxmemory <bytes>   # redis 配置最大的内存容量
maxmemory-policy noeviction # 内存到大上线之后的处理策略
	# 移除一些过期的可以
	# 报错
	# 。。。
    1.volatile-lru：只对设置了过期时间的key进行LRU（默认值）
    2.allkeys-lru：删除lru算法的key
    3.volatile-random： 随机删除即将过期key
    4.allkeys-random：随机删除
    5.volatile-ttl：删除即将过期的
    6.noeviction：永不过期，返回错误
```

> ​	APPEND ONLY模式 aof配置

```bash
appendonly no # 默认是不开启aof模式的，默认是使用rdb持久化的，在大部分情况下，rdb完全够用！
appendfilename "appendonly.aof" #持久化文件的名字
# appendfsync always # 每次修改都会 sync同步，消耗性能
appendfsync everysec # 每秒执行一次 sync，可能丢失这1s的数据！
# appendfsync no # 不执行 sync，这个时候操作系统自己同步数据
```

