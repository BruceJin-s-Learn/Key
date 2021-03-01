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
   1. Scala是强类型语言
3. 并发和分布式（Actor）
4. 特质、特征（类似java中interface和abstract的结合）
5. 模式匹配（类似java switch）
6. 高阶函数