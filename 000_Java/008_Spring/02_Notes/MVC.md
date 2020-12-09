![image-20201209141921238](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201209141921238.png)

## 1. MVC

### 1.1 MVC思想

model-view-controller分层思想，代码中运用dao、service、controller三层进行实现。

### 1.2 SpringMVC

#### 1.2.1 理解



#### 1.2.2 重定向与请求转发

重定向：redirect

请求转发：forward

#### 1.2.3 常用注解及作用

+ @comxxx
  + @controller
  +  @service
  + @rexxx
+ @Autoxxx 自动注入依赖
+ @Resouce 自动注入依赖
+ @Bean bean对象
+ @Value Key-value值

#### 1.2.4 如何接收客户端传递的不同类型的参数

@RequestBody

接收JSON对象

#### 1.2.5 @RequestMapping

作用：地址 

使用：