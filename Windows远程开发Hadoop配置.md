### 远程开发Hadoop
1. 创建Maven工程，编写pom.xml文件
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>HadoopLearning</groupId>
    <artifactId>FirstMR</artifactId>
    <version>1.0-SNAPSHOT</version>

    <property>
        <hadoopVersion>3.1.1</hadoopVersion>
    </property>
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-common</artifactId>
            <version>3.1.1</version>
        </dependency>

        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-hdfs</artifactId>
            <version>3.1.1</version>
        </dependency>

        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-mapreduce-client-core</artifactId>
            <version>3.1.1</version>
        </dependency>

        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-mapreduce-client-jobclient</artifactId>
            <version>3.1.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>3.1.1</version>
        </dependency>
    </dependencies>
</project>
```
2. 在resources文件夹中添加core-site.xml，hdfs-site.xml，log4j.properties文件，文件内容复制远程服务器同名文件内容
3. 下载远程服务器上的同版本Hadoop，在项目结构中设置Library，加入下载的hadoop/share文件夹中的jar文件
4. 下载对应版本的winutil.exe和hadoop.dll文件，拷贝到hadoop/bin和Windows/System32文件夹
5. 如果报错NativeIO.java中access，在main方法中加入代码段，手动加载hadoop.dll
```
static {
    try {
        System.load("E:/software/hadoop-3.1.1/bin/hadoop.dll");
    } catch (UnsatisfiedLinkError e) {
        System.err.println("Native code library failed to load.\n" + e);
        System.exit(1);
    }
    }
```