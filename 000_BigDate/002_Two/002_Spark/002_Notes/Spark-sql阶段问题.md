# Spark-sql阶段问题

## 1.了解Parquet



存储后：

<img src="Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316103750770.png" alt="image-20210316103750770" style="zoom:50%;" />

生成snappy压缩格式文件（中规中矩）

## 2.公式rdd\DF\DS三者

dataset=RDD+schema

dataFrame=dataset(row)



<img src="Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318205518966.png" alt="image-20210318205518966" style="zoom:50%;" />

1. RDD

1. 1. 后加.toDS
   2. 返回去是ds名后加 .rdd

2. DF

1. 1. df名 as[类型如User]
   2. 返回去：ds.toDF

## 3.不同session表的访问

放到global_temp全局库中

## 4.升级指南

Kafka

HDFS

数据迁移

## 5.schama

数据结构信息

元数据

## 6.spark对话加载数据

源码：org/apache/spark/sql/Dataset.scala

代码例子（107-112）：

```scala
There are typically two ways to create a Dataset. The most common way is by pointing Spark
 * to some files on storage systems, using the `read` function available on a `SparkSession`.
 * {{{
 *   val people = spark.read.parquet("...").as[Person]  // Scala
 *   Dataset<Person> people = spark.read().parquet("...").as(Encoders.bean(Person.class)); // Java
 * }}}
```

1. 常用：

   sparksession.read().textFile("path")

   对话名+read()方法+存储系统上的某些文件

2. 现有数据集上可用的转换来创建数据集

   ...源码查看
## 7. spark-sql特点



## 8.公司常用数据格式

<img src="Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316104841311.png" alt="image-20210316104841311" style="zoom:50%;" />

##    9.文件压缩

配置

重启集群

## 10.连接mysql

jar -> driver

司机开车去目的地有路径 url

到了需要出入许可证：名字+密码

## 11.spark-sql默认并行度

200个task（199.0从0.0开始）

## 12.连接hive

### 报错：![image-20210316115958257](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316115958257.png)

### 解决：

1.<img src="Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316120038243.png" alt="image-20210316120038243" style="zoom:50%;" />

可能导致每次都识别为HDFS路径，所以放外面

<img src="Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316165645867.png" alt="image-20210316165645867" style="zoom:50%;" />

![image-20210316120206924](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316120206924.png)

2.会再报错，需要在hive中先创建库

![image-20210316120439498](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316120439498.png)

## 13.必须写

![image-20210316120330178](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316120330178.png)

## 14.序列化问题

对象 - 状态信息，存不了状态，只能存数据，把数据存储起来或者通过网络io，就需要序列化。

序列化，Java生成对象的方式之一：

+ new
+ 反射（.class）
+ 序列化
+ clone

## 15.static修饰的属性

<img src="Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316162622066.png" alt="image-20210316162622066" style="zoom:50%;" />



## 16.函数

<img src="Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316163917122.png" alt="image-20210316163917122" style="zoom:50%;" />

## 17.注意参数类型不匹配

![image-20210316170757480](../../../996_%E5%AE%89%E8%A3%85%E6%89%8B%E5%86%8C/000_%E4%B8%A4%E7%AB%AF%E9%85%8D%E7%BD%AE/001_Linux%E7%AB%AF/002_Notes/image-20210316170757480.png)

![image-20210316170827897](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210316170827897.png)

## 18.自定义

累加器：6种

UDAF：8种

## 19.连接mysql出错

报错：

<img src="Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210317165000835.png" alt="image-20210317165000835" style="zoom:50%;" />

原因：

<img src="Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210317165127894.png" alt="image-20210317165127894" style="zoom:50%;" />

解决：

建立person（缺少的，找不到的）临时视图

## 20.实现UDF

UD[A]F结合官网（）

Java：

会话.udf().register注册一个自定义函数（名,UDFN,returnType）

在会话.sql种写sql语句时，运用函数统计查询，如：

`spark.sql("select name,age,nameLenPlusAge(name,age) as udf from person").show();`

Scala：

会话.udf.register("name", (参数)=>{方法体})

调用与Java相同

## 21.实现UDAF

**8步**

上下4步

**上**

input

buffer

返回类型

输入输出对应关系

**下**

init

update

merge

evaluate



## 22.数据源

**file**

RDD

json：方便（k，v）

parquet：存在一定压缩比率，效率高

CSV：“，”分割（）textfile

**other**（jar包）

mysql

hive（元数据+hive --）与（site.xml的有）（enable...）



## 23.相关网站

sql：http://spark.apache.org/docs/2.4.6/api/sql/index.html#initcap

## 24.explain()和show()

explain显示出物理计划，sql执行顺序

![image-20210318092756236](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318092756236.png)

## 25.hive中找不到建的表

配置必须放classes中

![image-20210318102518078](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318102518078.png)

```java
session.sql("drop database if exists spark");
        session.sql("create database spark");
        session.sql("drop table if exists sales");
        session.sql("use spark");
        session.sql("create table if not exists sales (date string,category string, sales_sum int) " +
                "row format delimited fields terminated by '\t'");
        session.sql("load data local inpath 'src/main/resources/data/sales.txt' into table sales");
```

## 26.找不到库和表

报错：

![image-20210318102743499](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318102743499.png)

解决：

```java
session.sql("use spark");
```

![image-20210318102818083](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318102818083.png)

## 27.创建DF

1. 通过Spark数据源进行创建

   1. spark支持的文件数据源格式

   ![image-20210318200237244](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318200237244.png)

   2. 对比hive支持的

2. 从一个存在的RDD进行转换

3. 从hive table进行查询返回

## 28.视图view

createOrReplaceTempView，创建不重复的临时视图，以便进行sql操作，只能查不能改，table可改。

## 29.普通临时表与全局临时表

![image-20210318203826437](Spark-sql%E9%98%B6%E6%AE%B5%E9%97%AE%E9%A2%98.assets/image-20210318203826437.png)

新的session无法访问普通临时表。

解决：createOrReplaceGlobalTempView("emp")

访问时：.sql("select * from global_temp.emp")（注意限定名称）

## 30.DSL

DF提供的一个特定领域语言（domain-specific language,DSL）

不需要创建临时表。

用df的方法（在sparkshell中输入df.）出来的方法中有select，则df.select("参数")可获得sql查询的效果。

涉及运算:

每列都必须用`$`进行引用，或采用引号表达式：单引号+字段名

df.select($"age"+1)

df.select('age + 1)



