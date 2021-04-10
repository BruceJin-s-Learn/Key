# Flink相关问题

## 关于监听

Windows: nc -L -p 9999

Linux： nc -lk 9999

## A1 NoClassDefFoundError环境报错

报错：

![image-20210331155924922](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331155924922.png)

![image-20210401150753836](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401150753836.png)

原因：

![image-20210331160018074](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331160018074.png)

解决：

![image-20210331160122378](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331160122378.png)

scope：打包的时候不包含这个依赖，增强移植性。

## A2 webUI端呈现过程

![image-20210331171755416](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331171755416.png)



## A3 用lambda表达式

报错：

![image-20210331173013164](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331173013164.png)

![image-20210331200926451](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331200926451.png)

原因：

lambda表达式编写方式不识别返回类型，需要手动跟上returns指定类型。

解决：

![image-20210331173459748](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331173459748.png)



## A4 (...)

报错：

![image-20210331204507635](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331204507635.png)

原因：

没有导入响应包

解决：

![image-20210331180057527](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331180057527.png)



## A5 java: 程序包org.apache.flink.api.java不存在

报错：

java: 程序包org.apache.flink.api.java不存在

解决：

第一个：

![image-20210331183541714](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331183541714.png)

第二个：

重启项目，然后刷新maven

第三种：

在终端加入命令：

`mvn idea:idea`



## A6 报execute错

报错：

![image-20210331183738936](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331183738936.png)

原因：

代码中使用了socket作为DataSource,如果socket监听的端口没有nc -lk 9999,就会报错

9999端口是代码中指定的

![image-20210331183921800](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331183921800.png)

解决：

![image-20210331183855950](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331183855950.png)



## A7 内存

![image-20210331192640595](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331192640595.png)

## A8 socketTextStream出错

报错：

![image-20210331194305034](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331194305034.png)

![image-20210331194316189](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331194316189.png)

原因：

导入的`StreamExecutionEnvironment`的包是Scala的：

`import org.apache.flink.streaming.api.scala.StreamExecutionEnvironment;`

解决：

导入下面的包

![image-20210331194424429](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331194424429.png)

注意：

用Scala编写的话，导包导Scala的环境

![image-20210331204446938](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210331204446938.png)

## A9 scalac ：token not found

报错：

![image-20210401090053832](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401090053832.png)

原因：



解决：



## A10 上次任务未关

报错：

这个报错不影响执行

![image-20210401093303076](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401093303076-1617437063675.png)

原因：

上一次任务的网页没有关，请求一个不存在的网页

![image-20210401094341558](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401094341558.png)

解决：

关闭上次任务的网页

![image-20210401093411191](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401093411191.png)



## A11 key要hash分区

![image-20210401094402729](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401094402729.png)



## A12 获取执行计划web（并行度）

网址：

https://flink.apache.org/visualizer/

![image-20210401104904600](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401104904600.png)

![image-20210401104920934](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401104920934.png)

![image-20210401104854136](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401104854136.png)

计划:vs:实际执行​

![image-20210401105431821](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401105431821.png)



报错：

![image-20210401150451196](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401150451196.png)

问题：

要放在操作符之后

解决：

![image-20210401150524075](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401150524075.png)

## A13 关于key

先找到key，才能groupByKey，对key进行操作



## A14 tuple区别

Java25

+ ```java
  /**
   * The base class of all tuples. Tuples have a fix length and contain a set of fields,
   * which may all be of different types. Because Tuples are strongly typed, each distinct
   * tuple length is represented by its own class. Tuples exists with up to 25 fields and
   * are described in the classes {@link Tuple1} to {@link Tuple25}.
   *
   * <p>The fields in the tuples may be accessed directly a public fields, or via position (zero indexed)
   * {@link #getField(int)}.
   *
   * <p>Tuples are in principle serializable. However, they may contain non-serializable fields,
   * in which case serialization will fail.
   */
  @Public
  public abstract class Tuple implements java.io.Serializable {
  
  	private static final long serialVersionUID = 1L;
  
  	public static final int MAX_ARITY = 25;
  
  
  	/**
  	 * Gets the field at the specified position.
  	 *
  	 * @param pos The position of the field, zero indexed.
  	 * @return The field at the specified position.
  	 * @throws IndexOutOfBoundsException Thrown, if the position is negative, or equal to, or larger than the number of fields.
  	 */
  	public abstract <T> T getField(int pos);
  
  	/**
  	 * Gets the field at the specified position, throws NullFieldException if the field is null. Used for comparing key fields.
  	 *
  	 * @param pos The position of the field, zero indexed.
  	 * @return The field at the specified position.
  	 * @throws IndexOutOfBoundsException Thrown, if the position is negative, or equal to, or larger than the number of fields.
  	 * @throws NullFieldException Thrown, if the field at pos is null.
  	 */
  	public <T> T getFieldNotNull(int pos){
  		T field = getField(pos);
  		if (field != null) {
  			return field;
  		} else {
  			throw new NullFieldException(pos);
  		}
  	}
  
  	/**
  	 * Sets the field at the specified position.
  	 *
  	 * @param value The value to be assigned to the field at the specified position.
  	 * @param pos The position of the field, zero indexed.
  	 * @throws IndexOutOfBoundsException Thrown, if the position is negative, or equal to, or larger than the number of fields.
  	 */
  	public abstract <T> void setField(T value, int pos);
  
  	/**
  	 * Gets the number of field in the tuple (the tuple arity).
  	 *
  	 * @return The number of fields in the tuple.
  	 */
  	public abstract int getArity();
  
  	/**
  	 * Shallow tuple copy.
  	 * @return A new Tuple with the same fields as this.
  	 */
  	public abstract <T extends Tuple> T copy();
  
  	// --------------------------------------------------------------------------------------------
  
  	/**
  	 * Gets the class corresponding to the tuple of the given arity (dimensions). For
  	 * example, {@code getTupleClass(3)} will return the {@code Tuple3.class}.
  	 *
  	 * @param arity The arity of the tuple class to get.
  	 * @return The tuple class with the given arity.
  	 */
  	@SuppressWarnings("unchecked")
  	public static Class<? extends Tuple> getTupleClass(int arity) {
  		if (arity < 0 || arity > MAX_ARITY) {
  			throw new IllegalArgumentException("The tuple arity must be in [0, " + MAX_ARITY + "].");
  		}
  		return (Class<? extends Tuple>) CLASSES[arity];
  	}
  
  	// --------------------------------------------------------------------------------------------
  	// The following lines are generated.
  	// --------------------------------------------------------------------------------------------
  
  	// BEGIN_OF_TUPLE_DEPENDENT_CODE
  	// GENERATED FROM org.apache.flink.api.java.tuple.TupleGenerator.
  	public static Tuple newInstance(int arity) {
  		switch (arity) {
  			case 0: return Tuple0.INSTANCE;
  			case 1: return new Tuple1();
  			case 2: return new Tuple2();
  			case 3: return new Tuple3();
  			case 4: return new Tuple4();
  			case 5: return new Tuple5();
  			case 6: return new Tuple6();
  			case 7: return new Tuple7();
  			case 8: return new Tuple8();
  			case 9: return new Tuple9();
  			case 10: return new Tuple10();
  			case 11: return new Tuple11();
  			case 12: return new Tuple12();
  			case 13: return new Tuple13();
  			case 14: return new Tuple14();
  			case 15: return new Tuple15();
  			case 16: return new Tuple16();
  			case 17: return new Tuple17();
  			case 18: return new Tuple18();
  			case 19: return new Tuple19();
  			case 20: return new Tuple20();
  			case 21: return new Tuple21();
  			case 22: return new Tuple22();
  			case 23: return new Tuple23();
  			case 24: return new Tuple24();
  			case 25: return new Tuple25();
  			default: throw new IllegalArgumentException("The tuple arity must be in [0, " + MAX_ARITY + "].");
  		}
  	}
  
  	private static final Class<?>[] CLASSES = new Class<?>[] {
  		Tuple0.class, Tuple1.class, Tuple2.class, Tuple3.class, Tuple4.class, Tuple5.class, Tuple6.class, Tuple7.class, Tuple8.class, Tuple9.class, Tuple10.class, Tuple11.class, Tuple12.class, Tuple13.class, Tuple14.class, Tuple15.class, Tuple16.class, Tuple17.class, Tuple18.class, Tuple19.class, Tuple20.class, Tuple21.class, Tuple22.class, Tuple23.class, Tuple24.class, Tuple25.class
  	};
  	// END_OF_TUPLE_DEPENDENT_CODE
  }
  ```

Scala22

+ ```scala
  
  ```

## A15 Csv需要

报错：

![image-20210401171450550](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401171450550.png)

原因：

![image-20210401171556274](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210401171556274.png)

解决：

csv需要以逗号作为分隔符，而tuple（元组）的toString方法正好是以逗号分割。



如果并行度为1则写出去文件。

否则是文件夹包含从1开始的文件。

如果并行度大于文件数则生成等并行度文件数，含有空文件。

## A16 关于能拿到环境的函数

能拿到环境就能玩很多花样

## A17 keyBy的key

这个key是虚拟key，没有实体，所以不会返回。

其是从进来的流数据中选取的字段。

关键看这个虚拟key是什么类型。

```java
KeyedStream<Tuple3<String, String, Integer>, Tuple> keyedStream = map.keyBy(0);
keyedStream.print();
KeyedStream<Tuple3<String, String, Integer>, String> KeyedStream5 = map.keyBy(tuple -> tuple.f1);
```

## A18 执行时优化

![image-20210402094022413](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210402094022413.png)



## A19 flinkweb上传任务出错

报错：

![image-20210402110846115](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210402110846115.png)

原因：

![image-20210402110712247](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210402110712247.png)

这是测试的本地createLocalEnvironment...

解决：

![image-20210402110626716](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210402110626716.png)

## A20 web中查看socket在哪



## A21 maven打包

项目路径不要有中文

没有maven用build

有maven用clean+install



## A22 yarn模式特点

+ 资源用多少拿多少



## A23 flink窗口time的类型





## A24 keyBy 和 window

![image-20210402162600071](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210402162600071.png)



## A25 并行度变化

找keyBy和window就可以

这两个的前后

并行度设置有4个级别：

+ 算子级别（代码）
+ 执行环境级别（代码）
+ 客户端级别（-p命令行模式最好）
+ 系统级别（文件）

因为代码方式运行时，已经打了jar包（编译、执行、发布），导致不能再更改。

## A26 改并行度

keyby没有对数据进行操作，因为是虚拟key，相当于一个准备工作，没有对流处理，只告诉用哪个key来整合。

在操作后可以进行改并行度，setParallelism()

## A27 event time 时间类型

Procession time 处理时间：

+ 优点：最小延迟+最佳性能
+ 缺点：可能会有数据乱序问题 

Event Time 事件时间：

+ 解决顺序问题
+ 因为数据来了之后会有等待看是否有之前的事件来，所以会有延迟
+ event+timestamp

Ingestion time 摄入时间

## A28 timeWindow

timeWindow

[start.end)



## A29 数据容忍度



![image-20210406105626623](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210406105626623.png)

与语义的关系：

+ 容忍度与语义程反比



## A30 写时间类型未指定水印

**报错：**

![image-20210406111147546](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/image-20210406111147546.png)

**原因：**

改了时间类型，需要指定水印，报的错

**解决：**

waterMark（水印），本质时间戳

getAutoWatermarkInterval()

水印默认200ms

处理时间戳：assignTimestampAndWatermatks、

默认并行

## A31 水印

### 是什么



### 干什么（作用）



### 实现

抽时间加水印

+ 抽时间戳
+ get

非周期性

+ check
+ get

抽时间+check

两个类执行时间



----

迟到的数据侧输出



## A32 idea无法加载到主类

在网上找了很多资料，都是说配置一下主类就可以，但是试过发现还是不能解决问题，找到下面的博客，解决了问题。

 

在IDEA的使用过程中，经常断掉服务或者重启服务，最近断掉服务重启时突然遇到了一个启动报错：

错误：找不到或无法加载主类

猜测：1，未能成功编译；

​      尝试：菜单---》Build---》Rebuild Prodject 

​      结果：启动服务仍然报同样的错误

​     2，缓存问题；

​      尝试：菜单---》File---》Invalidate Caches/Restart 选择Invalidate and Restart 或者 只是Invalidate，清除掉缓存，然后Rebuild Project

​      结果：启动成功，问题解决

 

设置一下file-->project structure-->Module：
paths里面的编译路径Complier output：

![img](Flink%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98.assets/1284193-20180428141926102-1068677227.png)

## A33 checkpoint

checkpoint会影响数据处理时间（先保存再计算）。

checkpoint优先级是最高的，可能导致用户计算的延迟，避免结果产生问题。



并行度都设置为1的话，有两个流

一个数据处理的流（并行度1），时间

一个checkpoint（设置1个checkpoint），时间

## A34 flink容错机制

state：mem/fs/rocksdb（kv，增量）

env

## A35 操作链

优点：

+ 默认开启，避免了序列化和反序列化。计算快
+ 减少缓冲区数据的交换
+ 可以减少延迟和提高吞吐量
+ 减少线程切换

缺点：

+ 任务都跑在一个slot中，如果业务非常复杂，会让整体计算情况更加缓慢。
  + 可以手动对操作符进行startNewChain和disableChaing+

目的：

+ 让taskSlot发挥最大的（共享发挥到极致，避免沟通的通信成本）

可以细粒度的控制工作链，但是不要在头部开（head只能与下游连接，不能与上游连接）

## A36 任务槽

任务槽的多少决定了并行度的上限。

组内看最大，组外看之和。



solt组，开启的group，组内的operator和之前的操作符不在一个手机里，就不能共享slot，就会重占用其他的slot。

组内不能共享slot，组内互斥

组内可以共享slot，组内taskslots占用数量由最大并行度决定

最终slot数量为各组之和。

## A37 偏移量解决方案

一致性问题：幂等操作+事务

事务处理中心



## A40 CEP

四步：

+ 事件/数据流
+ 定义，匹配规则pattern
+ 检测
+ 处理



## A41 flink API

SQL

DataStream

ProcessFunction

## A42 特殊符号表字段

$符号

`a这种，表示这是个字段