# Redis三大问题

### **缓存穿透（redis中查不到）**

方案一 	缓存空数据

方案二	布隆过滤器

![image-20201118133534846](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201118133534846.png)

### **缓存击穿（某一时期访问某个key访问量大，缓存过期）**

方案一	设置热点数据

方案二	加互斥锁

![image-20201118211537218](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201118211537218.png)

**redisson分布式锁实现原理图**![image-20201118225602979](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201118225602979.png)

**主机崩了怎么办？**

如果此时`redis master`节点宕机，为保证集群可用性，会进行`主备切换`，`slave`变为了`redis master`。`B客户端`在新的`master`节点上加锁成功，而`A客户端`也以为自己还是成功加了锁的。

至于解决办法嘛，目前看还没有什么根治的方法，有效算法Redis之父创建的**Redlock算法**。

此时就会导致同一时间内多个客户端对一个分布式锁完成了加锁，导致各种脏数据的产生。

### **缓存雪崩	（缓存集体过期或失效）**

双十一：停掉一些服务，（保证主要的服务可用！）

退款服务停用，遇到退不掉服务繁忙

方案一：redis高可用

方案二：限流降级

方案三：数据预热

