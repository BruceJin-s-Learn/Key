# shop

OAC破解技术

行为验证



## .问题

### 1.zookeeper未连接成功

**解决思路**

【1】虚拟机中

+ 是否启动 zookeeper 服务

  + ```bash
    1.#查看状态
    #zookeeper的bin中
    ./zkServer.sh status
    #正确结果：mode:standelone(单机)
    
    2.#查看进程
    pa aux|grep zookeeper
    #正确结果：有进程
    
    3.#启动
    ./zkServer.sh start
    #正确结果：STARTED
    ```

+ 必须copy `zoo-simple.cfg `为` zoo.cfg`，因为zookeeper默认启动`zoo.cfg`文件。

【2】代码中

+ 配置文件`application.yml`中 zookeeper 地址和端口是否写对

  + ```shell
    #查看ip
    ip addr
    ```

  + cmd中ping查看是否能访问

+ 启动类中是否写注解`@EnableDubbo`（apache的）

+ 关闭防火墙

【3】版本问题

+ ```xml
  <dubbo-version>2.7.5</dubbo-version>
  <!-- zookeeper版本是3.5.5,这里是客户端版本，不可过高，否则可能连接不上 -->
  <curator-version>4.2.0</curator-version>
  ```



### 2.idea启动类问题

一个项目中默认只能放6个启动类。

为了保证当项目多的时候，都能放得下，保存启动类，当启动类多了之后也不会覆盖之前得。

固定启动类：

edit中，save configuration对启动类进行保存。



### 3.配置数据源

**报错信息：**

`Failed to configure a DataSource: 'url' attribute is not specified and no em`

无法配置DataSource：未指定'url'属性，也无法配置嵌入数据源。

**解决：**

在启动类的注解`@SpringBootApplication`后加入

`(exclude= {DataSourceAutoConfiguration.class})`

### 4.配置文件加载问题

默认加载application.yml（必须有）

如果加载其他的需要写

```yml
spring:
	application:
		name:
	profiles:
		active: dev
```





