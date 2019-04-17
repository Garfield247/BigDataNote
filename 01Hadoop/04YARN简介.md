# Yarn

​	<!--Apache Hadoop YARN （Yet Another Resource Negotiator，另一种资源协调者）是一种新的 Hadoop 资源管理器，它是一个通用资源管理系统，可为上层应用提供统一的资源管理和调度，它的引入为集群在利用率、资源统一管理和数据共享等方面带来了巨大好处。-->

## 云计算服务的三层

云计算可以认为包括以下几个层次的服务：基础设施即服务（**IaaS**），平台即服务（**PaaS**）和软件即服务（**SaaS**）。

+ **IaaS**：基础设施即服务

    IaaS(Infrastructure-as-a-Service)：基础设施即服务。消费者通过Internet可以从完善的计算机基础设施获得服务。例如：硬件服务器租用。

+ **PaaS**：平台即服务

    PaaS(Platform-as-a-Service)：平台即服务。PaaS实际上是指将软件研发的平台作为一种服务，以SaaS的模式提交给用户。因此，PaaS也是SaaS模式的一种应用。但是，PaaS的出现可以加快SaaS的发展，尤其是加快SaaS应用的开发速度。例如：软件的个性化定制开发。

+ **SaaS**：软件即服务

    SaaS(Software-as-a-Service)：软件即服务。它是一种通过Internet提供软件的模式，用户无需购买软件，而是向提供商租用基于Web的软件，来管理企业经营活动。例如：阳光云服务器。

> **从云计算概念上讲，YARN可看做PAAS层，他能够为不同类型的应用程序提供统一的管理和调度**



## YARN设计目标

- 通用的统一资源管理系统

    同时运行长应用程序和短应用程序

- 长应用程序

    通常情况下永不停止

    Service（hadoop、spark、storm)、Http Server等

- 短应用程序

    短时间（秒级、分级、时级）内会运行结束的程序

    MR job、Spark job等



## YARN服务组件

![MapReduce NextGen Architecture](http://hadoop.apache.org/docs/stable/hadoop-yarn/hadoop-yarn-site/yarn_architecture.gif)

 从 YARN 的架构图来看，它主要由ResourceManager、NodeManager、ApplicationMaster和Container等以下几个组件构成。

- ResourceManager（RM）

    > 由Scheduler调度器和ApplicationsManager（ASM：资源管理器）2个组件组成，ResourceManager和每个NodeManager (NM)构成一个资源估算框架，管理协调分配集群中的资源，对在系统中所有应用的资源分配拥有最终最高级别的仲裁权。

    ​    总的来说，RM有以下作用

    1. 处理客户端请求
    2. 启动或监控ApplicationMaster
    3. 监控NodeManager
    4. 资源的分配与调度

- ApplicationMaster（AM）

    > 用来协调应用程序下Task的运行。它和MapReduce Task都运行在 Container中，这个Container由RM(ResourcesManager)调度（启动/停止）并由NM(NodeManager)管理，并且监控所有Task的运行情况，在任务运行失败时，重新为任务申请资源以启动任务。
    > 注：（**MRAppMaster**是mapreduce的ApplicationMaster实现）

    ​    总的来说,AM有以下作用

    1. 负责数据的切分
    2. 为应用程序申请资源并分配给内部的任务
    3. 任务的监控与容错

- NodeManager（NM）

    >  来启动和监控本地计算机资源单位Container的利用情况，是每个节点上的资源和任务管理器，定时地向RM汇报本节点上的资源使用情况和各个Container的运行状态，并且接受并处理来自AM的Container启动/停止等请求。

    ​    总的来说，NM有以下作用

    1. 管理单个节点上的资源
    2. 处理来自ResourceManager的命令
    3. 处理来自ApplicationMaster的命令

- Container

    >  Container是yarn资源的抽象，它封装了某个节点上的多维度资源（内存，cpu，磁盘，网络等），当AM向RM申请资源时，RM为AM返回的资源便是用Container表示的。yarn会为每个任务分配一个Container，且该任务只能使用该Container描述的资源，它是一个动态资源划分单位，是根据应用程序的需求动态生成的。（目前yarn只支持cpu和内存2种资源）

    ​    总的来说，Container有以下作用

    1. 对任务运行环境进行抽象，封装CPU、内存等多维度的资源以及环境变量、启动命令等任务运行相关的信息

   要使用一个 YARN 集群，首先需要一个包含应用程序的客户的请求。ResourceManager 协商一个容器的必要资源，启动一个 ApplicationMaster 来表示已提交的应用程序。通过使用一个资源请求协议，ApplicationMaster 协商每个节点上供应用程序使用的资源容器。执行应用程序时，ApplicationMaster 监视容器直到完成。当应用程序完成时，ApplicationMaster 从 ResourceManager 注销其容器，执行周期就完成了。



## YARN工作流程

### Hadoop1的流程



```mermaid
graph TD

a(Client)
b(Client)

subgraph JobTracker
c[Job<br/>Tracker]
end
subgraph 
d[Task<br/>Tracker]
e((Task))
f((Task))
end
subgraph 
g[Task<br/>Tracker]
h((Task))
i((Task))
end
subgraph 
k[Task<br/>Tracker]
l((Task))
m((Task))
end

a -.Job Submission.-> c
b -.Job Submission.-> c
d --MapReduce Status--> c
g --MapReduce Status--> c
k --MapReduce Status--> c
e --MapReduce Status--> d
f --MapReduce Status--> d
h --MapReduce Status--> g
i --MapReduce Status--> g
l --MapReduce Status--> k
m --MapReduce Status--> k
```



Hadoop2流程

```mermaid
graph TB

a(Client)
b(Client)

subgraph 
c[Resource<br/>Manager]
end
subgraph 
d[Node<br/>Manager]
e((Container))
f((Application<br/>Master))
end
subgraph 
g[Node<br/>Manager]
h((Application<br/>Master))
i((Container))
end
subgraph 
k[Node<br/>Manager]
l((Container))
m((Container))
end

a -.Job Submission.-> c
b -.Job Submission.-> c
d ==Node Status==> c
g ==Node Status==> c
k ==Node Status==> c
e --MapReduce Status--> h
f --Resource Request--> c
h --Resource Request--> c
i --MapReduce Status--> f
l --MapReduce Status--> h
m --MapReduce Status--> h
```

 ![MapReduce NextGen Architecture](http://hadoop.apache.org/docs/stable/hadoop-yarn/hadoop-yarn-site/yarn_architecture.gif)

1. Client向RM中提交JOB。RM会生成新的Job ID（即Application ID)，接着Client计算输入分片，拷贝资源(包括Job JAR文件、配置文件，分片信息)到HDFS，提交JOB给RM。

2. RM接受提交的JOB，则将其请求交给Scheduler（调度器）处理，Scheduler（调度器）分配Container，同时RM在NM上分配应用程序第一个Container来启动ApplicationMaster进程，MRAppMatser会初始化一定数量的记录对象(bookkeeping)来跟踪JOB的运行进度， 并收取每个TASK的进度和完成情况，接着MRAppMaster收集计算后的输入分片情况，如果应用程序很小，能在同一个JVM上运行，则用uber模式.

3. 如果不在uber模式下运行，则Application Master会为所有的Map和Reducer task向RM请求Container，所有的请求都通过heartbeat(心跳)传递，心跳也传递其他信息，例如关于map数据本地化的信息，分片所在的主机和机架地址信息，这些信息帮助调度器来做出调度的决策，调度器尽可能遵循数据本地化或者机架本地化的原则分配Container。

    > 在Yarn中，例如，用yarn.scheduler.capacity.minimum- allocation-mb设置最小申请资源1G，用yarn.scheduler.capacity.maximum-allocation-mb设置 最大可申请资源10G 这样一个Task申请的资源内存可以灵活的在1G~10G范围内

4. 获取到Container后，NM上的Application Master就联系NM启动Container，Task最后被一个叫org.apache.hadoop.mapred.YarnChild的main类执行，不过在此之前各个资源文件已经从分布式缓存拷贝下来，这样才能开始运行map Task或者reduce Task。PS：YarnChild是一个(dedicated)的JVM。

5. 当Yarn运行同时，各个Container会报告它的进度和状态给Application Master，客户端会每秒轮询检测Application Master，这样就随时收到更新信息，这些信息可以通过Web UI来查看。

6. 客户端每5秒轮询检查Job是否完成，期间需要调用函数Job类下waitForCompletion()方法,Job结束后该方法返回。轮询时间间隔可以用配置文件的属性mapreduce.client.completion.pollinterval来设置

7. 应用程序运行完成后， MRAppMaster向ResourceManager 注销并关闭自己。

