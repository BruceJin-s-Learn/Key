# Kylin相关问题

## A1 基础知识

### 1.1 数仓:vs:数据库

|      | 数据库 | 数仓 |
| ---- | ------ | ---- |
| 英文 | DB     | BW   |
| 面向 | 事务   | 分析 |



### 1.2 OLAP:vs:OLTP



### 1.3 压缩

比例和性能，比例大，计算慢，比如十年前的数据，不经常用，所以可以用最大的压缩比。

### 1.4 数据集市

比仓库小一点，但更精。

![数据集市](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/%E6%95%B0%E6%8D%AE%E9%9B%86%E5%B8%82.png)

### 1.5 数仓分层

#### why:

+ 复杂问题简单化
+ 隔离原始数据（后期统计和真实数据解耦）
+ 数据复用性提高
+ 数据结构更清晰
+ 统一数据口径

#### 优缺点

优点

+ 效率高

缺点

+ 预计算

+ 占空间

#### 图解

![image-20210329114755160](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210329114755160.png)

#### 实现

![数仓实现](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/%E6%95%B0%E4%BB%93%E5%AE%9E%E7%8E%B0.png)

#### 位置

![数仓位置](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/%E6%95%B0%E4%BB%93%E4%BD%8D%E7%BD%AE-1617007200393.png)

### 1.6 维度和度量

维度：分门别类，groupBy后的

度量：具体大小，考量值，前面的结果

### 1.7 维度表和事实表

维度表：分门别类

事实表：具体

两者有关联关系

### 1.8 cube和cuboid

#### Cuboid

给定一个数据模型，我们可以对其上的所有维度进行组合。对于**N个维度**来说，组合的所有可能性共有`2^N` 种。对于每一种维度的组合，将度量做聚合运算，然后将运算的结果保存为一个物化视图。

#### Cube

所有维度组合的`Cuboid`作为一个整体，即Cuboid物化视图的集合。

#### 图解

![cube&cuboid](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/cube&cuboid.png)



### cube segment

模型

### 1.9 数据模型

#### 星型模型

大数据用的多，查询快效率高

#### 雪花模型

减少冗余

#### 对比

|          | 星型模型 | 雪花模型 |
| -------- | -------- | -------- |
| 数据总量 | 多       | 少       |
| 冗余度   | 高       | 低       |
| 可阅读性 | 相对容易 | 相对差   |
| 表的个数 | 少       | 多       |
| 查询效率 | 快       | 慢       |
| 可拓展性 | 差       | 好       |



## A2 Kylin原料

开源的分布式分析引擎，提供亚秒级的交互式分布能力。

数据源：hive

存储：HBase（目前最新版进行了替换，parquet）

## A3 做法

### 3.1 原理

核心思想：Cube预计算

理论基础：空间换时间，把高复杂的聚合计算，多表连接等操作转换成对预计算结果的查询。

### 3.2 技术架构



## A4 kylin安装

hadoop：2.6.5

hive：1.2.1

hbase：1.3.5

kylin：2.5.0

![image-20210329171658432](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210329171658432.png)

## A5 

![image-20210329200845257](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210329200845257.png)



![image-20210329200850175](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210329200850175.png)

## A6 时区问题

换算时间戳会有时区问题

所以用WebUI

![image-20210330144646508](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210330144646508.png)

![image-20210330150709804](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210330150709804.png)



## A7 HTable

HTable代表HBase中的一张表，但存到HDFS中的数据。

subdir中，blockID，实际存储路径，文件。

## A8 失败

重新尝试 resume

页面中

![image-20210330151008738](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210330151008738.png)

或者命令

![image-20210330151531833](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210330151531833.png)

## A9 报错2181，appct，connect等

重试，连接，资源不够？

挂掉了？

在重试连接，资源问题重新 resume

## A10 全量Or增量

model有没有选 分区日期

选了就是增量（符合历史数据日益增长的要求）

没选就是全量（数据全，查起来快）

![image-20210330155709845](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210330155709845.png)

## A11 查看资源命令

`free`

## A12 编辑构建cube

![image-20210330161521574](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210330161521574.png)

已经构建cube不能再编辑构建（Edit）。

解决：clone

## A13 增量构建合并机制

### why

增量构建的Cube每天都可能有新的增量。日益剧增，Cube可能会包含上百个Segment，查询性能会受到影响。

### 解决

合并segment：可手动，可自动。

在Web GUI中选中需要进行Segments合并的Cube，单击
Action→Merge，然后在对话框中选中需要合并的Segment，可以同时合并多个Segment，但是这些Segment必须是连续的。

### 自动合并

![自动合并机制](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/%E8%87%AA%E5%8A%A8%E5%90%88%E5%B9%B6%E6%9C%BA%E5%88%B6.png)

### 数据持续更新

数仓里面的数据拿取的是数据库中某个时间的状态数据，不可能像Mysql中数据一样频繁的更新。

因为数据拉取的过程是有延时性的。T+1业务中，每日12点之后开始计算前一天的数据。

然后数据已经随着时间流式计算了。但是数据库中同步的数据其实是错误或者还需要修改的数据。

那么从kylin的角度来看，把对应日期的数据重新同步后重新计算。

对应日增情况，就是根据时间容忍度N，刷新前N个segment的数据，build新增的segment数据，如果设置了自动合并机制，或者不小心进行了不合适的合并情况下，可能造成大量数据的重复计算。

![image-20210330221217782](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210330221217782.png)

当最新数据进来时，刷新过去7天的数据，但是，这数据中有有一部分在之前的segment(94)中。有大量数据重复计算了。

因为segment是一个整体，无法拆分。所以只能全部更新达到数据持续更新的效果。

**缺点：**

日增数据建立segment。1天一个，在不合适的合并条件下，可能产生比较差的执行效率。

**解决：**

将时间范围放大，将segment的范围调整成N或者N+1, 以7天为例，持续更新7天的数据。

![image-20210330221311014](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210330221311014.png)

**手动刷新：refresh**

![image-20210330172537055](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210330172537055.png)

**问题：**

即使将时间范围放大，但是到达一定的临界点也会导致要refresh很多数据，使执行效率变差，这是可以采用手动合并。

## A14 数据持续更新

场景：

数仓里面的数据拿取的是数据库中某个时间的状态数据，不可能像Mysql中数据一样频繁的更新。

因为数据拉取的过程是有延时性的。T+1业务中，每日12点之后开始计算前一天的数据。

然后数据已经随着时间流式计算了。但是数据库中同步的数据其实是错误或者还需要修改的数据。



解决：refresh

![image-20210330172537055](Kylin%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210330172537055.png)



## A15 事实表和维度表&维度退化

事实表

维度表

维度退化：将维度表和事实表合并，因为这个维度表时常被访问，两者本来就存在依赖，所以退化来减少联查，提高查询性能。

## A16 

