---
layout:     post
title:      "HDFS相关笔记"
date:       2018-05-30 09:46:00
categories: Computer System
tags:   [๑Hadoop, ๑BigData, ๑HDFS, ๑Spark]
description: "学习记录"
---

> 不适合人类阅读的学习笔记

## 前言

- 马上就六一了，赶在月底结束之前再记录一些东西吧～

- 以下HDFS的操作是基于Ubuntu18的

## HDFS简介
---

- [Hadoop分布式文件系统(HDFS)官方中文文档](https://hadoop.apache.org/docs/r1.0.4/cn/hdfs_design.html)

### Namenode 和 Datanode

- HDFS采用master/slave架构。一个HDFS集群是由一个Namenode和一定数目的Datanodes组成。

- HDFS采用Java语言开发，因此任何支持Java的机器都可以部署Namenode或Datanode。

- Namenode是一个中心服务器，负责管理文件系统的名字空间(namespace)以及客户端对文件的访问。集群中的Datanode一般是一个节点一个，负责管理它所在节点上的存储。HDFS暴露了文件系统的名字空间，用户能够以文件的形式在上面存储数据。

- 从内部看，一个文件其实被分成一个或多个数据块，这些块存储在一组Datanode上。Namenode执行文件系统的名字空间操作，比如打开、关闭、重命名文件或目录。它也负责确定数据块到具体Datanode节点的映射。Datanode负责处理文件系统客户端的读写请求。在Namenode的统一调度下进行数据块的创建、删除和复制。

- Namenode负责维护文件系统的名字空间，任何对文件系统名字空间或属性的修改都将被Namenode记录下来。应用程序可以设置HDFS保存的文件的副本数目。文件副本的数目称为文件的副本系数，这个信息也是由Namenode保存的。

- Namenode全权管理数据块的复制，它周期性地从集群中的每个Datanode接收心跳信号和块状态报告(Blockreport)。接收到心跳信号意味着该Datanode节点工作正常。块状态报告包含了一个该Datanode上所有数据块的列表。

- HDFS中的文件都是一次性写入的，并且 **严格要求在任何时候只能有一个写入者**。

## HDFS文件系统
---

### DFSShell

- HDFS以文件和目录的形式组织用户数据。它提供了一个命令行的接口(DFSShell)让用户与HDFS中的数据进行交互。命令的语法和用户熟悉的其他shell(例如 bash, csh)工具类似。下面是一些动作/命令的示例：

- 创建一个名为 `/foodir` 的目录:	`bin/hadoop dfs -mkdir /foodir`

- 创建一个名为 `/foodir` 的目录:	`bin/hadoop dfs -mkdir /foodir`

- 查看名为 `/foodir/myfile.txt` 的文件内容:	`bin/hadoop dfs -cat /foodir/myfile.txt`

#### 常用

- **注意，分布式文件系统中没有切换到某个目录下的概念，因为其文件全是分散在各个节点上的**

- 分布式文件系统的文件路径完整格式为 `hdfs://namenode|master:编号/root/...`

- 例如：`hdfs://master:8020/dataset/evaluation/bots_10m_10.csv`

- `hdfs dfs -ls  /...`显示分布式文件系统中某个目录（实际并不存在，只是逻辑上的）下的文件

- `hdfs dfs -rm -r file_name|directory_name` 删除某个文件或者目录

### 通讯协议

- 所有的HDFS通讯协议都是建立在TCP/IP协议之上。客户端通过一个可配置的TCP端口连接到Namenode，通过ClientProtocol协议与Namenode交互。而Datanode使用DatanodeProtocol协议与Namenode交互。

- 一个远程过程调用(RPC)模型被抽象出来封装ClientProtocol和Datanodeprotocol协议。在设计上，Namenode不会主动发起RPC，而是响应来自客户端或 Datanode 的RPC请求。

### 数据块

- HDFS被设计成支持大文件，适用HDFS的是那些需要处理大规模的数据集的应用。这些应用都是只写入数据一次，但却读取一次或多次，并且读取速度应能满足流式读取的需要。HDFS支持文件的“一次写入多次读取”语义。一个典型的数据块大小是64MB。因而，HDFS中的文件总是按照64M被切分成不同的块，每个块尽可能地存储于不同的Datanode中。




<br>
> 最后更新于2018.5.31
