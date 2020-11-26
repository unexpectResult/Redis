# Redis

Linux

## Nosql

## Redis

### 概述

Redis是什么？

Redis(Remote Dictionary Server),即远程字典服务！

是一个开源的使用ANSI [C语言](https://baike.baidu.com/item/C语言)编写、支持网络、可基于内存亦可持久化的日志型、Key-Value[数据库](https://baike.baidu.com/item/数据库/103728)，并提供多种语言的API

![image-20201108152255819](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108152255819.png)

免费和开源！是当下最热门的NoSQL技术之一！也被称之为结构化数据库！

### Redis能干嘛？

1、内存存储，持久化（内存中是断电即失，所以持久化很重要（rdb、aof））

2.、效率高，可以用于告诉缓存

3、发布订阅系统

4、地图信息分析

5、计时器、计数器（浏览量！）

6、。。。。。。

### 特性

1.多样的数据类型

2.持久化

3.集群

4.事务

。。。。。。

### 学习中需要用到的东西

1.官网：https://redis.io/

2.中文网:http://www.redis.cn/

3.下载地址:https://www.redis.io/

Redis推荐都在Linux服务器上搭建的，基于Linux学习！

### Windows安装

下载地址:https://github.com/tporadowski/redis/releases

打开redis-server.exe

![image-20201108154125526](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108154125526.png)

打开redis-cli.exe

![image-20201108154228550](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108154228550.png)

### Linux安装

1.下载安装包

一般安装在 /opt下

![image-20201108155247483](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108155247483.png)

![image-20201108155409870](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108155409870.png)

2.需要跟新GCC

下载地址:http://ftp.gnu.org/gnu/gcc/gcc-10.2.0/ 

centos7redis6.0以上报错

```
In file included from server.c:30:0:
server.h:1022:5: error: expected specifier-qualifier-list before ‘_Atomic’
     _Atomic unsigned int lruclock; /* Clock for LRU eviction */
```

解决方法：更新gcc

```
sudo yum install centos-release-scl
sudo yum install devtoolset-7-gcc*
scl enable devtoolset-7 bash
```

3.执行make

![image-20201108201242338](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108201242338.png)

4.执行make install

![image-20201108201706489](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108201706489.png)

redis的默认安装路径'usr/local/bin'

![image-20201108201730704](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108201730704.png)

5.将redis解压目录下的redis.config 拷贝到自己创建的myredisconfig的目录下

![image-20201108201905928](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108201905928.png)

6.注、redis默认不是后台启动的

打开redis.conf

![image-20201108202205733](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108202205733.png)

7.通过配置文件启动redis服务

![image-20201108202502035](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108202502035.png)

8.使用redis-cli连接测试

![image-20201108202802541](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108202802541.png)

9.查看redis的进程是否开启

![image-20201108202849782](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108202849782.png)

10.关闭Redis服务

![image-20201108202939170](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108202939170.png)

11.再次查看进程是否存在

![image-20201108203013090](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201108203013090.png)