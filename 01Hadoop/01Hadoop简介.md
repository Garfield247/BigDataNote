# *Hadoop*

![https://hadoop.apache.org/hadoop-logo.jpg](https://hadoop.apache.org/hadoop-logo.jpg)

[Hadoop](https://hadoop.apache.org)是一个由Apache基金会所开发的开源的分布式系统基础架构。

## 产生背景

Hadoop的思想之源Google

Google的三驾马车`GFS`、`MapReduce`、`BigTable`

## 发展历程

- 2003-2004年

  Google公布了部分GFS和MapReduce思想的细节，受此启发的Doug Cutting等人用2年的业余时间实现了DFS和MapReduce机制，使Nutch性能飙升。然后Yahoo招安Doug Gutting及其项目。 

- 2005年

  Hadoop作为Lucene的子项目Nutch的一部分正式引入Apache基金会。 

- 2006年2月

  被分离出来，成为一套完整独立的软件，起名为Hadoop 
  Hadoop名字不是一个缩写，而是一个生造出来的词。是Hadoop之父Doug Cutting儿子毛绒玩具象命名的。 

Hadoop的成长过程 

​	`Lucene`–>`Nutch`—>`Hadoop`

总结起来

Hadoop起源于Google的三大论文 

GFS：Google的分布式文件系统Google File System 

MapReduce：Google的MapReduce开源分布式并行计算框架 

BigTable：一个大型的分布式数据库

演变关系 

GFS—->HDFS 
Google MapReduce—->Hadoop MapReduce 
BigTable—->HBase

## 优点

1. 扩容能力（Scalable）：Hadoop是在可用的计算机集群间分配数据并完成计算任务的，这些集群可用方便的扩展到数以千计个节点中。
2. 成本低（Economical）：Hadoop通过普通廉价的机器组成服务器集群来分发以及处理数据，以至于成本很低。
3. 高效率（Efficient）：通过并发数据，Hadoop可以在节点之间动态并行的移动数据，使得速度非常快。
4. 可靠性（Rellable）：能自动维护数据的多份复制，并且在任务失败后能自动地重新部署（redeploy）计算任务。所以Hadoop的按位存储和处理数据的能力值得人们信赖。

## 模块

该Hadoop包括以下模块：

- **Hadoop Common**：支持其他Hadoop模块的常用实用程序。
- **Hadoop分布式文件系统（HDFS™）**：一种分布式文件系统，可提供对应用程序数据的高吞吐量访问。
- **Hadoop YARN**：作业调度和集群资源管理的框架。
- **Hadoop MapReduce**：基于YARN的系统，用于并行处理大型数据集。
- **Hadoop Ozone**： **Hadoop**的对象存储。
- **Hadoop Submarine**： **Hadoop**的机器学习引擎。

## 相关项目

Apache的其他Hadoop相关项目包括：

- [**Ambari™**](https://ambari.apache.org/)：基于Web的工具，用于配置，管理和监控Apache Hadoop集群，包括对Hadoop HDFS，Hadoop MapReduce，Hive，HCatalog，HBase，ZooKeeper，Oozie，Pig和Sqoop的支持。Ambari还提供了一个用于查看群集运行状况的仪表板，例如热图和能够直观地查看MapReduce，Pig和Hive应用程序以及以用户友好的方式诊断其性能特征的功能。
- [**Avro™**](https://avro.apache.org/)：数据序列化系统。
- [**Cassandra™**](https://cassandra.apache.org/)：可扩展的多主数据库，没有单点故障。
- [**Chukwa™**](https://chukwa.apache.org/)：用于管理大型分布式系统的数据收集系统。
- [**HBase™**](https://hbase.apache.org/)：可扩展的分布式数据库，支持大型表的结构化数据存储。
- [**Hive™**](https://hive.apache.org/)：一种数据仓库基础架构，提供数据汇总和即席查询。
- [**Mahout™**](https://mahout.apache.org/)：可扩展的机器学习和数据挖掘库。
- [**Pig™**](https://pig.apache.org/)：用于并行计算的高级数据流语言和执行框架。
- [**Spark™**](https://spark.apache.org/)：用于Hadoop数据的快速通用计算引擎。Spark提供了一种简单而富有表现力的编程模型，支持广泛的应用程序，包括ETL，机器学习，流处理和图形计算。
- [**Tez™**](https://tez.apache.org/)：基于Hadoop YARN的通用数据流编程框架，它提供了一个功能强大且灵活的引擎来执行任意DAG任务，以处理批量和交互式用例的数据。Tez正在被Hadoop生态系统中的Hive™，Pig™和其他框架以及其他商业软件（例如ETL工具）采用，以取代Hadoop™MapReduce作为底层执行引擎。
- [**ZooKeeper™**](https://zookeeper.apache.org/)：用于分布式应用程序的高性能协调服务。