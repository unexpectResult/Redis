# Redis3

我们要使用Java来操作Redis

Jedis是Redis官网推荐的的java连接开发工具！是

是使用Java操作Redist中间件！

## 测试

1.导入对应的依赖

```xml
<!--导入Jedis的包-->
    <dependencies>
        <!-- https://mvnrepository.com/artifact/redis.clients/jedis -->
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
            <version>3.3.0</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/com.alibaba/fastjson -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.73</version>
        </dependency>

    </dependencies>
```

2.编码测试：

- 连接数据库
- 操作命令
- 断开连接

```java
public static void main(String[] args){
    //1.new Jedis 对象即可
    Jedis jedistest = new Jedis("127.0.0.1",6379);
    //Jedis 所有的命令就是我们之前学习的所有指令
    System.out.println(jedistest.ping());
}
```

![image-20201109165407635](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\image-20201109165407635.png)

### 常用的APIS

String

List

Set

Hash

Zset

```java
package com.unexpect;

import redis.clients.jedis.Jedis;

import java.util.Set;

public class TestPing {

    public static void main(String[] args){
        //1.new Jedis 对象即可
        Jedis jedistest = new Jedis("127.0.0.1",6379);
        //Jedis 所有的命令就是我们之前学习的所有指令
        System.out.println(jedistest.ping());
        System.out.println("清空数据库"+jedistest.flushAll());
        System.out.println("判断某个键是否存在："+jedistest.exists("username"));
        System.out.println("新增<'username','unexpect'>的键值对："+jedistest.set("username","unexpect"));
        System.out.println("新增<'password','123456'>的键值对："+jedistest.set("password","123456"));
        System.out.println("系统中所有的键如下：");
        Set<String> keys = jedistest.keys("*");
        System.out.println(keys);

        System.out.println("删除键password："+jedistest.del("password"));
        System.out.println("判断键password是否存在："+jedistest.exists("password"));
        System.out.println("查看键username所存储的值的类型："+jedistest.type("user"));
        System.out.println("随即返回key空间的一个："+jedistest.randomKey());
        System.out.println("重命名key"+jedistest.rename("username","newname"));
        System.out.println("取出改后的name"+jedistest.get("newname"));
        System.out.println("按索引查询"+jedistest.select(0));
        System.out.println("删除当前选择书库中的所有数据"+jedistest.flushDB());
        System.out.println("返回当前数据库中key的数目："+jedistest.dbSize());
        System.out.println("删除所有数据库中的所有key"+jedistest.flushAll());

    }


}

```

> jedis执行事务操作

```java
package com.unexpect;

import com.alibaba.fastjson.JSONObject;
import redis.clients.jedis.Jedis;
import redis.clients.jedis.Transaction;

public class TestTX {
    public static void main(String[] args) {
        Jedis jedis = new Jedis("127.0.0.1", 6379);
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("hello","world");
        jsonObject.put("name","unexpect");
        jedis.flushAll();
        //开启事务
        Transaction multi = jedis.multi();
        String result = jsonObject.toJSONString();


        try{
            multi.set("user1",result);
            multi.set("user2",result);
            // int i = 1/0; //代码抛出事务异常，执行失败
            multi.exec();//执行事务！
        }catch (Exception e){
            multi.discard();//放弃事务
            e.printStackTrace();
        }finally {
            System.out.println(jedis.get("user1"));
            System.out.println(jedis.get("user2"));
            jedis.close();//关闭jedis
        }

        jedis.close();
    }
}

```

