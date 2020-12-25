# CRM | 思路

## 1. 分层思想

### 【controller】

#### 1.1.1 作用

##### 1. 连接前端（处理请求）

+ 地址栏，前端页面连接

  ```java
  @RequestMapping("/地址")
  ```

+ 实现前端页面的跳转

  ```java
  @RequestMapping("index")
  public String index(){
  	return "index";
  }
  ```

##### 2. 调用service层方法

+ 注入service，调用service层的方法

  ```java
  @RequestMapping("list")
  @ResponseBody
  public Map<String,Object> queryUserList(UserQuery userQuery){
      return userService.queryByParamsForTable(userQuery);
  }
  ```


##### 3. 作用域



### 【service】

实现业务功能

### 【dao】

连接数据库信息

+ 返回查询数据
+ 增删改会返回影响行数

## 2. 前后端交互

### 【前端】

#### 2.1.1 请求

##### 1. Ajax

```js
$.ajax({
    type:"get"/"post"/""
    
})
/**
* ajax中的data，来自前端获取的请求信息
* 其中key是后端bean对象的属性，value是前端来的数据的属性（对应.ftl前端页面标签中的name）
*/
```

![image-20201206170411552](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201206170411552.png)

##### 2. Post

```js
$.post({
    
})
```

#### 2.1.2 页面跳转

#### 2.1.3 页面监听

##### 1. 通过表单按钮（lay-filter）

```js
form.on("submit(saveBtn)",function(data){   
});
```

##### 2. 通过class

```js
 $(".class属性名").click(function (){
 })
```

头部工具栏

行工具栏

### 【后端】

.1 数据库分析,需要什么得到什么数据

.2 前端页面点击的页面跳转情况（如main.ftl）

.3 设置页面跳转(controller)

.4 代码实现 sql->mapper->service->controller

## 3.CRUD

### 3.1 查询



### 3.2 添加



### 3.3 修改

1. 必须有唯一签名（一般是id）进行定位（在sql语句的where中筛选）
2. 前端页面有隐藏域id（hidden，value是${}），后端在controller层从request作用域中获取，setAttribute()传入对象中
3. 在service层，对作用域传入的值进行业务逻辑处理，返回结果
4. 在controller层获取到结果返回页面或者JSON对象



### 3.4 删除



## 4. 重要

### 1. 角色管理



## 5. 小点

### 5.1 # or $

`#`:

+ 代表id
+ sql语句中

`$`:

+ 前端ajax,post

## 6. 扫描配置

mapper到后台dao层接口的连接：配置文件中有扫描进行实现

启动类有扫描，扫描dao层的接口

