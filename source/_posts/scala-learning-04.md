---
layout:     post
title:      "《Scala编程》阅读记录——列表进阶"
date:       2018-07-24 11:25:00
categories: Computer Programes
tags:   ๑Scala
---

> 不适合人类阅读的学习笔记

## 第十六章 使用列表
---

- [列表的使用方法表格见另一篇博客](https://fleschier.github.io/2018/07/Scala-infos/)

- 列表跟数组非常像，但是有两个重要的区别：
1. 列表是不可变的，也就是说列表的元素不能通过赋值改变
2. 列表是递归的(即链表)，而数组是平的

- `init`和`last`要消耗的时间与列表的长度成正比，而`head`和`tail`消耗常量级别的时间

- `indices`方法返回包含了指定列表所有有效的下标，所以一般用在for表达式遍历列表时：
```
val lst = new List("af","g3g","g53v")
for( i <- lst.indices){ //这里i即是从lst的第一个有效下标开始直到最后一个下标
  ...
}
```

### `flatten`方法：接受一个列表的列表并返回单个列表

- 例子：
```
scala> List(List(1,2),List(3),List(),List(4,5)).flatten
res0: List[Int] = List(1,2,3,4,5)
```

- 例子：
![](/images/Scala/flatten_test.jpg)

### `zip`和`unzip`

- zip操作接受两个列表，返回一个有对偶组成的列表

- 如果两个列表的元素个数不同，那么任何没有配对上的元素将被丢弃

#### `zipWithIndex`方法

- 例子：
```
scala> val abcde = List('a','b','c','d','e')
abcde: List[Char] = List(a,b,c,d,e)
scala> abcde.zipWithIndex
res0: List[(Char,Int)] = List((a,0),(b,1),(c,2),(d,3),(e,4))
```

- 任何元组的列表都可以通过unzip方法转换回由列表组成的元组

### 显示列表

- 下面一些例子：
```
scala> abcde mkString("[", ",", "]")
res0: String = [a,b,c,d,e]
scala> abcde mkString ""
res1: String = abcde
scala> abcde.mkString
res2: String = abcde
scala> abcde mkString ("List(", ", ", ")")
res3: String = List(a,b,c,d,e)
```

### 过滤列表

- `filter`，`partition`，`find`，`takeWhile`，`dropWhile`和`span`

- 这些过滤函数的参数都是`T => Boolean`类型的

- `x.takeWhile(p)`返回x列表中连续满足p的最长前缀，例：`nums.takeWhile(_ > 0)`

- `x.dropWhile`将去除列表x中连续满足p的最长前缀，例：`words.dropWhile(_.startsWith("t"))`

### 对列表前提条件的检查

- `forall`和`exists`

- `xs.forall(p)`，如果列表中所有元素都满足p则返回true

- `xs.exists(p)`，如果列表中有至少一个元素满足p则返回true


<br>
> 最后更新于2018.7.24
