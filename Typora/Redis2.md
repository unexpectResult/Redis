# Redis2

## 测试性能

**redis-benchmark**压力测试工具！

官方自带的性能测试工具

![image-20201108203613807](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108203613807.png)

测试

```bash
测试：100个并发连接100000请求

redis-benchmark -c 100 -n 100000
```

![image-20201108205337861](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108205337861.png)

## 基础的知识

redist默认有16个数据库

默认数据库为第0个

**可以使用select进行切换数据库**

![image-20201108205627071](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108205627071.png)

**keys * 查看数据库中所有的key**

![image-20201108205817367](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108205817367.png)

**清除当前数据库所有数据**

![image-20201108205849077](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108205849077.png)

**清除所有数据库的数据**

![image-20201108210053314](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108210053314.png)

### Redis6支持多线程了

Redis的单线程为什么这么快？

1.误区1：高性能的服务器一定是多线程？

2.误区2：多线程（CPU上下文会切换！）一定比单线程效率高？

先去CPU>内存>硬盘的速度要有所了解

核心：redis是将所有的数据放在内存中的，所以说使用单线程操作去操作效率就是最高的，多线程（CPU上下文会切换：耗时的操作！），对于内存系统来说，如果没有上下文切换效率就是最高的！多次读写都是在一个CPU上的，在内存情况下，这个就是最佳方案！

### 五大数据类型

![image-20201108210915476](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108210915476.png)

#### 服务器命令

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [BGREWRITEAOF](https://www.w3cschool.cn/redis/server-bgrewriteaof.html) 异步执行一个 AOF（AppendOnly File） 文件重写操作 |
| 2    | [BGSAVE](https://www.w3cschool.cn/redis/server-bgsave.html) 在后台异步保存当前数据库的数据到磁盘 |
| 3    | [CLIENT KILL [ip:port\] [ID client-id]](https://www.w3cschool.cn/redis/server-client-kill.html) 关闭客户端连接 |
| 4    | [CLIENT LIST](https://www.w3cschool.cn/redis/server-client-list.html) 获取连接到服务器的客户端连接列表 |
| 5    | [CLIENT GETNAME](https://www.w3cschool.cn/redis/server-client-getname.html) 获取连接的名称 |
| 6    | [CLIENT PAUSE timeout](https://www.w3cschool.cn/redis/server-client-pause.html) 在指定时间内终止运行来自客户端的命令 |
| 7    | [CLIENT SETNAME connection-name](https://www.w3cschool.cn/redis/server-client-setname.html) 设置当前连接的名称 |
| 8    | [CLUSTER SLOTS](https://www.w3cschool.cn/redis/server-cluster-slots.html) 获取集群节点的映射数组 |
| 9    | [COMMAND](https://www.w3cschool.cn/redis/server-command.html) 获取 Redis 命令详情数组 |
| 10   | [COMMAND COUNT](https://www.w3cschool.cn/redis/server-command-count.html) 获取 Redis 命令总数 |
| 11   | [COMMAND GETKEYS](https://www.w3cschool.cn/redis/server-command-getkeys.html) 获取给定命令的所有键 |
| 12   | [TIME](https://www.w3cschool.cn/redis/server-time.html) 返回当前服务器时间 |
| 13   | [COMMAND INFO command-name [command-name ...\]](https://www.w3cschool.cn/redis/server-command-info.html) 获取指定 Redis 命令描述的数组 |
| 14   | [CONFIG GET parameter](https://www.w3cschool.cn/redis/server-config-get.html) 获取指定配置参数的值 |
| 15   | [CONFIG REWRITE](https://www.w3cschool.cn/redis/server-config-rewrite.html) 对启动 Redis 服务器时所指定的 redis.conf 配置文件进行改写 |
| 16   | [CONFIG SET parameter value](https://www.w3cschool.cn/redis/server-config-set.html) 修改 redis 配置参数，无需重启 |
| 17   | [CONFIG RESETSTAT](https://www.w3cschool.cn/redis/server-config-resetstat.html) 重置 INFO 命令中的某些统计数据 |
| 18   | [DBSIZE](https://www.w3cschool.cn/redis/server-dbsize.html) 返回当前数据库的 key 的数量 |
| 19   | [DEBUG OBJECT key](https://www.w3cschool.cn/redis/server-debug-object.html) 获取 key 的调试信息 |
| 20   | [DEBUG SEGFAULT](https://www.w3cschool.cn/redis/server-debug-segfault.html) 让 Redis 服务崩溃 |
| 21   | [FLUSHALL](https://www.w3cschool.cn/redis/server-flushall.html) 删除所有数据库的所有key |
| 22   | [FLUSHDB](https://www.w3cschool.cn/redis/server-flushdb.html) 删除当前数据库的所有key |
| 23   | [INFO [section\]](https://www.w3cschool.cn/redis/server-info.html) 获取 Redis 服务器的各种信息和统计数值 |
| 24   | [LASTSAVE](https://www.w3cschool.cn/redis/server-lastsave.html) 返回最近一次 Redis 成功将数据保存到磁盘上的时间，以 UNIX 时间戳格式表示 |
| 25   | [MONITOR](https://www.w3cschool.cn/redis/server-monitor.html) 实时打印出 Redis 服务器接收到的命令，调试用 |
| 26   | [ROLE](https://www.w3cschool.cn/redis/server-role.html) 返回主从实例所属的角色 |
| 27   | [SAVE](https://www.w3cschool.cn/redis/server-save.html) 异步保存数据到硬盘 |
| 28   | [SHUTDOWN [NOSAVE\] [SAVE]](https://www.w3cschool.cn/redis/server-shutdown.html) 异步保存数据到硬盘，并关闭服务器 |
| 29   | [SLAVEOF host port](https://www.w3cschool.cn/redis/server-slaveof.html) 将当前服务器转变为指定服务器的从属服务器(slave server) |
| 30   | [SLOWLOG subcommand [argument\]](https://www.w3cschool.cn/redis/server-showlog.html) 管理 redis 的慢日志 |
| 31   | [SYNC](https://www.w3cschool.cn/redis/server-sync.html) 用于复制功能(replication)的内部命令 |

#### 连接命令

下表列出了 redis 连接的基本命令：

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [AUTH password](https://www.w3cschool.cn/redis/connection-auth.html) 验证密码是否正确 |
| 2    | [ECHO message](https://www.w3cschool.cn/redis/connection-echo.html) 打印字符串 |
| 3    | [PING](https://www.w3cschool.cn/redis/connection-ping.html) 查看服务是否运行 |
| 4    | [QUIT](https://www.w3cschool.cn/redis/connection-quit.html) 关闭当前连接 |
| 5    | [SELECT index](https://www.w3cschool.cn/redis/connection-select.html) 切换到指定的数据库 |

#### Redis-Key

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [DEL key](https://www.w3cschool.cn/redis/keys-del.html) 该命令用于在 key 存在时删除 key。 |
| 2    | [DUMP key](https://www.w3cschool.cn/redis/keys-dump.html) 序列化给定 key ，并返回被序列化的值。 |
| 3    | [EXISTS key](https://www.w3cschool.cn/redis/keys-exists.html) 检查给定 key 是否存在。 |
| 4    | [EXPIRE key](https://www.w3cschool.cn/redis/keys-expire.html) seconds 为给定 key 设置过期时间。 |
| 5    | [EXPIREAT key timestamp](https://www.w3cschool.cn/redis/keys-expireat.html) EXPIREAT 的作用和 EXPIRE 类似，都用于为 key 设置过期时间。 不同在于 EXPIREAT 命令接受的时间参数是 UNIX 时间戳(unix timestamp)。 |
| 6    | [PEXPIRE key milliseconds](https://www.w3cschool.cn/redis/keys-pexpire.html) 设置 key 的过期时间以毫秒计。 |
| 7    | [PEXPIREAT key milliseconds-timestamp](https://www.w3cschool.cn/redis/keys-pexpireat.html) 设置 key 过期时间的时间戳(unix timestamp) 以毫秒计 |
| 8    | [KEYS pattern](https://www.w3cschool.cn/redis/keys-keys.html) 查找所有符合给定模式( pattern)的 key 。 |
| 9    | [MOVE key db](https://www.w3cschool.cn/redis/keys-move.html) 将当前数据库的 key 移动到给定的数据库 db 当中。 |
| 10   | [PERSIST key](https://www.w3cschool.cn/redis/keys-persist.html) 移除 key 的过期时间，key 将持久保持。 |
| 11   | [PTTL key](https://www.w3cschool.cn/redis/keys-pttl.html) 以毫秒为单位返回 key 的剩余的过期时间。 |
| 12   | [TTL key](https://www.w3cschool.cn/redis/keys-ttl.html) 以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)。 |
| 13   | [RANDOMKEY](https://www.w3cschool.cn/redis/keys-randomkey.html) 从当前数据库中随机返回一个 key 。 |
| 14   | [RENAME key newkey](https://www.w3cschool.cn/redis/keys-rename.html) 修改 key 的名称 |
| 15   | [RENAMENX key newkey](https://www.w3cschool.cn/redis/keys-renamenx.html) 仅当 newkey 不存在时，将 key 改名为 newkey 。 |
| 16   | [TYPE key](https://www.w3cschool.cn/redis/keys-type.html) 返回 key 所储存的值的类型。 |

![image-20201108211223800](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108211223800.png)

![image-20201108211359927](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108211359927.png)

```makefile
127.0.0.1:6379> set name zjp # set key
OK
127.0.0.1:6379> set name2 pjz
OK
127.0.0.1:6379> keys *
1) "name2"
2) "name"
127.0.0.1:6379> EXISTS name # 判断当前的key是否存在
(integer) 1
127.0.0.1:6379> EXISTS name3
(integer) 0
127.0.0.1:6379> move name 1 # 移除当前的key
(integer) 1
127.0.0.1:6379> keys *
1) "name2"
127.0.0.1:6379> set name zjp
OK
127.0.0.1:6379> EXPIRE name 10 # 设置可以的过期时间，单位是秒
(integer) 1
127.0.0.1:6379> ttl name # 查看当前key的剩余时间
(integer) 5
127.0.0.1:6379> get name
(nil)
127.0.0.1:6379> 
127.0.0.1:6379> type name2 #查看当前key的类型
string
127.0.0.1:6379> 

```

#### String字符串

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [SET key value](https://www.w3cschool.cn/redis/strings-set.html) 设置指定 key 的值 |
| 2    | [GET key](https://www.w3cschool.cn/redis/strings-get.html) 获取指定 key 的值。 |
| 3    | [GETRANGE key start end](https://www.w3cschool.cn/redis/strings-getrange.html) 返回 key 中字符串值的子字符 |
| 4    | [GETSET key value](https://www.w3cschool.cn/redis/strings-getset.html) 将给定 key 的值设为 value ，并返回 key 的旧值(old value)。 |
| 5    | [GETBIT key offset](https://www.w3cschool.cn/redis/strings-getbit.html) 对 key 所储存的字符串值，获取指定偏移量上的位(bit)。 |
| 6    | [MGET key1 [key2..\]](https://www.w3cschool.cn/redis/strings-mget.html) 获取所有(一个或多个)给定 key 的值。 |
| 7    | [SETBIT key offset value](https://www.w3cschool.cn/redis/strings-setbit.html) 对 key 所储存的字符串值，设置或清除指定偏移量上的位(bit)。 |
| 8    | [SETEX key seconds value](https://www.w3cschool.cn/redis/strings-setex.html) 将值 value 关联到 key ，并将 key 的过期时间设为 seconds (以秒为单位)。 |
| 9    | [SETNX key value](https://www.w3cschool.cn/redis/strings-setnx.html) 只有在 key 不存在时设置 key 的值。 |
| 10   | [SETRANGE key offset value](https://www.w3cschool.cn/redis/strings-setrange.html) 用 value 参数覆写给定 key 所储存的字符串值，从偏移量 offset 开始。 |
| 11   | [STRLEN key](https://www.w3cschool.cn/redis/strings-strlen.html) 返回 key 所储存的字符串值的长度。 |
| 12   | [MSET key value [key value ...\]](https://www.w3cschool.cn/redis/strings-mset.html) 同时设置一个或多个 key-value 对。 |
| 13   | [MSETNX key value [key value ...\]](https://www.w3cschool.cn/redis/strings-msetnx.html) 同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。 |
| 14   | [PSETEX key milliseconds value](https://www.w3cschool.cn/redis/strings-psetex.html) 这个命令和 SETEX 命令相似，但它以毫秒为单位设置 key 的生存时间，而不是像 SETEX 命令那样，以秒为单位。 |
| 15   | [INCR key](https://www.w3cschool.cn/redis/strings-incr.html) 将 key 中储存的数字值增一。 |
| 16   | [INCRBY key increment](https://www.w3cschool.cn/redis/strings-incrby.html) 将 key 所储存的值加上给定的增量值（increment） 。 |
| 17   | [INCRBYFLOAT key increment](https://www.w3cschool.cn/redis/strings-incrbyfloat.html) 将 key 所储存的值加上给定的浮点增量值（increment） 。 |
| 18   | [DECR key](https://www.w3cschool.cn/redis/strings-decr.html) 将 key 中储存的数字值减一。 |
| 19   | [DECRBY key decrement](https://www.w3cschool.cn/redis/strings-decrby.html) key 所储存的值减去给定的减量值（decrement） 。 |
| 20   | [APPEND key value](https://www.w3cschool.cn/redis/strings-append.html) 如果 key 已经存在并且是一个字符串， APPEND 命令将 value 追加到 key 原来的值的末尾。 |

```bash
127.0.0.1:6379> set key1 v1 		# 设置值
OK
127.0.0.1:6379> get key1 			# 获取值
"v1"
127.0.0.1:6379> APPEND key1 "hello" # 追加字符串，如果当前可以不存在，就会set一个key
(integer) 7
127.0.0.1:6379> get key1 			
"v1hello"
127.0.0.1:6379> STRLEN key1 		#获取字符串长度
(integer) 7
127.0.0.1:6379> APPEND key1 ",world"
(integer) 13
127.0.0.1:6379> get key1
"v1hello,world"
127.0.0.1:6379> 
```

```bash

127.0.0.1:6379> set views 0 #初始值为1
OK
127.0.0.1:6379> get views
"0"
127.0.0.1:6379> incr views #自增1
(integer) 1
127.0.0.1:6379> incr views
(integer) 2
127.0.0.1:6379> get views
"2"
127.0.0.1:6379> decr views #自减1
(integer) 1
127.0.0.1:6379> get views
"1" 
127.0.0.1:6379> INCRBY views 10 #可以设置自定增加的步长
#DECRBY 自定义减少的步长
(integer) 11
127.0.0.1:6379> get views
"11"
127.0.0.1:6379> 

```

```bash
##字符串范围

127.0.0.1:6379> set key1 "hello,redis" #设置值
OK
127.0.0.1:6379> get key1
"hello,redis"
127.0.0.1:6379> GETRANGE key1 0 3 #截取字符串[0,3]
"hell"
127.0.0.1:6379> GETRANGE key1 0 -1 #获取全部的字符串
"hello,redis"
127.0.0.1:6379> 

##替换
127.0.0.1:6379> set key2 abcdefg
OK
127.0.0.1:6379> get key2
"abcdefg"
127.0.0.1:6379> SETRANGE key2 2 hello #替换指定位置开始的字符串
(integer) 7
127.0.0.1:6379> get key2
"abhello"
127.0.0.1:6379> SETRANGE key2 2 cd
(integer) 7
127.0.0.1:6379> get key2
"abcdllo"
127.0.0.1:6379> 

##setex(set with expire)	# 设置过期时间
##setnx(set if not exist)	# key不存在再设置（在分布式锁中会常常使用！）
127.0.0.1:6379> setex key3 30 "hello" #设置key3值“hello”，30s后过期
OK
127.0.0.1:6379> ttl key3
(integer) 20
127.0.0.1:6379> setnx mykey "redis"
(integer) 1
127.0.0.1:6379> keys *
1) "mykey"
2) "key2"
3) "key1"
127.0.0.1:6379> setnx mykey "mysql"	#设置mykey存在，则不设置
(integer) 0
127.0.0.1:6379> get mykey
"redis"

##
##mset 设置多个值
##mget
127.0.0.1:6379> mset k1 v1 k2 v2 k3 v3	# 同时设置多个值
OK
127.0.0.1:6379> keys *
1) "k2"
2) "k3"
3) "k1"
127.0.0.1:6379> mget k1 k2 k3	# 同时获取多个值
1) "v1"
2) "v2"
3) "v3"
127.0.0.1:6379> msetnx k1 v1 k4 v4	# msetnx 是一个原子性的操作，要么一起成功，要么一起失败
(integer) 0
127.0.0.1:6379> get k4
(nil)

# 对象
set user:admin{name:zhangsan,age:3}  #设置一个user:admin 对象值为json字符来保存一个对象！

#这里的key是一个巧妙地设计：user:{id}:{filed},如此设计在Redis中是完全OK了！
127.0.0.1:6379> mset user:admin:name zhangsan user:admin:age 2
OK
127.0.0.1:6379> mget user:admin:name user:admin:age
1) "zhangsan"
2) "2"

##getset	#先get然后再set
127.0.0.1:6379> getset db redis # 如果不存在值，则返回nil
(nil)
127.0.0.1:6379> get db
"redis"
127.0.0.1:6379> getset db mongodb # 如果存在值，获取原来的值，并设置新的值
"redis"
127.0.0.1:6379> get db
"mongodb"
127.0.0.1:6379> 

```

**String类似的使用场景：value除了是我们学习的字符串还可以是是数字**

- 计数器
- 统计多单位的数量：uid：xxxx
- 粉丝数
- 对象缓存存储

#### Hash哈希

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [HDEL key field2 [field2\]](https://www.w3cschool.cn/redis/hashes-hdel.html) 删除一个或多个哈希表字段 |
| 2    | [HEXISTS key field](https://www.w3cschool.cn/redis/hashes-hexists.html) 查看哈希表 key 中，指定的字段是否存在。 |
| 3    | [HGET key field](https://www.w3cschool.cn/redis/hashes-hget.html) 获取存储在哈希表中指定字段的值 |
| 4    | [HGETALL key](https://www.w3cschool.cn/redis/hashes-hgetall.html) 获取在哈希表中指定 key 的所有字段和值 |
| 5    | [HINCRBY key field increment](https://www.w3cschool.cn/redis/hashes-hincrby.html) 为哈希表 key 中的指定字段的整数值加上增量 increment 。 |
| 6    | [HINCRBYFLOAT key field increment](https://www.w3cschool.cn/redis/hashes-hincrbyfloat.html) 为哈希表 key 中的指定字段的浮点数值加上增量 increment 。 |
| 7    | [HKEYS key](https://www.w3cschool.cn/redis/hashes-hkeys.html) 获取所有哈希表中的字段 |
| 8    | [HLEN key](https://www.w3cschool.cn/redis/hashes-hlen.html) 获取哈希表中字段的数量 |
| 9    | [HMGET key field1 [field2\]](https://www.w3cschool.cn/redis/hashes-hmget.html) 获取所有给定字段的值 |
| 10   | [HMSET key field1 value1 [field2 value2 \]](https://www.w3cschool.cn/redis/hashes-hmset.html) 同时将多个 field-value (域-值)对设置到哈希表 key 中。 |
| 11   | [HSET key field value](https://www.w3cschool.cn/redis/hashes-hset.html) 将哈希表 key 中的字段 field 的值设为 value 。 |
| 12   | [HSETNX key field value](https://www.w3cschool.cn/redis/hashes-hsetnx.html) 只有在字段 field 不存在时，设置哈希表字段的值。 |
| 13   | [HVALS key](https://www.w3cschool.cn/redis/hashes-hvals.html) 获取哈希表中所有值 |
| 14   | HSCAN key cursor [MATCH pattern] [COUNT count] 迭代哈希表中的键值对。 |

Map集合，key-map，可以对应的值是一个map集合！本质和String类型没有太大区别，还是一个简单的key-value

```bash
127.0.0.1:6379> flushdb 
OK
127.0.0.1:6379> hset myhash field1 hello # set一个具体 key-value
(integer) 1
127.0.0.1:6379> hget myhash field1 # 获取一个字段值
"hello"
127.0.0.1:6379> hmset myhash field1 hello2 field2 word # 设置多个key-value
OK
127.0.0.1:6379> hmget myhash field1 field2 # 获取多个值
1) "hello2"
2) "word"
127.0.0.1:6379> hgetall myhash #获取全部的数据
1) "field1"
2) "hello2"
3) "field2"
4) "word"
127.0.0.1:6379> hdel myhash field2 #删除hash指定的key字段，对应的value值也被删除
(integer) 1
127.0.0.1:6379> hgetall myhash
1) "field1"
2) "hello2"

##
127.0.0.1:6379> hset myhash field2 hello
(integer) 1
127.0.0.1:6379> hlen myhash # 获取hash表的字段数量
(integer) 2
127.0.0.1:6379> hgetall myhash
1) "field1"
2) "hello2"
3) "field2"
4) "hello"
127.0.0.1:6379> hexists myhash field1 # 判断hash中指定字段是否存在
(integer) 1
127.0.0.1:6379> hexists myhash field3
(integer) 0

##
127.0.0.1:6379> hkeys myhash # 只获取哈希的键值
1) "field1"
2) "field2"
127.0.0.1:6379> hvals myhash # 只获取键对应的values值
1) "hello2"
2) "hello"

##
##incr decr 用 hincrby
127.0.0.1:6379> hset myhash field3 5 
(integer) 1
127.0.0.1:6379> hincrby myhash field3 5 #指定增量
(integer) 10
127.0.0.1:6379> hincrby myhash field3 -6 
(integer) 4
127.0.0.1:6379> hsetnx myhash field4 hello #不存在则设置
(integer) 1
127.0.0.1:6379> hsetnx myhash field4 world #存在则不设置
(integer) 0
```

hash变更的数据 user 	name	age，尤其是用户信息之类的，经常变动的信息！hash更适合于对象的存储，string更加适合字符串的存储。

#### List列表

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [BLPOP key1 [key2 \] timeout](https://www.w3cschool.cn/redis/lists-blpop.html) 移出并获取列表的第一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。 |
| 2    | [BRPOP key1 [key2 \] timeout](https://www.w3cschool.cn/redis/lists-brpop.html) 移出并获取列表的最后一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。 |
| 3    | [BRPOPLPUSH source destination timeout](https://www.w3cschool.cn/redis/lists-brpoplpush.html) 从列表中弹出一个值，将弹出的元素插入到另外一个列表中并返回它； 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。 |
| 4    | [LINDEX key index](https://www.w3cschool.cn/redis/lists-lindex.html) 通过索引获取列表中的元素 |
| 5    | [LINSERT key BEFORE\|AFTER pivot value](https://www.w3cschool.cn/redis/lists-linsert.html) 在列表的元素前或者后插入元素 |
| 6    | [LLEN key](https://www.w3cschool.cn/redis/lists-llen.html) 获取列表长度 |
| 7    | [LPOP key](https://www.w3cschool.cn/redis/lists-lpop.html) 移出并获取列表的第一个元素 |
| 8    | [LPUSH key value1 [value2\]](https://www.w3cschool.cn/redis/lists-lpush.html) 将一个或多个值插入到列表头部 |
| 9    | [LPUSHX key value](https://www.w3cschool.cn/redis/lists-lpushx.html) 将一个或多个值插入到已存在的列表头部 |
| 10   | [LRANGE key start stop](https://www.w3cschool.cn/redis/lists-lrange.html) 获取列表指定范围内的元素 |
| 11   | [LREM key count value](https://www.w3cschool.cn/redis/lists-lrem.html) 移除列表元素 |
| 12   | [LSET key index value](https://www.w3cschool.cn/redis/lists-lset.html) 通过索引设置列表元素的值 |
| 13   | [LTRIM key start stop](https://www.w3cschool.cn/redis/lists-ltrim.html) 对一个列表进行修剪(trim)，就是说，让列表只保留指定区间内的元素，不在指定区间之内的元素都将被删除。 |
| 14   | [RPOP key](https://www.w3cschool.cn/redis/lists-rpop.html) 移除并获取列表最后一个元素 |
| 15   | [RPOPLPUSH source destination](https://www.w3cschool.cn/redis/lists-rpoplpush.html) 移除列表的最后一个元素，并将该元素添加到另一个列表并返回 |
| 16   | [RPUSH key value1 [value2\]](https://www.w3cschool.cn/redis/lists-rpush.html) 在列表中添加一个或多个值 |
| 17   | [RPUSHX key value](https://www.w3cschool.cn/redis/lists-rpushx.html) 为已存在的列表添加值 |

redis里面所有的list命令L开头

```bash
#push
127.0.0.1:6379> LPUSH list one two three # 将一个值或多个值，插入到列表头部（左）
(integer) 3
127.0.0.1:6379> LRANGE list 0 -1	#获取list的值
1) "three"
2) "two"
3) "one"
127.0.0.1:6379> RPUSH list right	# # 将一个值或多个值，插入到列表尾部
(integer) 4
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
3) "one"
4) "right"

##pop
127.0.0.1:6379> lpop list # 移除list左边第一个元素
"three"
127.0.0.1:6379> rpop list # 移除list的右边第一个元素
"right"
127.0.0.1:6379> lrange list 0 -1
1) "two"
2) "one"
127.0.0.1:6379> 

##index
127.0.0.1:6379> lindex list 1 #获取下标值
"one"

##Llen
127.0.0.1:6379> Llen list
(integer) 2

##移除指定的值

lrem
127.0.0.1:6379> LPUSH list four
(integer) 3
127.0.0.1:6379> LPUSH list one
(integer) 4
127.0.0.1:6379> LRANGE list 0 -1
1) "one"
2) "four"
3) "two"
4) "one"
127.0.0.1:6379> LREM list 1 one # 移除list集合中指定个数的value
(integer) 1
127.0.0.1:6379> LRANGE list 0 -1
1) "four"
2) "two"
3) "one"
127.0.0.1:6379> LPUSH list four
(integer) 4
127.0.0.1:6379> LREM list 2 four
(integer) 2
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"

##
trim
127.0.0.1:6379> LPush list "hello"
(integer) 1
127.0.0.1:6379> LPush list "hello2"
(integer) 2
127.0.0.1:6379> LPush list "hello3"
(integer) 3
127.0.0.1:6379> LPush list "hello4"
(integer) 4
127.0.0.1:6379> LPush list "hello4"
(integer) 5
127.0.0.1:6379> LTRIM list 1 3 # 通过下表截取指定的长度，这个list已经被改变了，截断了只剩下截取的元素
OK
127.0.0.1:6379> LRANGE list 0 -1
1) "hello4"
2) "hello3"
3) "hello2"
127.0.0.1:6379> 

##
rpoplpush移除右边第一个元素，在另一个列别左头添加这个个元素
127.0.0.1:6379> rpoplpush list anotherlist
"hello2"
127.0.0.1:6379> LRANGE list 0 -1	#查看原来的列表
1) "hello4"
2) "hello3"
127.0.0.1:6379> LRANGE anotherlist 0 -1  #查看新的列表
1) "hello2"

##
Lset 将列表中指定下标的值替换为两外一个值，更新操作
127.0.0.1:6379> FLUSHALL
OK
127.0.0.1:6379> EXISTS list #判断列表是否存在
(integer) 0
127.0.0.1:6379> LPUSH list value1 
(integer) 1
127.0.0.1:6379> LRANGE list 0 0
1) "value1"
127.0.0.1:6379> LSET list 0 item # 如果存在，更新当前下标
OK
127.0.0.1:6379> LRANGE list 0 0
1) "item"
127.0.0.1:6379> LSET list 1 other # 如果列表或元素不存在，则会报错
(error) ERR index out of range
127.0.0.1:6379> 

##
Linsert # 将某个具体的value插入列表的左边或右边
127.0.0.1:6379> rpush mylist "helo"
(integer) 1
127.0.0.1:6379> rpush mylist "worlde"
(integer) 2
127.0.0.1:6379> LRANGE mylist 0 -1
1) "helo"
2) "worlde"
127.0.0.1:6379> linsert mylist before "worlde" "other"
(integer) 3
127.0.0.1:6379> LRANGE mylist 0 -1
1) "helo"
2) "other"
3) "worlde"
127.0.0.1:6379> linsert mylist after "worlde" "newother"
(integer) 4
127.0.0.1:6379> LRANGE mylist 0 -1
1) "helo"
2) "other"
3) "worlde"
4) "newother"
127.0.0.1:6379> 

```

- 它实际是一个双向链表，before Node after，left，right 都可以插入值
- 如果key不存在，创建新的链表
- 如果key存在，新增内容
- 如果移除了所有值，空链表，也代表不存在
- 在两边插入或改动值，效率最高！中间元素，相对来说效率会低一点~

消息排队！消息队列（Lpush Rpop）|栈（Lpush Lpop）

#### Set集合

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [SADD key member1 [member2\]](https://www.w3cschool.cn/redis/sets-sadd.html) 向集合添加一个或多个成员 |
| 2    | [SCARD key](https://www.w3cschool.cn/redis/sets-scard.html) 获取集合的成员数 |
| 3    | [SDIFF key1 [key2\]](https://www.w3cschool.cn/redis/sets-sdiff.html) 返回给定所有集合的差集 |
| 4    | [SDIFFSTORE destination key1 [key2\]](https://www.w3cschool.cn/redis/sets-sdiffstore.html) 返回给定所有集合的差集并存储在 destination 中 |
| 5    | [SINTER key1 [key2\]](https://www.w3cschool.cn/redis/sets-sinter.html) 返回给定所有集合的交集 |
| 6    | [SINTERSTORE destination key1 [key2\]](https://www.w3cschool.cn/redis/sets-sinterstore.html) 返回给定所有集合的交集并存储在 destination 中 |
| 7    | [SISMEMBER key member](https://www.w3cschool.cn/redis/sets-sismember.html) 判断 member 元素是否是集合 key 的成员 |
| 8    | [SMEMBERS key](https://www.w3cschool.cn/redis/sets-smembers.html) 返回集合中的所有成员 |
| 9    | [SMOVE source destination member](https://www.w3cschool.cn/redis/sets-smove.html) 将 member 元素从 source 集合移动到 destination 集合 |
| 10   | [SPOP key](https://www.w3cschool.cn/redis/sets-spop.html) 移除并返回集合中的一个随机元素 |
| 11   | [SRANDMEMBER key [count\]](https://www.w3cschool.cn/redis/sets-srandmember.html) 返回集合中一个或多个随机数 |
| 12   | [SREM key member1 [member2\]](https://www.w3cschool.cn/redis/sets-srem.html) 移除集合中一个或多个成员 |
| 13   | [SUNION key1 [key2\]](https://www.w3cschool.cn/redis/sets-sunion.html) 返回所有给定集合的并集 |
| 14   | [SUNIONSTORE destination key1 [key2\]](https://www.w3cschool.cn/redis/sets-sunionstore.html) 所有给定集合的并集存储在 destination 集合中 |
| 15   | [SSCAN key cursor [MATCH pattern\] [COUNT count]](https://www.w3cschool.cn/redis/sets-sscan.html) 迭代集合中的元素 |

**set中的值是不能重复的**

```bash
##
127.0.0.1:6379> sadd myset "hello" "hello2" # set集合中添加元素
(integer) 2
127.0.0.1:6379> sadd myset "hello3"
(integer) 1
127.0.0.1:6379> smembers myset	# 查看指定set的所有值
1) "hello2"
2) "hello3"
3) "hello"
127.0.0.1:6379> sismember myset "hello" # 查看是否存在某个值
(integer) 1
127.0.0.1:6379> sismember myset "hello4"
(integer) 0

##获取set集合中的个数
127.0.0.1:6379> sadd myset "unexpect"
(integer) 1
127.0.0.1:6379> scard myset
(integer) 4
##
127.0.0.1:6379> srem myset "hello2" "hello3" #移除set中的指定元素
(integer) 2
127.0.0.1:6379> scard myset
(integer) 2
127.0.0.1:6379> smembers myset
1) "unexpect"
2) "hello"

##
set 是无需不重复集合、可以抽随机元素
127.0.0.1:6379> srandmember myset 1# 随机抽选指定个数元素
"unexpect"
127.0.0.1:6379> srandmember myset 
"hello"
127.0.0.1:6379> srandmember myset 
"hello"

##
删除随机的key
127.0.0.1:6379> sadd set "123"
(integer) 1
127.0.0.1:6379> sadd set "123456"
(integer) 1
127.0.0.1:6379> sadd set "666"
(integer) 1
127.0.0.1:6379> sadd set "hello"
(integer) 1
127.0.0.1:6379> smembers set
1) "123"
2) "123456"
3) "666"
4) "hello"
127.0.0.1:6379> spop set	#随机删除集合中的元素
"hello"
127.0.0.1:6379> spop set
"666"
127.0.0.1:6379> sadd set "hello"
(integer) 1
127.0.0.1:6379> sadd set "666"
(integer) 1
127.0.0.1:6379> spop set
"hello"
127.0.0.1:6379> spop set
"123456"
127.0.0.1:6379> smembers set
1) "123"
2) "666"

##
将一个指定的值，移动到两外一个set集合中
127.0.0.1:6379> flushall
OK
127.0.0.1:6379> sadd myset "hello"
(integer) 1
127.0.0.1:6379> sadd myset "world"
(integer) 1
127.0.0.1:6379> sadd myset "zjp"
(integer) 1
127.0.0.1:6379> sadd myset2 "unexpect"
(integer) 1
127.0.0.1:6379> smove myset myset2 "world" # 将一个指定的值移动到另外一个set集合
(integer) 1
127.0.0.1:6379> smembers myset
1) "zjp"
2) "hello"
127.0.0.1:6379> smembers myset2
1) "world"
2) "unexpect"
127.0.0.1:6379> 

##
交集 SINTER
差集 SDIFF
并集 SUNIOON
127.0.0.1:6379> flushall
OK
127.0.0.1:6379> sadd key1 a
(integer) 1
127.0.0.1:6379> sadd key1 b
(integer) 1
127.0.0.1:6379> sadd key1 c
(integer) 1
127.0.0.1:6379> sadd key2 b
(integer) 1
127.0.0.1:6379> sadd key2 c
(integer) 1
127.0.0.1:6379> sadd key2 d
(integer) 1
127.0.0.1:6379> sdiff key1 key2 # 差集
1) "a"
127.0.0.1:6379> sinter key1 key2 # 交集 比如实现共同好友
1) "c"
2) "b"
127.0.0.1:6379> sunion key1 key2 # 并级
1) "a"
2) "c"
3) "d"
4) "b"
127.0.0.1:6379> 

```

微博，A用户将所有关注的人放在一个set集合中。

将它的粉丝也放在一个集合中。

共同关注，共同爱好，推荐好友

#### Zset有序集合

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [ZADD key score1 member1 [score2 member2\]](https://www.w3cschool.cn/redis/sorted-sets-zadd.html) 向有序集合添加一个或多个成员，或者更新已存在成员的分数 |
| 2    | [ZCARD key](https://www.w3cschool.cn/redis/sorted-sets-zcard.html) 获取有序集合的成员数 |
| 3    | [ZCOUNT key min max](https://www.w3cschool.cn/redis/sorted-sets-zcount.html) 计算在有序集合中指定区间分数的成员数 |
| 4    | [ZINCRBY key increment member](https://www.w3cschool.cn/redis/sorted-sets-zincrby.html) 有序集合中对指定成员的分数加上增量 increment |
| 5    | [ZINTERSTORE destination numkeys key [key ...\]](https://www.w3cschool.cn/redis/sorted-sets-zinterstore.html) 计算给定的一个或多个有序集的交集并将结果集存储在新的有序集合 key 中 |
| 6    | [ZLEXCOUNT key min max](https://www.w3cschool.cn/redis/sorted-sets-zlexcount.html) 在有序集合中计算指定字典区间内成员数量 |
| 7    | [ZRANGE key start stop [WITHSCORES\]](https://www.w3cschool.cn/redis/sorted-sets-zrange.html) 通过索引区间返回有序集合成指定区间内的成员 |
| 8    | [ZRANGEBYLEX key min max [LIMIT offset count\]](https://www.w3cschool.cn/redis/sorted-sets-zrangebylex.html) 通过字典区间返回有序集合的成员 |
| 9    | [ZRANGEBYSCORE key min max [WITHSCORES\] [LIMIT]](https://www.w3cschool.cn/redis/sorted-sets-zrangebyscore.html) 通过分数返回有序集合指定区间内的成员 |
| 10   | [ZRANK key member](https://www.w3cschool.cn/redis/sorted-sets-zrank.html) 返回有序集合中指定成员的索引 |
| 11   | [ZREM key member [member ...\]](https://www.w3cschool.cn/redis/sorted-sets-zrem.html) 移除有序集合中的一个或多个成员 |
| 12   | [ZREMRANGEBYLEX key min max](https://www.w3cschool.cn/redis/sorted-sets-zremrangebylex.html) 移除有序集合中给定的字典区间的所有成员 |
| 13   | [ZREMRANGEBYRANK key start stop](https://www.w3cschool.cn/redis/sorted-sets-zremrangebyrank.html) 移除有序集合中给定的排名区间的所有成员 |
| 14   | [ZREMRANGEBYSCORE key min max](https://www.w3cschool.cn/redis/sorted-sets-zremrangebyscore.html) 移除有序集合中给定的分数区间的所有成员 |
| 15   | [ZREVRANGE key start stop [WITHSCORES\]](https://www.w3cschool.cn/redis/sorted-sets-zrevrange.html) 返回有序集中指定区间内的成员，通过索引，分数从高到底 |
| 16   | [ZREVRANGEBYSCORE key max min [WITHSCORES\]](https://www.w3cschool.cn/redis/sorted-sets-zrevrangebyscore.html) 返回有序集中指定分数区间内的成员，分数从高到低排序 |
| 17   | [ZREVRANK key member](https://www.w3cschool.cn/redis/sorted-sets-zrevrank.html) 返回有序集合中指定成员的排名，有序集成员按分数值递减(从大到小)排序 |
| 18   | [ZSCORE key member](https://www.w3cschool.cn/redis/sorted-sets-zscore.html) 返回有序集中，成员的分数值 |
| 19   | [ZUNIONSTORE destination numkeys key [key ...\]](https://www.w3cschool.cn/redis/sorted-sets-zunionstore.html) 计算给定的一个或多个有序集的并集，并存储在新的 key 中 |
| 20   | [ZSCAN key cursor [MATCH pattern\] [COUNT count]](https://www.w3cschool.cn/redis/sorted-sets-zscan.html) 迭代有序集合中的元素（包括元素成员和元素分值） |

在set的基础上，增加了一个值

```bash
127.0.0.1:6379> zadd myset 1 one
(integer) 1
127.0.0.1:6379> zadd myset 2 two
(integer) 1
127.0.0.1:6379> zadd myset 4 four
(integer) 1
127.0.0.1:6379> zadd myset 3 three
(integer) 1
127.0.0.1:6379> zrange myset 0 -1 #默认从小到大排序
1) "one"
2) "two"
3) "three"
4) "four"

##
127.0.0.1:6379> zrangebyscore myset -inf +inf # 从小到大排序
1) "one"
2) "two"
3) "three"
4) "four"

127.0.0.1:6379> zrangebyscore myset -inf +inf withscores # 从小到大排序，附带值
1) "one"
2) "1"
3) "two"
4) "2"
5) "three"
6) "3"
7) "four"
8) "4"
127.0.0.1:6379> zrevrangebyscore myset +inf -inf # 降序排序
1) "four"
2) "three"
3) "two"
4) "one"
127.0.0.1:6379> zrevrangebyscore myset +inf 2 # 降序显示值大于等于2的元素
1) "four"
2) "three"
3) "two"

##
zcard
127.0.0.1:6379> zrem myset "two" # 移除指定的元素
(integer) 1
127.0.0.1:6379> zrange myset 0 -1 
1) "one"
2) "three"
3) "four"
127.0.0.1:6379> zcard myset # 获取集合个数
(integer) 3

##
zcount
127.0.0.1:6379> flushdb
OK
127.0.0.1:6379> zadd myset 1 hello
(integer) 1
127.0.0.1:6379> zadd myset 2 hello2
(integer) 1
127.0.0.1:6379> zadd myset 4 hello4
(integer) 1
127.0.0.1:6379> zcount myset 1 3 # 获取指定区间的成员数量
(integer) 2
127.0.0.1:6379> zcount myset 1 2
(integer) 2
127.0.0.1:6379> zcount myset 1 4
(integer) 3

```

其余的一些API，通过我们的学习，如果工作中有需要，可以去查查官网。

案例思路：set排序，存储班级成绩表，工资表排序！

普通消息，1：重要消息！2：带权重进行判断！

排行榜实时应用

#### 发布订阅命令

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [PSUBSCRIBE pattern [pattern ...\]](https://www.w3cschool.cn/redis/pub-sub-psubscribe.html) 订阅一个或多个符合给定模式的频道。 |
| 2    | [PUBSUB subcommand [argument [argument ...\]]](https://www.w3cschool.cn/redis/pub-sub-pubsub.html) 查看订阅与发布系统状态。 |
| 3    | [PUBLISH channel message](https://www.w3cschool.cn/redis/pub-sub-publish.html) 将信息发送到指定的频道。 |
| 4    | [PUNSUBSCRIBE [pattern [pattern ...\]]](https://www.w3cschool.cn/redis/pub-sub-punsubscribe.html) 退订所有给定模式的频道。 |
| 5    | [SUBSCRIBE channel [channel ...\]](https://www.w3cschool.cn/redis/pub-sub-subscribe.html) 订阅给定的一个或多个频道的信息。 |
| 6    | [UNSUBSCRIBE [channel [channel ...\]]](https://www.w3cschool.cn/redis/pub-sub-unsubscribe.html) 指退订给定的频道。 |

### 三种特殊数据类型

#### geospatial地理位置

地理位置定位，附近的人，打车距离计算

Redis的Geo在Redis3.2版本就推出了

Geo可以推算地理位置的信息，两地之间的距离

http://www.toolzl.com/tools/gps.html

https://jingweidu.51240.com/

```bash
##geoadd 添加地理位置
#规则 两极是无法直接添加的，我们一般会下载城市数据，直接通过java程序导入
#有效的经度从-180度到180度。
#有效的纬度从-85.05112878度到85.05112878度。
127.0.0.1:6379> geoadd china:city 104.10194 30.65984 beijin
(integer) 1
127.0.0.1:6379> geoadd china:city 121.472641 31.231707 shanghai
(integer) 1
127.0.0.1:6379> geoadd china:city 106.50 29.53 chongqin
(integer) 1
127.0.0.1:6379> geoadd china:city 114.05 22.52 shenzhen
(integer) 1
127.0.0.1:6379> geoadd china:city 108.96 34.26 xian
(integer) 1

```

获取当前定位

```bash
##geopos
127.0.0.1:6379> geopos china:city shanghai chongqin # 获取指定的经度纬度
1) 1) "121.47264093160629272"
   2) "31.23170744181923197"
2) 1) "106.49999767541885376"
   2) "29.52999957900659211"

```

计算距离

```bash
#geodist
127.0.0.1:6379> geodist china:city chongqin shenzhen mi # 查看重庆到深圳的距离 单位 英里
"673.8337"
127.0.0.1:6379> geodist china:city chongqin shenzhen km # 查看重庆到深圳的距离 单位 千米
"1084.4275"
```

附近的人（通过附近的人的地址，定位）通过半径来查询

```bash
## georadius
127.0.0.1:6379> georadius china:city 110 30 1000 km # 以经度110，维度30为中心，寻找半径1000km内的城市
1) "chongqin"
2) "beijin"
3) "xian"
4) "shenzhen"
127.0.0.1:6379> georadius china:city 110 30 500 km
1) "chongqin"
2) "xian"
127.0.0.1:6379> georadius china:city 110 30 500 km withdist # 显示其到中心的距离
1) 1) "chongqin"
   2) "341.9374"
2) 1) "xian"
   2) "483.8340"
127.0.0.1:6379> georadius china:city 110 30 500 km withdist withcoord # 显示他人的位置信息
1) 1) "chongqin"
   2) "341.9374"
   3) 1) "106.49999767541885376"
      2) "29.52999957900659211"
2) 1) "xian"
   2) "483.8340"
   3) 1) "108.96000176668167114"
      2) "34.25999964418929977"
127.0.0.1:6379> georadius china:city 110 30 500 km withdist withcoord count 1 # 筛选出指定的结果
1) 1) "chongqin"
   2) "341.9374"
   3) 1) "106.49999767541885376"
      2) "29.52999957900659211"
127.0.0.1:6379> 
```

```bash
## 找出位于指定元素周围的其他元素
#georadiusbymember
127.0.0.1:6379> georadiusbymember china:city beijin 1000 km
1) "chongqin"
2) "beijin"
3) "xian"
127.0.0.1:6379> georadiusbymember china:city beijin 500 km
1) "chongqin"
2) "beijin"

```

```bash
##geohash
#将二维的经纬度转换为一维的字符串
127.0.0.1:6379> geohash china:city shenzhen shanghai
1) "ws10578st80"
2) "wtw3sjt9vs0"

```

底层的实现原理：

Zset

使用Zset命令来操作geo

```bash
127.0.0.1:6379> zrange china:city 0 -1 # 用zrange来查看元素
1) "chongqin"
2) "beijin"
3) "xian"
4) "shenzhen"
5) "shanghai"
127.0.0.1:6379> zrem china:city beijin # 用zrem删除元素
(integer) 1
127.0.0.1:6379> zrange china:city 0 -1
1) "chongqin"
2) "xian"
3) "shenzhen"
4) "shanghai"

```

#### Hyperloglog

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [PFADD key element [element ...\]](https://www.w3cschool.cn/redis/hyperloglog-pfadd.html) 添加指定元素到 HyperLogLog 中。 |
| 2    | [PFCOUNT key [key ...\]](https://www.w3cschool.cn/redis/hyperloglog-pfcount.html) 返回给定 HyperLogLog 的基数估算值。 |
| 3    | [PFMERGE destkey sourcekey [sourcekey ...\]](https://www.w3cschool.cn/redis/hyperloglog-pfmerge.html) 将多个 HyperLogLog 合并为一个 HyperLogLog |

基数：一个集合内不重复的元素

Redis Hyperloglog 用来做基数统计的算法

优点：占用的内存是固定的，2^64不同的元素的技术，需要12kb内存

**网页的UV（一个人访问一个网站多次，但是还是算作一个人）**

传统的方式，set保存用户的id，然后就可以统计set中的元素数量作为标准判断

这个方式如果保存大量的用户id，就会比较麻烦！目的是为了技术，而不是保存用户id

```bash
127.0.0.1:6379> PFadd keys a b c d e f g h i j k l m n
(integer) 1 # 创建第一组元素
127.0.0.1:6379> pfcount keys # 统计keys的基数数量
(integer) 14
127.0.0.1:6379> pfadd keys2 z x c v b n m # 创建第一组元素
(integer) 1
127.0.0.1:6379> pfcount keys2 # 统计keys的基数数量
(integer) 7
127.0.0.1:6379> pfmerge newkeys keys keys2 # 合并两组元素
OK
127.0.0.1:6379> pfcount newkeys # 统计并集newkeys的数量
(integer) 17

```

如果允许容错，那么一定可以使用Hyperloglog

如果不允许容错，就使用Set或自己的数据类型即可

#### Bitmap

位存储

0 或 1

实现布隆过滤器的底层就是通过 bitmap 这种数据结构

统计用户信息，活跃，不活跃，登录，未登录，打卡

使用bitmap来记录周一到周日的打卡

```bash
127.0.0.1:6379> setbit sign 0 1
(integer) 0
127.0.0.1:6379> setbit sign 1 0
(integer) 0
127.0.0.1:6379> setbit sign 2 1
(integer) 0
127.0.0.1:6379> setbit sign 3 0
(integer) 0
127.0.0.1:6379> setbit sign 4 0
(integer) 0
127.0.0.1:6379> setbit sign 5 1
(integer) 0
127.0.0.1:6379> setbit sign 6 0
(integer) 0

```

查看某一天打卡情况

```bash
127.0.0.1:6379> getbit sign 5 
(integer) 1
127.0.0.1:6379> getbit sign 2
(integer) 1
127.0.0.1:6379> getbit sign 1
(integer) 0

```

统计本周打卡天数

```bash
127.0.0.1:6379> bitcount sign # 统计这周的打卡记录  
(integer) 3

```

## 事务

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [DISCARD](https://www.w3cschool.cn/redis/transactions-discard.html) 取消事务，放弃执行事务块内的所有命令。 |
| 2    | [EXEC](https://www.w3cschool.cn/redis/transactions-exec.html) 执行所有事务块内的命令。 |
| 3    | [MULTI](https://www.w3cschool.cn/redis/transactions-multi.html) 标记一个事务块的开始。 |
| 4    | [UNWATCH](https://www.w3cschool.cn/redis/transactions-unwatch.html) 取消 WATCH 命令对所有 key 的监视。 |
| 5    | [WATCH key [key ...\]](https://www.w3cschool.cn/redis/transactions-watch.html) 监视一个(或多个) key ，如果在事务执行之前这个(或这些) key 被其他命令所改动，那么事务将被打断。 |

Redis单条命令是保证原子性的，但是事务不保证原子性

Redis事务本质：一组命令的集合！

一个事务中的所有命令都会被序列化，在事务执行过程中，会按照顺序执行

一次性、顺序、排他性

Redis事务是没有隔离级别的概念

所有的命令在事务中，并没有直接被执行。只有发起执行命令的时候才执行 exec

redis的事务：

- 开启事务：multi
- 命令入队：其它命令
- 执行事务：exec

```bash
127.0.0.1:6379> multi # 开启事务 命令入队
OK
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> get k1
QUEUED
127.0.0.1:6379> set k3 v3
QUEUED
127.0.0.1:6379> exec # 执行事务
1) OK
2) OK
3) "v1"
4) OK


```

> 放弃事务

```bash
##discard
127.0.0.1:6379> multi
OK
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> set k3 v3
QUEUED
127.0.0.1:6379> discard # 取消事务
OK
127.0.0.1:6379> get k3 # 事务队列中命令都不会被执行
(nil)

```

> 编译型异常（代码有问题，命令有错），事务中所有的命令都不会被执行

```bash
127.0.0.1:6379> multi 
OK
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> set k3 v3
QUEUED
127.0.0.1:6379> getset k3 # 错误的命令 
(error) ERR wrong number of arguments for 'getset' command
127.0.0.1:6379> set k4 v4
QUEUED
127.0.0.1:6379> set k5 v5
QUEUED
127.0.0.1:6379> exec #执行时事务报错
(error) EXECABORT Transaction discarded because of previous errors.

```

> 运行时异常（1/0），如果事务队列存在语法性错误，那么执行命令的时候，错误命令抛出异常

```bash
127.0.0.1:6379> set k1 v1
OK
127.0.0.1:6379> multi
OK
127.0.0.1:6379> incr k1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> set k3 v3
QUEUED
127.0.0.1:6379> get k3
QUEUED
127.0.0.1:6379> get k1
QUEUED
127.0.0.1:6379> exec # 第一条命令报错，但是后面依旧正常执行
1) (error) ERR value is not an integer or out of range 
2) OK
3) OK
4) "v3"
5) "v1"

```

#### 锁

**悲观锁**

认为什么时候都会出问题，无论做什么都会加锁

**乐观锁**

认为什么时候都不会出问题，所以不会上锁。更新数据的时候去判断一下，在此期间是否有人修改过这个数据

- 获取version
- 更新的时候比较version

```bash
127.0.0.1:6379> set money 100
OK
127.0.0.1:6379> set out 0
OK
127.0.0.1:6379> watch money 
OK
127.0.0.1:6379> multi
OK
127.0.0.1:6379> decrby money 20
QUEUED
127.0.0.1:6379> incrby out 20
QUEUED
127.0.0.1:6379> exec
1) (integer) 80
2) (integer) 20

```

测试多线程修改值，使用watch可以当作redis的乐观锁操作！

```bash
127.0.0.1:6379> watch money # 监视 money
OK
127.0.0.1:6379> multi
OK
127.0.0.1:6379> decrby money 10
QUEUED
127.0.0.1:6379> incrby out 10
QUEUED
127.0.0.1:6379> exec # 执行之前，另一个线程，修改了mongey，导致事务执行失败
(nil)

```

如果修改失败，获取最新的值就好

```bash
127.0.0.1:6379> unwatch # 先解锁
OK
127.0.0.1:6379> watch money # 获取新的money，再次监视
OK
127.0.0.1:6379> multi
OK
127.0.0.1:6379> decrby money 20
QUEUED
127.0.0.1:6379> incrby out 20
QUEUED
127.0.0.1:6379> exec # 对比监视的值是否发生了变化，如果没有变化，那么可以执行成功，如果变化就会执行失败
1) (integer) 160
2) (integer) 40

```

