---
layout:     post
title:      "Scala方法查询记录"
date:       2018-07-12 16:40:00
categories: Computer Programs
tags:   ๑Scala
description: "学习记录"
---

> 仅供查询，禁止转载

- 一般的Int类型的都可以通过`.max`和`.min`获取最大最小元素

## List的一些方法和用途

|方法|用途|
|---|---|
|List()或者Nil|表示空列表|
|List("Cool","Tools")|创建一个新的List[String],包含两个值:"Cool","Tools"|
|val thrill = "Will"::"Fill"::Nil|创建一个新的List[String]包含两个值："Will"和"Fill"|
|List("a","b"):::List("c","d")|将两个列表拼接起来(返回一个新的列表List("a","b","c","d"))|
|thrill(2)|返回列表thrill下标为2(从0开始计数)|
|thrill.count(s => s.length == 4)|对thrill中长度为4的字符串进行计数|
|thrill.drop(2)|返回去掉了thrill的头两个元素的列表|
|thrill.dropRight(2)|返回去掉了thrill后两个元素的列表|
|thrill.exists(s => s=="until")|判断thrill中是否有字符串元素的值为"until"，返回值为Boolean|
|thrill.filter(s => s.length == 4)|按顺序返回列表thrill中所有长度为4的元素列表|
|thrill.forall(s => s.endsWith("1"))|表示列表中是否所有元素都以字母"1"结尾|
|thrill.foreach(s => println(s)) / thrill.foreach(println)|遍历列表执行打印|
|thrill.head|返回列表的首个元素|
|thrill.init|返回列表thrill除最后一个元素之外其他元素组成的列表|
|thrill.isEmpty|判断列表是否为空|
|thrill.last|返回thrill的最后一个元素|
|thrill.length|返回列表的元素个数|
|thrill.map(s => s + "y")|返回一个对列表thrill所有字符串元素末尾添加"y"的新字符串列表|
|thrill.makeString", "|返回用列表thrill的所有元素组合成的字符串，以", "连接各个元素|
|thrill.filterNot(s => s.length == 4)|按顺序返回列表中所有长度不为4的元素列表|
|thrill.reverse|返回包含列表thrill的逆序列表|
|thrill.sort( (s,t) => s.charAt(0).toLower < t.charAt(0).toLower)|返回包含thrill的所有元素，按照首字母小写顺序排序的列表|
|thrill.tail|返回列表thrill除首个元素之外其他元素组成的列表|

## 常用的集操作

|操作|效果|
|---|---|
|val nums = Set(1,2,3)|创建一个不可变集(nums.toString返回Set(1,2,3))|
|nums + 5|添加一个元素(返回Set(1,2,3,5))|
|nums - 3|移除一个元素(返回Set(1,2))|
|nums ++ List(5,6)|添加多个元素(返回Set(1,2,3,5,6))|
|nums -- List(1,2)|移除多个元素(返回Set(3))|
|nums & Set(1,3,5,7)|获取两个集的交集(返回Set(1,3))|
|nums.size|返回集的大小(返回3)|
|nums.contains(3)|检查是否包含(此处返回true)|
|import scala.collection.mutable|让可变集易于访问|
|val words = mutable.Set.empty[String]|创建一个空的可变集(words.toString将返回Set())|
|words += "the"|添加一个元素(words.toString将返回Set(the))|
|words -= "the"|移除一个元素，如果这个元素存在(words.toString将返回Set())|
|words ++= List("do","re","mi")|添加多个元素(words.toString将返回Set(do,re,mi))|
|words --= List("do","re")|移除多个元素(words.toString将返回Set(mi))|
|words.clear|移除所有元素(words.toString将返回Set())|

- [更详细的链接](https://docs.scala-lang.org/zh-cn/overviews/collections/sets.html)

## 常用的映射操作

|操作|效果|
|---|---|
|val nums = Map("i" -> 1, "ii" -> 2)|创建一个不可变映射(nums.toString返回Map(i -> 1, ii -> 2))|
|nums + ("vi" -> 6)|添加一个条目(返回Map(i -> 1, ii -> 2, vi -> 6))|
|nums - "ii"|移除一个条目(返回Map(i -> 1))|
|nums ++ List("iii" -> 3, "v" -> 5)|添加多个条目(返回Map(i -> 1, ii -> 2, iii -> 3, v -> 5))|
|nums -- List("i","ii")|移除多个条目(返回Map())|
|nums.size|返回映射的大小(返回2)|
|nums.contains("ii")|检查是否包含(返回true)|
|nums("ii")|获取指定键的值(返回2)|
|nums.keys|返回所有键(返回字符串"i"和"ii"的Iterable)|
|nums.keySet|以集的形式返回所有的键(返回Set(i,ii))|
|nums.values|返回所有的值(返回整数1和2的Iterable)|
|nums.isEmpty|表示映射是否为空|
|import scala.collection.mutable|让可变集合易于访问|
|val words = mutable.Map.empty[String,Int]|创建一个空的可变映射|
|words += ("one" -> 1, "two" -> 2, "three" -> 3)|添加一个从"one"到1的映射条目|
|words -= "one"|移除一个映射条目，如果存在|
|words ++= List("one" -> 1, "two" -> 2, "three" -> 3)|添加多个条目|
|words --= List("one","two")|移除多个条目|

- [更详细的链接](https://docs.scala-lang.org/zh-cn/overviews/collections/maps.html)

## 序列

|操作|说明|
|---|---|
|索引和长度的操作 apply、isDefinedAt、length、indices，及lengthCompare|序列的apply操作用于索引访问；因此，Seq[T]类型的序列也是一个以单个Int（索引下标）为参数、返回值类型为T的偏函数。换言之，Seq[T]继承自Partial Function[Int, T]。序列各元素的索引下标从0开始计数，最大索引下标为序列长度减一。序列的length方法是collection的size方法的别名。lengthCompare方法可以比较两个序列的长度，即便其中一个序列长度无限也可以处理。|
|索引检索操作（indexOf、lastIndexOf、indexofSlice、lastIndexOfSlice、indexWhere、lastIndexWhere、segmentLength、prefixLength）|用于返回等于给定值或满足某个谓词的元素的索引。|
|加法运算（+:，:+，padTo）|用于在序列的前面或者后面添加一个元素并作为新序列返回。|
|更新操作（updated，patch）|用于替换原序列的某些元素并作为一个新序列返回。|
|排序操作（sorted, sortWith, sortBy）|根据不同的条件对序列元素进行排序。|
|反转操作（reverse, reverseIterator, reverseMap）|用于将序列中的元素以相反的顺序排列。|
|比较（startsWith, endsWith, contains, containsSlice, corresponds）|用于对两个序列进行比较，或者在序列中查找某个元素。|
|多集操作（intersect, diff, union, distinct）|用于对两个序列中的元素进行类似集合的操作，或者删除重复元素。|

## Seq类的操作

|WHAT IT IS|WHAT IT DOES|
|---|---|
|索引和长度|-----------------------------------|
|xs(i)|	(或者写作xs apply i)。xs的第i个元素|
|xs isDefinedAt i|	测试xs.indices中是否包含i。|
|xs.length|序列的长度（同size）。|
|xs.lengthCompare ys|如果xs的长度小于ys的长度，则返回-1。如果xs的长度大于ys的长度，则返回+1，如果它们长度相等，则返回0。即使其中一个序列是无限的，也可以使用此方法。|
|xs.indices|xs的索引范围，从0到xs.length - 1。|
|索引搜索|-----------------------------------|
|xs indexOf x|返回序列xs中等于x的第一个元素的索引（存在多种变体）。|
|xs lastIndexOf x|返回序列xs中等于x的最后一个元素的索引（存在多种变体）。|
|xs indexOfSlice ys|查找子序列ys，返回xs中匹配的第一个索引。|
|xs indexOfSlice ys|查找子序列ys，返回xs中匹配的倒数一个索引。|
|xs indexWhere p|xs序列中满足p的第一个元素。（有多种形式）|
|xs segmentLength (p, i)|xs中，从xs(i)开始并满足条件p的元素的最长连续片段的长度。|
|xs prefixLength p|xs序列中满足p条件的先头元素的最大个数。|
|加法|-----------------------------------|
|x +: xs|由序列xs的前方添加x所得的新序列。|
|xs :+ x|由序列xs的后方追加x所得的新序列。|
|xs padTo (len, x)|在xs后方追加x，直到长度达到len后得到的序列。|
|更新|-----------------------------------|
|xs patch (i, ys, r)|将xs中第i个元素开始的r个元素，替换为ys所得的序列。|
|xs updated (i, x)|将xs中第i个元素替换为x后所得的xs的副本。|
|xs(i) = x|（或写作 xs.update(i, x)，仅适用于可变序列）将xs序列中第i个元素修改为x。|
|排序|-----------------------------------|
|xs.sorted|通过使用xs中元素类型的标准顺序，将xs元素进行排序后得到的新序列。|
|xs sortWith lt|将lt作为比较操作，并以此将xs中的元素进行排序后得到的新序列。|
|xs sortBy f|将序列xs的元素进行排序后得到的新序列。参与比较的两个元素各自经f函数映射后得到一个结果，通过比较它们的结果来进行排序。|
|反转|-----------------------------------|
|xs.reverse|与xs序列元素顺序相反的一个新序列。|
|xs.reverseIterator|产生序列xs中元素的反序迭代器。|
|xs reverseMap f|以xs的相反顺序，通过f映射xs序列中的元素得到的新序列。|
|比较|-----------------------------------|
|xs startsWith ys|测试序列xs是否以序列ys开头（存在多种形式）。|
|xs endsWith ys|测试序列xs是否以序列ys结束（存在多种形式）。|
|xs contains x|测试xs序列中是否存在一个与x相等的元素。|
|xs containsSlice ys|	测试xs序列中是否存在一个与ys相同的连续子序列。|
|(xs corresponds ys)(p)|测试序列xs与序列ys中对应的元素是否满足二元的判断式p。|
|多集操作|-----------------------------------|
|xs intersect ys|序列xs和ys的交集，并保留序列xs中的顺序。|
|xs diff ys|序列xs和ys的差集，并保留序列xs中的顺序。|
|xs union ys|并集；同xs ++ ys。|
|xs.distinct|不含重复元素的xs的子序列。|

## Buffer类的操作

|WHAT IT IS|WHAT IT DOES|
|---|---|
|加法：|-----------------------------------|
|buf += x|将元素x追加到buffer，并将buf自身作为结果返回。|
|buf += (x, y, z)|将给定的元素追加到buffer。|
|buf ++= xs|将xs中的所有元素追加到buffer。|
|x +=: buf|将元素x添加到buffer的前方。|
|xs ++=: buf|将xs中的所有元素都添加到buffer的前方。|
|buf insert (i, x)|将元素x插入到buffer中索引为i的位置。|
|buf insertAll (i, xs)|将xs的所有元素都插入到buffer中索引为i的位置。|
|移除：|-----------------------------------|
|buf -= x|将元素x从buffer中移除。|
|buf remove i|将buffer中索引为i的元素移除。|
|buf remove (i, n)|将buffer中从索引i开始的n个元素移除。|
|buf trimStart n|移除buffer中的前n个元素。|
|buf trimEnd n|移除buffer中的后n个元素。|
|buf.clear()|移除buffer中的所有元素。|
|克隆：|-----------------------------------|
|buf.clone|与buf具有相同元素的新buffer。|

## Traversable对象的操作

|WHAT IT IS	|WHAT IT DOES|
|---|---|
|抽象方法：|	 |
|xs foreach f	|对xs中的每一个元素执行函数f|
|加运算（Addition）：|	 |
|xs ++ ys	|生成一个由xs和ys中的元素组成容器。ys是一个TraversableOnce容器，即Taversable类型或迭代器。|
|Maps:	 ||
|xs map f	|通过函数xs中的每一个元素调用函数f来生成一个容器。|
|xs flatMap f	|通过对容器xs中的每一个元素调用作为容器的值函数f，在把所得的结果连接起来作为一个新的容器。|
|xs collect f	|通过对每个xs中的符合定义的元素调用偏函数f，并把结果收集起来生成一个集合。|
|转换（Conversions）：	 ||
|xs.toArray	|把容器转换为一个数组|
|xs.toList|	把容器转换为一个list|
|xs.toIterable|	把容器转换为一个迭代器。|
|xs.toSeq	|把容器转换为一个序列|
|xs.toIndexedSeq|	把容器转换为一个索引序列|
|xs.toStream|	把容器转换为一个延迟计算的流。|
|xs.toSet	|把容器转换为一个集合（Set）。|
|xs.toMap	|把由键/值对组成的容器转换为一个映射表（map）。如果该容器并不是以键/值对作为元素的，那么调用这个操作将会导致一个静态类型的错误。|
|拷贝（Copying）：	 ||
|xs copyToBuffer buf	|把容器的所有元素拷贝到buf缓冲区。|
|xs copyToArray(arr, s, n)|	拷贝最多n个元素到数组arr的坐标s处。参数s，n是可选项。|
|大小判断（Size info）：	 ||
|xs.isEmpty	|测试容器是否为空。|
|xs.nonEmpty	|测试容器是否包含元素。|
|xs.size	|计算容器内元素的个数。|
|xs.hasDefiniteSize	|如果xs的大小是有限的，则为true。|
|元素检索（Element Retrieval）：	 ||
|xs.head	|返回容器内第一个元素（或其他元素，若当前的容器无序）。|
|xs.headOption|	xs选项值中的第一个元素，若xs为空则为None。|
|xs.last	|返回容器的最后一个元素（或某个元素，如果当前的容器无序的话）。|
|xs.lastOption	|xs选项值中的最后一个元素，如果xs为空则为None。|
|xs find p|	查找xs中满足p条件的元素，若存在则返回第一个元素；若不存在，则为空。|
|子容器（Subcollection）：	||
|xs.tail|	返回由除了xs.head外的其余部分。|
|xs.init|	返回除xs.last外的其余部分。|
|xs slice (from, to)|	返回由xs的一个片段索引中的元素组成的容器（从from到to，但不包括to）。|
|xs take n	|由xs的第一个到第n个元素（或当xs无序时任意的n个元素）组成的容器。|
|xs drop n	|由除了xs take n以外的元素组成的容器。|
|xs takeWhile p	|容器xs中最长能够满足断言p的前缀。|
|xs dropWhile p	|容器xs中除了xs takeWhile p以外的全部元素。|
|xs filter p|	由xs中满足条件p的元素组成的容器。|
|xs withFilter p|	这个容器是一个不太严格的过滤器。子容器调用map，flatMap，foreach和withFilter只适用于xs中那些的满足条件p的元素。|
|xs filterNot p	|由xs中不满足条件p的元素组成的容器。|
|拆分（Subdivision）：	 ||
|xs splitAt n	|把xs从指定位置的拆分成两个容器（xs take n和xs drop n）。|
|xs span p|	根据一个断言p将xs拆分为两个容器（xs takeWhile p, xs.dropWhile p）。|
|xs partition p	|把xs分割为两个容器，符合断言p的元素赋给一个容器，其余的赋给另一个(xs filter p, xs.filterNot p)。|
|xs groupBy f	|根据判别函数f把xs拆分一个到容器（collection）的map中。|
|条件元素（Element Conditions）：	 ||
|xs forall p|	返回一个布尔值表示用于表示断言p是否适用xs中的所有元素。|
|xs exists p	|返回一个布尔值判断xs中是否有部分元素满足断言p。|
|xs count p	|返回xs中符合断言p条件的元素个数。|
|折叠（Fold）：||	 
|(z /: xs)(op)|	在xs中，对由z开始从左到右的连续元素应用二进制运算op。|
|(xs :\ z)(op)	|在xs中，对由z开始从右到左的连续元素应用二进制运算op|
|xs.foldLeft(z)(op)|	与(z /: xs)(op)相同。|
|xs.foldRight(z)(op)|	与 (xs :\ z)(op)相同。|
|xs reduceLeft op	|非空容器xs中的连续元素从左至右调用二进制运算op。|
|xs reduceRight op|	非空容器xs中的连续元素从右至左调用二进制运算op。|
|特殊折叠（Specific Fold）：	 ||
|xs.sum	|返回容器xs中数字元素的和。|
|xs.product	|xs返回容器xs中数字元素的积。|
|xs.min|	容器xs中有序元素值中的最小值。|
|xs.max	|容器xs中有序元素值中的最大值。|
|字符串（String）：	||
|xs addString (b, start, sep, end)|	把一个字符串加到StringBuilder对象b中，该字符串显示为将xs中所有元素用分隔符sep连接起来并封装在start和end之间。其中start，end和sep都是可选的。|
|xs mkString (start, sep, end)	|把容器xs转换为一个字符串，该字符串显示为将xs中所有元素用分隔符sep连接起来并封装在start和end之间。其中start，end和sep都是可选的。|
|xs.stringPrefix|	返回一个字符串，该字符串是以容器名开头的xs.toString。|
|视图（View）：	 ||
|xs.view|	通过容器xs生成一个视图。|
|xs view (from, to)	|生成一个表示在指定索引范围内的xs元素的视图。|

## Trait Iterable操作

|WHAT IT IS	|WHAT IT DOES|
|---|---|
|抽象方法：	 ||
|xs.iterator	xs|迭代器生成的每一个元素，以相同的顺序就像foreach一样遍历元素。|
|其他迭代器：	 ||
|xs grouped size|	一个迭代器生成一个固定大小的容器（collection）块。||
|xs sliding size	|一个迭代器生成一个固定大小的滑动窗口作为容器（collection）的元素。|
|子容器（Subcollection）：||	 
|xs takeRight n	|一个容器（collection）由xs的最后n个元素组成（或，若定义的元素是无序，则由任意的n个元素组成）。|
|xs dropRight n	|一个容器（collection）由除了xs 被取走的（执行过takeRight （）方法）n个元素外的其余元素组成。|
|拉链方法（Zippers）：	||
|xs zip ys|	把一对容器 xs和ys的包含的元素合成到一个iterabale。|
|xs zipAll (ys, x, y)	|一对容器 xs 和ys的相应的元素合并到一个iterable ，实现方式是通过附加的元素x或y，把短的序列被延展到相对更长的一个上。|
|xs.zip WithIndex	|把一对容器xs和它的序列，所包含的元素组成一个iterable 。|
|比对：	 ||
|xs sameElements ys	|测试 xs 和 ys 是否以相同的顺序包含相同的元素。|

<br>
> 最后更新于2018.7.26
