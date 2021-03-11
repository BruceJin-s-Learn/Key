# 大数据学习配置之Windows端

## 1.hadoop环境

### Java访问

- window系统的环境变量配置

  - 解压hadoop-3.1.2.tar.gz，将解压后的文件夹存放到自己软件目录

    - 例如：D:\software\hadoop-3.1.2

  - 解压winutils-master.zip，找到3.1.2版本

    - 将所有的文件覆盖到D:\software\hadoop-3.1.2\bin目录

  - 将winutils.exe和hadoop.dll文件拷贝到 C:\Windows\System32目录下

- 环境变量

  - 将Hadoop添加到环境变量
    - HADOOP_HOME-->D:\software\hadoop-3.1.2
    - HADOOP_USER_NAME-->root
    - Path --> %HADOOP_HOME%\bin;%HADOOP_HOME%\sbin;
  - JDK的版本也设置的和服务器版本一致

  //TODO

  - 修改当前Window的hosts文件

    - C:\Windows\System32\drivers\etc\hosts
    - 192.168.58.101 node01
      192.168.58.102 node02
      192.168.58.103 node03

  - 拷贝Hadoop的配置文件

    - core-site.xml
    - hdfs-site.xml
    - mapred-site.xml
    -  yarn-site.xml

  - 打开Idead,创建一个普通的Maven项目

    - 添加pom.xml

    - ```xml
      <properties>
      	<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
      	<maven.compiler.source>1.8</maven.compiler.source>
      	<maven.compiler.target>1.8</maven.compiler.target>
      	<!-- Hadoop版本控制 -->
      	<hadoop.version>3.1.2</hadoop.version>
      	<!-- commons-io版本控制 -->
      	<commons-io.version>2.4</commons-io.version>
      </properties>
      
      <dependencies>
      	<!-- https://mvnrepository.com/artifact/org.apache.hadoop/hadoop-common -->
      	<dependency>
      		<groupId>org.apache.hadoop</groupId>
      		<artifactId>hadoop-common</artifactId>
      		<version>${hadoop.version}</version>
      	</dependency>
      	<!-- https://mvnrepository.com/artifact/org.apache.hadoop/hadoop-hdfs -->
      	<dependency>
      		<groupId>org.apache.hadoop</groupId>
      		<artifactId>hadoop-hdfs</artifactId>
      		<version>${hadoop.version}</version>
      	</dependency>
      	<!-- https://mvnrepository.com/artifact/org.apache.hadoop/hadoop-client -->
      	<dependency>
      		<groupId>org.apache.hadoop</groupId>
      		<artifactId>hadoop-client</artifactId>
      		<version>${hadoop.version}</version>
      	</dependency>
      	<!-- https://mvnrepository.com/artifact/org.apache.hadoop/hadoop-mapreduce-client-common -->
      	<dependency>
      		<groupId>org.apache.hadoop</groupId>
      		<artifactId>hadoop-mapreduce-client-common</artifactId>
      		<version>${hadoop.version}</version>
      	</dependency>
      	<!-- https://mvnrepository.com/artifact/org.apache.hadoop/hadoop-mapreduce-client-core -->
      	<dependency>
      		<groupId>org.apache.hadoop</groupId>
      		<artifactId>hadoop-mapreduce-client-core</artifactId>
      		<version>${hadoop.version}</version>
      	</dependency>
      	<!-- https://mvnrepository.com/artifact/org.apache.hadoop/hadoop-mapreduce-client-jobclient-->
      	<dependency>
      		<groupId>org.apache.hadoop</groupId>
      		<artifactId>hadoop-mapreduce-client-jobclient</artifactId>
      		<version>${hadoop.version}</version>
      	</dependency>
      	<!-- https://mvnrepository.com/artifact/commons-io/commons-io -->
      	<dependency>
      		<groupId>commons-io</groupId>
      		<artifactId>commons-io</artifactId>
      		<version>${commons-io.version}</version>
      	</dependency>
      	<dependency>
      		<groupId>com.janeluo</groupId>
      		<artifactId>ikanalyzer</artifactId>
      		<version>2012_u6</version>
      	</dependency>
      </dependencies>
      ```

    - ```java
      package com.lzj;
      
      import org.apache.hadoop.conf.Configuration;
      import org.apache.hadoop.fs.BlockLocation;
      import org.apache.hadoop.fs.FileSystem;
      import org.apache.hadoop.fs.Path;
      
      import java.io.IOException;
      import java.util.Arrays;
      
      public class Hello01HDfs {
      
          /**
           * 文件信息
           *
           * @throws IOException
           */
          private static void pathInfo() throws IOException {
              //加载配置文件
              Configuration configuration = new Configuration(true);
              //获取文件系统
              FileSystem fileSystem = FileSystem.get(configuration);
              //创建路径的Path对象
              Path path = new Path("/lzj/hadoop-3.1.2.tar.gz");
              boolean flag = fileSystem.exists(path);
              System.out.println(fileSystem.getDefaultBlockSize(path) / 1024 / 1024);
              System.out.println(fileSystem.getDefaultReplication(path));
              BlockLocation[] bls = fileSystem.getFileBlockLocations(path, 0, 10);
              for (BlockLocation blockLocation : bls) {
                  System.out.println("HelloHdfs.hello(============================1)");
                  System.out.println(blockLocation.getLength());
                  System.out.println(blockLocation.getOffset());
                  System.out.println(Arrays.toString(blockLocation.getHosts()));
                  System.out.println(Arrays.toString(blockLocation.getNames()));
                  System.out.println(blockLocation.toString());
                  System.out.println("HelloHdfs.hello(============================2)");
              }
          }
      
          /**
           * 文件上傳和下載
           *
           * @throws IOException
           */
          private static void upload_download() throws IOException {
              //加载配置文件
              Configuration configuration = new Configuration(true);
            //获取文件系统
              FileSystem fileSystem = FileSystem.get(configuration);
              //文件上傳
              //        Path srcPath = new Path("D:\\apache-tomcat-8.5.47-windows-x64.zip");
              //        Path destPath = new Path("/lzj/");
              //        fileSystem.copyFromLocalFile(srcPath, destPath);
              //文件下載
              Path localPath = new Path("D:\\");
              Path hdfsPath = new Path("/lzj/apache-tomcat-8.5.47-windows-x64.zip");
              fileSystem.copyToLocalFile(hdfsPath, localPath);
          }
      
      }
      
      ```

      

### Idea访问

- 将HadoopIntellijPlugin-1.0.zip文件放到Idea的插件目录
  - D:\Program Files\JetBrains\IntelliJ IDEA 2019.2.4\plugins
- 打开Idea添加插件，然后重启Idea
  - ![image-20200625213633537](K:%5C100%20-%20%E5%AD%A6%E4%B9%A0%5C105_sxtbd%5Cone%5C%E5%A4%A7%E6%95%B0%E6%8D%AE%E6%96%87%E6%A1%A3%5C0201Hadoop-HDFS%5C006_document%5CHadoop-HDFS03.assets%5Cimage-20200625213633537.png)
  - ![image-20200625213746761](K:%5C100%20-%20%E5%AD%A6%E4%B9%A0%5C105_sxtbd%5Cone%5C%E5%A4%A7%E6%95%B0%E6%8D%AE%E6%96%87%E6%A1%A3%5C0201Hadoop-HDFS%5C006_document%5CHadoop-HDFS03.assets%5Cimage-20200625213746761.png)
- 配置HDFS
  - ![image-20200626163221713](K:%5C100%20-%20%E5%AD%A6%E4%B9%A0%5C105_sxtbd%5Cone%5C%E5%A4%A7%E6%95%B0%E6%8D%AE%E6%96%87%E6%A1%A3%5C0201Hadoop-HDFS%5C006_document%5CHadoop-HDFS03.assets%5Cimage-20200626163221713.png)