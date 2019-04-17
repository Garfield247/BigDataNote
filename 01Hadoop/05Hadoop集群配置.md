# Hadoop集群配置

> 有一台已装Hadoop和JDK的云主机
>
> 使用该云主机Clone两台

1. 修改主机名

    ```shell
    vim /etc/hostname
    ```

2. 配置主机映射

    ```shell
    vim /etc/hosts
    ```

    添加

    ```
    192.168.3.116 hadoop01 www.hadoop01.com
    192.168.3.200 hadoop02 www.hadoop02.com
    192.168.3.195 hadoop01 www.hadoop03.com
    ```

3. 环境搭建

    