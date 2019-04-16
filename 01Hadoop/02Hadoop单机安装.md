## Hadoop单机安装

> CentOS7

## 安装过程

1. 关闭防火墙

    ```shell
    systemctl stop firewalld.service
    
    systemctl disable firewalld.service
    ```

2. 安装JDK1.8

    - 下载JDK源码包

        ```shell
        cd
        wget https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.tar.gz
        ```

    - 在/usr/lib下创建JDK的安装文件夹java

        ```shell
        mkdir /usr/lib/java
        ```

    - 将下载的源码包解压到刚创建的文件夹

        ```shell
        tar -zxvf jdk-8u201-linux-x64.tar.gz -C /usr/lib/java/
        ```

    - 写入环境变量

        ```shell
        echo "JAVA_HOME=/usr/lib/java/jdk1.8.0_201
        JRE_HOME=/usr/lib/java/jdk1.8.0_201/jre
        PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
        export JAVA_HOME JRE_HOME PATH CLASSPATH" >> /etc/profile
        ```

    - 使环境变量生效

        ```shell
        source /etc/profile
        ```

    - 测试JDK 是否安装成功

        ```shell
        java -version
        ```

3. 安装Hadoop

    - 下载Hadoop

        ```shell
        cd
        wget https://www-eu.apache.org/dist/hadoop/common/hadoop-2.7.7/hadoop-2.7.7.tar.gz
        ```

    - 将Hadoop解压至/usr/local目录下

        ```shell
        tar -zxvf hadoop-2.7.7.tar.gz -C /usr/local/
        ```

    - 为Hadoop配置环境变量

        ```shell
        echo "HADOOP_HOME=/usr/local/hadoop-2.7.7/
        PATH=$PATH:$HADOOP_HOME/bin:$HADOOP/sbin:$HADOOP/share
        export HADOOP_HOME PATH" >> /etc/profile
        ```

    - 使环境变量生效

        ```shell
        source /etc/profile
        ```

    - 测试Hadoop是否安装成功

        ```shell
        hadoop version
        ```

    

## Hadoop目录结构

```
hadoop-2.7.7/
├── bin
│   Hadoop最基本的管理脚本和使用脚本的目录
├── etc
│   hadoop的配置文件目录，存放hadoop的配置文件
├── include
│   对外提供的编程库头文件（具体动态库和静态库在lib目录中）
├── lib
│   该目录包含了Hadoop对外提供的编程动态库和静态库，与include目录中的头文件结合使用。
├── libexec
│   各个服务对用的shell配置文件所在的目录，可用于配置日志输出、启动参数（比如JVM参数）等基本信息。
├── LICENSE.txt
├── NOTICE.txt
├── README.txt
├── sbin
│   Hadoop管理脚本所在的目录，主要包含HDFS和YARN中各类服务的启动/关闭脚本。
└── share
	存放hadoop的依赖jar包和文档，文档可以被删除掉
```

Hadoop 测试DEMO

```shell
cd 
mkdir input
cp /usr/local/hadoop-2.7.7/etc/hadoop/*.xml
hadoop jar /usr/local/hadoop-2.7.7/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.7.jar wordcount input ouput
```

