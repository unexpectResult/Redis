# Redis持久化

### RDB

rdb的保存文件dump.rdb

在主从配置中，rdb就是备用了

![image-20201109204223795](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201109204223795.png)

> **触发rdb操作的机制**

1.save的规则满足的情况下，会自动触发rdb规则

2.执行flushall命令，也会触发我们的rdb规则！

3.推出redis，也会产生redis文件！

备份就自动生产一个dump.rdb

> **如何恢复rdb文件**

1.将rdb文件放在我们redis启动目录就可以，redis启动的时候会自动检查dump.rdp回复其中的数据

2.查看需要存在的位置

```bash
127.0.0.1:6379> config get dir
1) "dir"，
2) "/usr/local/bin" # 如果在这个目录下存在dump.rdb文件，redis启动就会自动恢复里面的数据
```

> **几乎就他自己默认的配置就够用了，但是我们还是需要去学习**

**有点：**

1.适合大规模的数据恢复 dump.rdb

2.对数据的完整性要求不高

**缺点：**

1.需要一定的时间间隔进行操作。如果redist意外宕机了，可能最后一次修改的数据就没有了

2.fork进程的时候，会占用一定的内容空间

### AOF

Aof保存的文件 appendonly.aof

![image-20201109210128897](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201109210128897.png)

> **开启AOF**

appendonly no改为yes

重启redist就可以生效了

aof默认就是文件的无限追加，文件会越来越大

![image-20201109213638510](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201109213638510.png)

如果aof文件大于64mb，fork一个新的进程将文件进行重写



如果这个aof文件出现问题，这时候是启动不了的，这时需要修复aof这个文件

redis给我们提供了一个工具 **redis-check-aof --fixe**

```bash
[root@localhost bin]# redis-check-aof --fix appendonly.aof
0x               4: Expected prefix '$', got: 'q'
AOF analyzed: size=89, ok_up_to=0, diff=89
This will shrink the AOF from 89 bytes, with 89 bytes, to 0 bytes
Continue? [y/N]: y
Successfully truncated AOF

```

优点：

1.每一次修改都同步

2.默认每秒同步一次，可能丢失一秒的数据

3.从不同步，效率是最高的

缺点：

1.相对于数据文件来说，aof远远大于rdb，修复数据也比rdb慢！

2.aof运行效率也要比rdb慢