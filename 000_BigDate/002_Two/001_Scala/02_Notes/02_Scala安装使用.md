# Scala安装使用

## A1 安装

1. 官网下载：https://www.scala-lang.org/download/all.html
2. 下载后，双击msi包安装，:exclamation:记住安装路径。
   + 路径要求：
     + 纯英文
     + 没有空格和特殊符号
3. 配置环境变量（和配置jdk一样）
   + 新建`SCALA_HOME`
     + 地址是安装路径
   + 编辑Path变量
     + `%SCALA_HOME%\bin`
4. 测试
   + 打开cmd并输入：`scala -version`

## A2 IDEA配置Scala插件

### 1.1 官网下载插件

https://plugins.jetbrains.com/

注意：插件版本与IDEA版本对应。

在IDEA文件夹`IntelliJ IDEA 2019.3.5\plugins\`下

### 1.2 新建项目相关设置

配置jdk

+ <img src="02_Scala%E5%AE%89%E8%A3%85%E4%BD%BF%E7%94%A8.assets/image-20210301151316649.png" alt="image-20210301151316649" style="zoom: 50%;" />
+ <img src="02_Scala%E5%AE%89%E8%A3%85%E4%BD%BF%E7%94%A8.assets/image-20210301151504145.png" alt="image-20210301151504145" style="zoom: 50%;" />

### 1.3 创建Scala项目

创建基础`scala`项目，配置`scala sdk(Software Development Kit)`

+ <img src="02_Scala%E5%AE%89%E8%A3%85%E4%BD%BF%E7%94%A8.assets/image-20210301162219675.png" alt="image-20210301162219675" style="zoom:33%;" />

