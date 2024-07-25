---
layout:     post
title:      "《Scala编程》阅读记录——集合类进阶"
date:       2018-07-24 11:25:00
categories: Computer Programs
tags:   ๑Scala
description: "学习记录"
---

> 不适合人类阅读的学习笔记

## 第十七章 使用集合类
---

### 序列

#### 列表

- List类是不可变 **链表**, 因此支持在头部快速添加和移除条目，但是不提供按下标快速访问的功能，因为实现这个功能需要线性地遍历列表。

#### 列表缓冲(ListBuffer)

- List类提供对列表头部的快速访问，但是对尾部就不那么高效，因此在尾部添加元素时我们经常需要用到reverse方法，在头部添加元素最后再reverse来获得我们想要的顺序

- ListBuffer是一个可变对象(包含在scala.collection.mutable中)，帮助我们在需要追加元素来构建列表时能够更加高效。ListBuffer提供了常量时间的往前和往后追加元素的操作。

- 可以使用`+=`来往后追加元素，使用`+=:`来往前追加元素

- 最后可以使用`toList`方法来转换成List类型

- 使用ListBuffer的另一个原因是可以防止可能的栈溢出

#### 数组缓冲(ArrayBuffer)

- 创建数组缓冲的时候不需要指定长度，只要给定类型
```
import scala.collection.mutable.ArrayBuffer
val buf = new ArrayBuffer[Int]()
```

- 使用`+=`方法来追加元素

- 所有的数组的常规操作都是可以用的

#### 字符串(通过StringOps)

- StringOps实现了很多序列的方法。由于Predef有一个从String到StringOps的隐式转换，可以将任何字符串当做序列来处理

- 例如:
```
def hasUpperCase(s: String) = s.exists(_.isUpper)
hasUpperCase("Robert Frost")
```
这里由于String类本身并没有任何名为`exists`的方法，但是StringOps有，通过隐式转换将s转换成StringOps来实现

### 集和映射
---

#### 使用集

- 集的关键特征是它们会确保在同一时刻，以`==`为标准，集里的每个对象都最多出现一次

- 集的方法见博客[方法查询](https://fleschier.github.io/2018/07/Scala-infos/)

#### 使用映射

- 映射使用键来索引对应的值

- 下面是一个统计每个单词在字符串中出现次数的方法：
```
def countWords(text: String) = {
  val counts = mutable.Map.empty[String,Int]
  for (rawWord <- text.split("[ ,!.]+")){
    val word = rawWord.toLowerCase // 统一变为小写字母
    val oldCount =
      if(counts.contains(word)) counts(word)
      else 0
    counts += (word -> (oldCount + 1))
  }
  counts
}
```

- 映射的方法见博客[方法查询](https://fleschier.github.io/2018/07/Scala-infos/)

- 可变集合和可变映射的工厂方法都采用了hash的技术。例如`scala.collection.mutable.Set()`这个工厂方法返回一个`scala.collection.mutable.HashSet`。同理， `scala.collection.mutable.Map()`这个工厂方法返回一个`scala.collection.mutable.HashMap`

### 元组
---

- 元组帮助我们省去定义那些简单的主要承载数据的类的麻烦。**元组的一个常见的应用场景是从方法返回多个值**


<br>
> 最后更新于2018.7.24
