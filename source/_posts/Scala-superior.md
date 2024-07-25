---
layout:     post
title:      "Scala学习笔记——进阶"
date:       2018-04-6 16:47:00
categories: Computer Programs
tags: ๑Scala
description: "学习记录"
---

> 不适合人类阅读的学习笔记  

## case class与模式匹配
---
- case class一般被翻译为样例类，它是一种特殊的类，能够被优化以用于模式匹配。

-

## scala性能测试
---
- 测试程序的运行时间的函数：`System.currentTimeMillis()`

- 用法：
```
[...]
  val time = System.currentTimeMillis()
  [要测试运行时间的代码段]
  println(" 耗时: " + (System.currentTimeMillis() - time))  //以时间差来看运行时间
[...]
```

## 函数式循环
---

- 函数式编程的循环都是用迭代来实现的

- 例1：对于一个Int数组a,对里面每个元素执行 +1的操作
```
a.map{x =>
  val y = x + 1  //因为Int是不可变类型，所以必须要新建一个值来存储改变后的值
  y  //返回值是y
}
```

- 例2：对于一个Int数组，每找出一个大于5的数count就加1
```
var count:Int = 0
a.foreach{x =>      //与map遍历方式不同，foreach不会对里面的内容修改，所以匿名函数也不需要返回值
  if(x >  5)
    count += 1
}
```

## 一些数据结构的使用
---

### ListBuffer:

- 首先需要引入包 `import scala.collection.mutable.ListBuffer`

- 在使用之前，先声明一个ListBuffer变量，通过以下代码：
`val buf = new ListBuffer[Int]()    //类型自定义，这里采用的是Int`

- 在末尾进行追加，使用append()方法：
`buf.append(x)`

- 将ListBuffer转化为List:
`val lst = buf.toList`

## Scala类的实例
---

-
```
class Point(xc: Int, yc: Int) {
   var x: Int = xc
   var y: Int = yc
   def move(dx: Int, dy: Int) {
      x = x + dx
      y = y + dy
      println ("x 的坐标点: " + x);
      println ("y 的坐标点: " + y);
   }
}
```

- Scala中的类不声明为public，一个Scala源文件中可以有多个类。以上实例的类定义了两个变量 x 和 y ，一个方法：move，方法没有返回值。Scala 的类定义可以有参数，称为类参数，如上面的 xc, yc，类参数在整个类中都可以访问。

- 类的字段要初始化，不然会报错(错误：类必须申明为抽象类才行)

## scala的一些笔记综合
---

### this关键字与构造函数

#### 主构造函数

- Scala提供了一个类的主构造函数的概念。如果代码只有一个构造函数，则可以不需要定义明确的构造函数。它有助于优化代码，可以创建具有零个或多个参数的主构造函数。

- scala主构造函数示例：(即在类中以参数的形式体现)
```
class Student(id:Int, name:String){  
    def showDetails(){  
        println(id+" "+name);  
    }  
}  
object Demo{  
    def main(args:Array[String]){  
        var s = new Student(1010,"Maxsu");  
        s.showDetails()  
    }  
}
```

#### 次要(辅助)构造器

- 可以在类中创建任意数量的辅助构造函数，必须要从辅助构造函数内部调用主构造函数。**this关键字用于从其他构造函数调用构造函数**。当调用其他构造函数时，**确保要将其放在构造函数中的第一行**。

- Scala二次构造函数示例：
```
class Student(id:Int, name:String){  
    var age:Int = 0  
    def showDetails(){  
        println(id+" "+name+" "+age)  
    }  
    def this(id:Int, name:String,age:Int){  
        this(id,name)       // Calling primary constructor, and it is first line  
        this.age = age  
    }  
}  
object Demo{  
    def main(args:Array[String]){  
        var s = new Student(1010,"Maxsu", 25);  
        s.showDetails()  
    }  
}
```

- 并且在this二次构造函数的第一个语句，调用主构造函数this()的参数与主构造函数一致(如上例中的id和name两个参数)。

<br>

> 最后更新于2018.5.27
