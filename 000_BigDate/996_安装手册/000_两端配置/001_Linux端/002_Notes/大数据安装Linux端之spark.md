# 大数据安装Linux端之spark

## A1 Standalone测试安装

### 1.1 解压

#### 1.1.1 前提

hadoop、Java jdk

#### 1.1.2 解压

`tar -zxvf spark-2.4.6-bin-without-hadoop.tgz`

可加`-C`指定解压目录

### 1.2 改名

`mv spark-2.4.6-bin-without-hadoop.tgz spark-2.4.6`

### 1.3 修改conf

进入安装包的`conf`目录下

`mv slaves.template slaves`配置worker节点（即从节点）

如：<img src="%E5%A4%A7%E6%95%B0%E6%8D%AE%E5%AE%89%E8%A3%85Linux%E7%AB%AF%E4%B9%8Bspark.assets/image-20210305220623803.png" alt="image-20210305220623803" style="zoom:50%;" />

### 1.4 测试启动

