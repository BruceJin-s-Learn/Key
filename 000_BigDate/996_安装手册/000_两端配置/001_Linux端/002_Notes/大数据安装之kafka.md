# 大数据安装之kafka

## A1 解压

tar -zxf kafka_2.12-0.11.0.3.tgz

## A2 修改配置

config 里面的 server.properties



![image-20210320113004972](%E5%A4%A7%E6%95%B0%E6%8D%AE%E5%AE%89%E8%A3%85%E4%B9%8Bkafka.assets/image-20210320113004972.png)



## A3 发送到其他节点

修改id

scp -r kafka_2.12-0.11.0.3 root@D-node02:`pwd`

config 下 server.properties 的 id 每个节点不一样

A4 