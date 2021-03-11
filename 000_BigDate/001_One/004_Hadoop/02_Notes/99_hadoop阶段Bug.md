# hadoop阶段Bug

## A1 HDFS

### 1.1 与Linux命令区别

Linux：`mkdir /opt/jin`

HDFS：`hdfs dfs -mkdir /opt/jin`

start-dfs.sh

stop-dfs.sh

### 1.2 1M

1048576

### 1.3 文件存储目录

/var/hadoop/full/dfs/ -> data -> current -> BP-xxx -> current ->  finalized 

文件中subdir0等，固定名字，但是显示是自己定义的名字。

这是为了避免更改名字路径发生变化的麻烦，直接建立映射关系，固定名字和自定义之间的映射，即使更改名字，路径也不变。

### 1.4 格式化namenode

只能做一遍

datanode变成了0，因为datanode的id还是上一个的集群id。

查看：/var/hadoop/full/dfs/data/current -> cat VERSION

解决：

+ 关闭集群
+ 两种策略
  + 拷贝之前的clusterID(在data的version中)
  + 进入name的version（/var/hadoop/full/dfs/name/current）
  + 换掉

