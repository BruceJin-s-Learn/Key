# Java线性池

## 1.优点

+ 缓解创建线程和销毁线程资源消耗
+ 提高响应速度
+ 重复利用



## 2.四种：

### 2.1 newSingleThreadExcutor

+ 单例

+ 每次执行一个线程

### 2.2 newFixedThreadPool

+ 创建固定大小的线性池

### 2.3 newScheduledThreadPool

+ 创建定长线程池
+ 定时和周期性任务执行

### 2.4 newCachedThreadPool

+ 创建一个可缓存的线性池