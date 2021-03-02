# Scala了解

### A1 为什么学

1. 基于JVM与Java语言相似

2. spark 底层是Scala写的

### A2 版本

| spark | scala |
| ----- | ----- |
| 1.6   | 2.10  |
| 2.0   | 2.11  |

版本对应可以在maven依赖网站（https://mvnrepository.com/artifact/org.apache.spark/spark-core）查看

+ <img src="01_Scala%E4%BA%86%E8%A7%A3.assets/image-20210228150320581.png" alt="image-20210228150320581" style="zoom:33%;" />

### A3 特性

**总：**

+ 面向对象

+ 面向函数

**分：**

1. Scala和Java可以混编，无缝连接
   1. 两种语言编写的类直接相互调用等
2. 类型推测（自动推测类型）
   1. java8版本还是强类型
   2. Java10版本之后可以局部变量实用var
3. 并发和分布式（Actor）
4. 特质、特征（类似java中interface和abstract的结合）
   1. 接口：抽象方法+value（常量）
   2. 抽象类
   3. Java是单继承多实现
   4. Scala是多继承没有实现
5. 模式匹配（类似java switch）
   1. Scala可以匹配更多
6. 高阶函数
   1. 一切皆函数
   2. 把函数当作参数传到任何地方

### A4 应用

+ `kafka`：分布式消息队列，内部代码经常用来处理**并发**的问题，用scala可以大大简化其代码。
+ `spark`：方便处理**多线程**场景，另外`spark`主要用作内存计算，经常要用来实现复杂的算法。利用`scala`这种**函数式编程语言**可以大大简化代码。



