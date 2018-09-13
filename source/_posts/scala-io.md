---
layout:     post
title:      "Scala IO 记录"
date:       2018-09-06 11:25:00
categories: Computer Programes
tags:   ๑Scala
---

## 控制台IO
---

### 调用java的IO库

- scala使用java的io类来读取

- 需要引入java的io类：`import java.io._`

- 使用Java的`BufferedReader`和`InputStreamReader`方法来实现

- 例：
```
val br = new BufferedReader(new InputStreamReader(System.in))
val x = br.readLine().trim  //注意readLine的L是大写
```

- 所有的读入的内容都是String类型，可以使用`toInt`，`toDouble`等方法来将输入转化成各种需要的格式

### 调用scala的IO库

- 例:
```
import scala.io._
object Test {
   def main(args: Array[String]) {
      val line = StdIn.readLine()
      ...
   }
}
```

- scala的IO库更为简洁，可以调用`readInt()`,`readBoolean`等一系列方法，直接进行转换。

> Scala2.11 后的版本 Console.readLine 已废弃，使用 scala.io.StdIn.readLine() 方法代替。

## 文件IO
---

- 需要引入`scala.io`库

- 例子(读取test.txt文件的内容)：
```
import scala.io.Source

object Test {
   def main(args: Array[String]) {
      println("文件内容为:" )
      Source.fromFile("test.txt" ).foreach{
         println
      }
   }
}
```
