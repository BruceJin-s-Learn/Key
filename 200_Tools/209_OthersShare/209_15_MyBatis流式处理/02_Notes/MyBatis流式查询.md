# MyBatis流式查询

1.Cursor是可关闭的

2.Cursor是可遍历的



提供的三个方法：

+ `isOpen()`
+ `isConsumed()`
+ `getCurrentIndex()`



构建Cursor过程方案

+ `SqlSessionFactory`
+ `TransactionTemplate`
+ `@Transactional`注解