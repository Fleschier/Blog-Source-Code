---
layout:     post
title:      "《Scala编程》阅读记录——类进阶"
date:       2018-07-23 17:40:00
categories: Computer Programes
tags:   ๑Scala
---

> 不适合人类阅读的学习笔记



## 第十章 组合和继承  面向对象进阶

### 抽象类

- 例子：
```
abstract class Element{
	def contents: Array[String]
}
```
注意，Element类中content方法没有标上abstract修饰符。一个方法只要是没有实现的(即没有等号或方法体)，那么它就是抽象的。跟Java不同，我们不能对方法加上abstract修饰符


### 定义无参方法

- 例子：
```
abstract class Element {
	def contents: Array[String]
	def height: Int = contents.length
	def width: Int = if(height == 0) 0 else contents(0).length
}
```

- 这个无参方法的特点是，如果将`def`换成`val`，那么他就成了一个字段而不会有编译错误

- 在这里无参方法和字段的区别是：字段的调用会更加快，但是每次实例化对象都要分配内存空间。具体取舍要看具体的用法。

- 总结下来就是，scala推荐我们将那些没有参数也没有副作用的方法定义为无参方法，而对于无参数而有副作用的方法不应当省略空括号，例如：
```
"hello".length  //没有()，因为没有副作用
println()	//有()，因为有副作用
```

### 扩展类

- 使用`extends`关键字，相当于继承

- scala中所有类的默认父类是AnyRef

- 继承的意思是超类的所有成员也是子类的成员，但是有两个例外：
一个是超类的私有成员不会被子类继承；
二是如果子类实现了相同名称和参数的成员，那么该成员不会被继承(重写，override)

- scala只有两个命名空间用于定义：
1. 值(字段，方法，包和单例对象)
2. 类型(类和特质名)

- 因此scala可以用val来重写一个无参方法(即将一个无参方法重写为一个字段)

- 如果我们要在子类中重写父类的方法，则要在方法前加上override修饰符：`override def funcName(...){...}`

- 使用final修饰符来确保某个成员不能被子类继承

- scala的继承关系图
![](/images/Scala/relation.jpg)

## 第十二章 特质
---

- 特质的定义跟类定义很像，除了关键字trait

- scala可以使用`extends`或者`with`关键字来 *混入* 特质，而不是继承。

- 例子：`class Frog extends Animal with Philosophical with HasLegs{..}`
混入多个特质用`with`连接

### 要点如下:

- **Scala中类只能继承一个超类, 可以扩展任意数量的特质**

- 特质可以要求实现它们的类具备特定的字段, 方法和超类

- 与Java接口不同, Scala特质可以提供方法和字段的实现

- 当将多个特质叠加使用的时候, 顺序很重要

- [scala特质详细解析](https://www.cnblogs.com/nowgood/p/scalatrait.html)

- 重写特质的抽象方法时, 不需要`override`关键字

- 可以为类和对象添加多个相互调用的特质时, 从最后一个开始调用. 这对于需要分阶段加工处理某个值的场景很有用.

## 第十三章 包和引入
---

- scala的引入可以出现在任何地方，不仅仅是某个编译单元的开始

- 例如，假设一个Fruit类，其中有有name和color字段。有如下的一个函数：
```
def showFruit(fruit: Fruit) = {
	import Fruit._
	println(name + "s are" + color)
}
```
showFruit引入了其参数fruit(Fruit类)的所有成员。下面的name和color就相当于fruit.name和fruit.color

## 第十四章 断言和测试
---

- 在scala中，断言的写法是对预定义方法assert的调用。

- 表达式：`assert(condition)`。如果condition不满足则抛出AssertionError

- 另一种：`assert(condition,explanation)`如果condition不满足则抛出指定的explanation的AssertionError

## 第十五章 样例类和模式匹配
---

- 样例类使用case关键字修饰，scala编译器会自动创建工厂方法，即可以直接用`className(parameter1,parameter2,...)`而不用`new`关键字即可创建对象

- 模式匹配，例子：
```
expr match{
	case BinOp(...) => println(...)
	case _ =>  //处理器默认case,这一行是必须的，否则所有非满足第一个条件的case都会返回MatchError
}
```
通配模式(`_`)会匹配任何对象

## 第二十章 抽象成员
---

- 所有四种抽象成员：`val`，`var`，方法和类型

- 例子：下面这个特质声明了四种抽象成员：一个抽象类型(T)，一个抽象方法(transform)，一个val(initial)和一个var(current)
```
trait Anstract{
	type T
	def transform(x: T): T
	val initial: T
	var current: T
}
```
- scala的抽象类型指的是用type关键字声明为某个类或者特质的成员(但并不给出定义)的类型。类或者特质都不能够叫抽象类型，抽象类型永远是某个类或者特质的成员，比如Abstract特质中的T

- `lazy`关键字：如果在`val`关键字前面加上`lazy`关键字，则该变量会在第一次被使用时被赋值。

- T是指一个在声明时还未知的类型。不同的子类可以提供不同的T的实现


<br>
> 最后更新于2018.7.24
