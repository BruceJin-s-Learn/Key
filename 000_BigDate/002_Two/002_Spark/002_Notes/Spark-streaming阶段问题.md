# Spark-streaming阶段问题

## A1 热词

![image-20210318103900013](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318103900013.png)

官网特定第三个

## A2 事务

ACID

原子性

## A3 操作对象

RDD

DS&DF

DStream

## A4 OOM

job执行的时间大于batchInterval问题：

job执行时间和receiver时间，数据堆积问题

<img src="Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318110512464.png" alt="image-20210318110512464" style="zoom:50%;" />

## A5 streamingContext源码

![image-20210318114955719](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318114955719.png)

优雅关闭

## A6 关于master数量

报错：

![image-20210318115026540](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318115026540.png)

原因：

![image-20210318115109787](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318115109787.png)

解决：

至少写2，一个接收一个算

![image-20210318115145650](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318115145650.png)



## A7 流的语义

收集数据时的方式

精确一致性，一条一条收集在receiver  task时



## A8 时间显示原因

源码：

![image-20210318144659199](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318144659199.png)

效果：

![image-20210318145047363](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318145047363.png)

代码：

```scala
result.print()
```

## A9 查看监听端口

netstat -tunlp | grep 9999

yum install net-tools

## A10 状态保留完成容错

报错：

![image-20210318163351959](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318163351959.png)

解决：

```java
SparkConf conf = new SparkConf().setMaster("local[2]").setAppName("javas");

JavaSparkContext jsc = new JavaSparkContext(conf);
JavaStreamingContext jssc = new JavaStreamingContext(jsc, Durations.seconds(5));
//添加下面这句
jssc.checkpoint("path");
```

## A11 开窗函数数据完整性问题

跟的参数，需要注意，否则导致数据完整性问题

1.如果设置15s的数据，5s滑动

2.窗口长度，滑动间隔

##  A12 数据丢失和数据重复消费

数据丢失发生在，提交偏移量之后，计算完成之前。

WAL机制：在数据备份的时候多加一份给HDFS（高延迟），当driver发生异常情况宕机后，导致任务失败再次重启时，先去检测HDFS上的数据，有则计算，无则从zookeeper上读取偏移量，继续往后计算数据。（可能导致数据重复消费）

首先HDFS是高延迟的，并且在此基础上，可能发生数据重复消费的问题。

总结：WAL机制不光影响性能，还可能造成数据重复消费。



## A13 block并行度

![image-20210319104154979](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210319104154979.png)



## A14 数据的处理类型

处理方式角度：

1. 流式（streaming）处理
2. 批量（batch）处理

处理延迟长短：

1. 实时：毫秒级别
2. 离线：小时Or天

sparkStreaming：准实时（秒，分钟），微批

## A15 针对版本迁移

1： 

![image-20210320080338725](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210320080338725.png)

2：

![image-20210320084956193](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210320084956193.png)

3：

![image-20210320085032194](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210320085032194.png)



## A16 kafka版本分水岭

0.10之前

0.8是zk管理offset

关于offset：smallest、largest

0.10之后

0.11是自己管理offset

关于offset：earliest、latest



创建方式不同

消费和位置策略不同

## A17 升级kafka

删除zk中：

![image-20210320100541784](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210320100541784.png)

五个文件

## A18 关于offset

拿出offset：

老版本：

![image-20210320102116183](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210320102116183.png)

提交：

老版本：

![image-20210320102200902](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210320102200902.png)

新版本

手动提交解决问题：自动从两方面：时间和，数据丢失和数据重复消费。

关于offset存储：

1. checkpoint 太笨重，存了一些无关紧要的东西，无法迭代开发

2. kafka本身，万一kafka挂掉（不支持事务）（__consumer_offsetes_num）中

3. your own data store

## A19 位置策略

**3种**

spark和kafka安装在一起：用preferBrokers

大多数情况满足计算偏向一致：preferConsistent

特殊情况：pregerFixed 需要执行topicPartition和Host的对应map关系

## A20 消费策略

**3种**

Subscribe   订阅-->主题topic

SubscribePattern

Assign

![image-20210320110613964](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210320110613964.png)

## A21 查看状态，偏移量

<img src="Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210320114354238.png" alt="image-20210320114354238" style="zoom:67%;" />



## A22 幂等操作

幂等的意味着对同一URL的多个请求应该返回同样的结果。

幂等（idempotent、idempotence）是一个数学或计算机学概念，常见于抽象代数中。

　　幂等有一下几种定义：

　　对于单目运算，如果一个运算对于在范围内的所有的一个数多次进行该运算所得的结果和进行一次该运算所得的结果是一样的，那么我们就称该运算是幂等的。比如绝对值运算就是一个例子，在实数集中，有abs(a)=abs(abs(a))。

　　对于双目运算，则要求当参与运算的两个值是等值的情况下，如果满足运算结果与参与运算的两个值相等，则称该运算幂等，如求两个数的最大值的函数，有在在实数集中幂等，即max(x,x)　=　x。

## A23 理解SparkStreaming

官网描述：

对比



特点深入



容错

​	语义

​	checkpoint

kafka

![image-20210320143802946](Spark-streaming%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210320143802946.png)

## A24 关于事务

mysql

日志

​	开始begin

​	提交commit

​	回滚rollback

redis

队列

​	标记multi

​	执行exec

​	取消discard（不能回滚）

## A25 spark中checkpoint

1. updateStateByKey -> batch独立

2. DriverHA getOrCreate(offset )
3. 优化后的window

