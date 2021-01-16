# sqoop

## 1.what

### 1.1 奥义

含义：sql to hadoop

实现：关系型数据库到HDFS的互相转换

+ hive与传统数据库之间进行数据传递的工具

### 1.2 原理

将导入导出命令翻译成`mapreduce`程序来实现

在翻译出的`mapreduce`中主要是对`inputformat`和`outputformat`进行定制。

+ > MapReduce：
  >
  > + 一种编程模型，用于大规模数据集（大于1TB）的并行运算。
  >
  > + 主要思想：map（映射）、reduce（归约）
  > + 特点：方便了程序员在不会分布式并行编程的情况下，将自己的程序运行在分布式系统上。
  > + 实现方式：指定一个map函数，用来把一组键值对映射成一组新的键值对，指定并发的reduce函数，用来保证所有映射的键值对中的每一个共享相同的键组。
  >
  > https://baike.baidu.com/item/MapReduce/133425?fr=aladdin



## 2.安装

下载

+ 官网下载.tar.gz包，导入虚拟机中

解压

+ `tar -zxvf sqoop-xxx -C /opt/module`

+ 解压后改名`mv sqoop-xxx sqoop`

## 3.配置

+ 运行：

  + 与zookeeper一样，与运行配置需修改。在`conf`中，将`sqoop-env-template.sh`改为`sqoop-env.sh`。

  + ```bash
    #重命名配置文件
    mv sqoop-env-template.sh sqoop-env.sh
    ```

+ 修改配置文件

  + ```bash
    #修改配置文件
    vim sqoop-env.sh
    ---------------------
    export HADOOP_COMMON_HOME=/opt/module/hadoop-2.7.2
    export HADOOP_MAPRED_HOME=/opt/module/hadoop-2.7.2
    export HIVE_HOME=/opt/module/hive
    export ZOOKEEPER_HOME=/opt/module/zookeeper-3.4.10
    export ZOOCFGDIR=/opt/module/zookeeper-3.4.10
    export HBASE_HOME=/opt/module/hbase
    ```

+ 拷贝JDBC配置

  + ```bash
    cp mysql-connector-java-5.1.27-bin.jar /opt/module/sqoop-1.4.6.bin_hadoop-2.0.4-alpha/lib/
    ```

+ 验证sqoop

  + ```bash
    
    ```

  + ![image-20210112222221095](sqoop.assets/image-20210112222221095.png)

  + 链接sqoop必有得启动

## 4.使用