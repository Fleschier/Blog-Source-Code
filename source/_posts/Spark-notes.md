---
layout:     post
title:      "Spark实际操作过程中的一些调优笔记"
date:       2018-09-13 21:47:00
categories: Computer Programs
tags: [๑Spark, ๑BigData]
---

## Spark调优的一些参数设置
---

### SparkConf的一些参数设置

- 见博客[Spark性能优化：资源调优篇](https://www.iteblog.com/archives/1659.html)

### 较为全面的一个Spark性能参数讲解

- [Spark性能相关参数配置](https://spark-config.readthedocs.io/en/latest/index.html)

### spark分区器

- 主要有HashPartitioner和RangePartitioner两种。

- HashPatitioner按照给定key计算出的HashCode通过模运算来分区，缺点是可能造成分区出现数据倾斜。

- RangePartioner尽量保证每个分区中数据量的均匀，而且分区与分区之间是有序的(分区内部无序)。在分区计算时可能需要消耗部分资源，因此选择那种分区方法应看具体情况。

- [Spark分区器HashPartitioner和RangePartitioner代码详解](https://www.iteblog.com/archives/1522.html)
