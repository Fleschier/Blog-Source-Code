---
layout:     post
title:      "hadoop集群使用中的一些问题记录"
date:       2018-07-20 10:40:00
categories: Hadoop CLuster
tags:   [๑Hadoop, ๑Linux, ๑CLuster]
description: "集群使用技巧"
---

> 不适合人类阅读的学习笔记

#### 无法运行spark-shell

- 一般出现这种情况是集群的内存满了

- 使用`df -h`命令来查看存储情况

- 空间几乎占满的状况：
![](/images/Hadoop/cluster_storage.png)

#### Linux下/proc目录简介

- [linux下proc目录的作用](https://blog.csdn.net/zdwzzu2006/article/details/7747977)

##### 删除文件夹

- 尽量使用`rmdir`来删除一个空目录，如果目录下存在多个文件，要一次性删除所有的使用`rm -rf`来实现。`-r`表示递归删除，`-f`表示强制执行。不过在删除之前一定要仔细确认，一旦删除无法撤销
