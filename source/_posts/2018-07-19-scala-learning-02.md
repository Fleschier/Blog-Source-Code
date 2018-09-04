---
layout:     post
title:      "《Scala编程》阅读记录——进阶部分"
date:       2018-07-19 10:40:00
categories: Computer Programes
tags:   ๑Scala
---

> 不适合人类阅读的学习笔记

## 概念
---

### 序列

- Seq trait用于表示序列。所谓序列，指的是一类具有一定长度的可迭代访问的对象，其中每个元素均带有一个从0开始计数的固定索引位置。

- 常用线性序列有 `scala.collection.immutable.List`和`scala.collection.immutable.Stream`。常用索引序列有 `scala.Array scala.collection.mutable.ArrayBuffer`。Vector 类提供一个在索引访问和线性访问之间有趣的折中。它同时具有高效的恒定时间的索引开销，和恒定时间的线性访问开销。正因为如此，对于混合访问模式，vector是一个很好的基础。

### 缓冲器

- Buffers是可变序列一个重要的种类。它们不仅允许更新现有的元素，而且允许元素的插入、移除和在buffer尾部高效地添加新元素。buffer 支持的主要新方法有：用于在尾部添加元素的`+=` 和 `++=`；用于在前方添加元素的`+=:` 和 `++=:` ；用于插入元素的 `insert`和`insertAll`；以及用于删除元素的 `remove` 和 `-=`。

## 第四章
---

### 类和对象

- 在类定义中，我们会填入字段(field)和方法(method)，这些统称为成员(member)

- 保持健壮性，我们可以将字段声明为私有(在字段前面加上private修饰符)，访问和修改都通过方法来实现。
scala的默认访问级别是public

- scala方法参数有一个特征，就是 **它们都是`val`而不是`var`**

- 一个类的例子：
```
class test{
	private var sum = 0
	def add(b: Byte): Unit = {
		sum += b
	}
	def checksum(): Int = {
		return ~(sum & 0xFF) + 1
	}
}
```

- 在方法中，没有任何显式的return语句时，**scala返回的是该方法计算出的最后一个(表达式的)值** ,因此上面这个例子的return语句可以省略不写
- 同时，另一种方法的简写方式是，当一个方法只会计算一个返回结果的表达式时，可以不写花括号。如果这个表达式很短，他甚至可以被放置在def的同一行。为了极致的精简，还可以省略掉结果类型。

- 更改后的写法：
```
class test{
	private var sum = 0
	def add(b: Byte) = sum += b
	def checksum() = ~(sum & 0xFF) + 1
}
```
在这段代码中，scala能够正确地推断出add和checksum这两个方法的结果类型。但是最好的写法是显式地给出结果类型，这样便于代码的调试和维护

- 本例中的add方法结果类型为Unit，执行它的目的就是产生副作用。对于那些仅仅为了其副作用而被执行的方法被称作*过程*。

- 一般分号是没有必要加的，但是如果一行写多个语句，则用分号间隔

### 单例对象

- scala比Java更面向对象一点，是scala **不允许有静态成员**。
因此，scala提供了*单例对象*，单例对象与普通的类很像，只是将`class`关键字换成了`object`

- 当单例对象跟某个类共用同一个名字时，它被称作这个类的 **伴生对象(companion object)**

- 必须在同一个源码文件中定义类和类的伴生对象，同时，类又叫做这个单例对象的 **伴生类(companion class)**

- 类和它的伴生对象可以互相访问对方的私有成员

- 单例对象当中的方法可以像Java中的静态方法一样直接通过类名来访问

- 单例对象不仅仅用来存放静态方法，他是一等的对象，可以把单例对象想象成附加在对象身上的“名字标签”

- 类和单例对象的区别是单例对象不能被实例化(即没法new一个单例对象，除非这个单例对象有伴生类)

- 单例对象在有代码首次访问时才会被初始化

- 没有同名的伴生类的单例对象称为 *孤立对象*(standalone object)，一般用来将工具方法归集在一起，或定义scala程序的入口。

### scala应用程序

- 要运行一个scala程序，必须提供一个孤立对象，这个孤立对象需要包含一个main方法，该方法接收一个Array[String]作为参数，结果类型为Unit,例如：
```
object Test{
	def main(args: Array[String]): Unit = {
		...
	}
}
```

> 注意：scala在每一个源码文件都隐式地引入了java.lang和scala包的成员，以及名为Predef的单例对象的所有成员。例如使用的println和assert都是来自于Predef

- 注意要运行这个程序，那么文件名需要与这个单例对象的名称相同。

### App特质

- scala提供了一个特质scala.App，我们可以不用编写main方法，而是将打算放在main方法里的代码直接写在单例对象的花括号里。不过首先要在单例对象名后加上`extends App`。例子：
```
object AppTest extends App{
	for(i <- 0 to 10){
		println("...")
	}
}
```
它可以像正常的scala程序一样运行

## 第五章
---

### 基础类型和操作

#### 一些基础类型

- Byte、Short、Int、Long和Char类型统称为 *整数类型*，整数类型加上Float和Double类型统称为 *数值类型*

- String是java.lang包的成员

- 注意这些数据类型实际上都是封装好的类，所以首字母都是大写

- Long类型以l或者L结尾

- 字符串插值：
```
val name="reader"
println(s"Hello, $name")
```

- 这个的结果与`println("Hello" + name)`是一样的

- scala中raw可以屏蔽转义字符`/`，例如`println(raw"abc\n\n")`其中斜杠和n将被原样输出

- scala中判断任意两个对象都可以用`==`方法，甚至可以是与null值进行比较而不会报错，并且总能返回正确的比较结果。scala的`==` **只比较值**，而Java的引用类型的==比较的是引用是否相同。

- 赋值操作符`=`的优先级是最低的,而像`*=`这样的操作符也被当做赋值操作符，因此其优先级不如`+`操作符


## 第六章 函数式对象
---

- 如果要在类中重新实现一个已经实现的方法，例如toString方法，要用到override关键字

- 例如`override def toString = {...}`

- 一个例子：创建一个有理数的类，这是个不可变的类并且要求分母不为零
```
class Rational(n: Int, d:Int){
	require(d!=0)
	override def toString = n + "/" + d
}
```
require方法接受一个boolean的参数。如果传入的参数为true，require将会正常返回。否则,require将会抛出IllegalArgumentException来阻止对象的构建。

### 添加字段

- 例如添加一个add方法：
```
def add(that: Rational): Rational = new(
	new Rational(n * that.d + that.n * d, d * that.d)
)
```
这个方法是会报错的

- 上面那个类如果要添加一个add方法，实现两个Rational类型的值的相加，此时add是不能直接调用this.n或者this.d的(虽然类参数n和d在add方法中是在作用域内的，但是编译器并不允许使用`that.n`和`that.d`，因为that并非指向调用add的那个对象，要访问that的d和n，需要将它做成字段(相当于成员变量))
我们需要添加字段才行：
```
class Rational(n: Int, d:Int){
	require(d != 0)
	val numer: Int = n
	val denom: Int = d
	override def toString = numer + "/" + denom
	def add(that: Rational): Rational =
		new Rational(
			numer * that.denom + that.numer * denom,
			denom * that.denom		
		)
}
```

- scala中 字段 默认的访问权限是public

### 自引用

- 使用关键字this，写法为`this.字段名`，也可以直接写字段名，用法与C++和Java一致

- 辅助构造方法：
`def this(...){...}`

- 操作符也可以像方法一样定义，例如：
```
def + (that: MyClass): MyClass ={...}
```

- scala支持方法重载，用法与C++和Java相同，通过定义多个参数不同的同名函数来实现重载


## 第七章 内建的控制结构
---

- scala的控制语句都有返回值，可以直接拿来用

- 例子：`println(if (!args.isEmoty) args(0) else "default.txt")`


- 形如 `a <- b`的称为生成器语法

- `1 to 4` 包含上界 4
- `1 until 4` 不包含上界 4



### 过滤

- 有时候遍历集合的时候不想完整地遍历集合，而是先过滤成一个子集。这时可以给for表达式添加过滤器(filter)
例：
```
val filesHere = (new java.io.File(".")).listDiles
for(file <- filesHere if file.getName.endsWith(".scala"))
	println(file)
```
- 过滤器就是for表达式圆括号中的一个if子句，并且可以随意添加更多的过滤器，直接添加if子句即可

### 嵌套迭代

- 如果添加多个`<-`子句，将得到嵌套的循环
例：
```
def fileLines(file: java.io.File) =
	scala.io.Source.fromFile(file).getLines().toList
def grep(pattern: String) =
	for(
		file <- filesHere
		if file.getName.endsWith(".scala");
		trimed = line.trim
		line <- fileLines(file)
		if trimed.matches(pattern)
	)
	println(file + ": " + line.trimed)
grep(".*gcd.*")
```
- 其中，外部循环遍历filesHere，内部循环遍历每个以.scala结尾的file的fileLines(file)
- 其中trimed作为中途变量绑定，用来保存line.trim的值，避免line.trim被重复计算两次

### match表达式

- 例子：
```
val firstArg = if (args.length > 0) args(0) else ""
val friend =
firstArg match {
	case "salt" => println("pepper")
	case "chips" => println("salsa")
	case "eggs" => println("bacon")
	case _ =>println("huh?")
}
println(friend)
```
- 这个例子中，match 表达式跟java的switch相比，有一些很重要的区别。其中一个区别是任何常量、字符串等都可以用作样例。另一个区别是，每个可选项后面没有break，因为scala中break是隐含的，不会出现某个可选项执行完又执行下一个的情况

- match表达式会返回值，上例可以直接将匹配的结果打印出来

- 一般不会用到continue和break

- 例如一段java代码：
```
int i = 0;
boolean foundIt = false;
while (i < args.length){
	if(args[i].startsWith("-")){
		i = i + 1;
		continue;
	}
	if(args[i].endsWith(".scala")){
		foundIt = true;
		break;
	}
	i = i+ 1
}
```

- scala可以写成：
```
var i = 0
var foundIt : Boolean = false
while (i < args.length && !foundIt){
	if(!args(i).startsWith("-")){
		if(args(i).endsWith(".scala")
			foundIt = true
	}
	i = i + 1
}
```

- 或者用递归函数代替循环：
```
def searchFrom(i: Int): Int = {
	if(i >= args.length) -1		//未找到返回-1
	else if(args(i).startsWith("-")) searchFrom(i + 1)	//递归查找下一处
	else if(args(i).endsWith(".scala")) i	//找到了就返回
	else searchFrom(i + 1)
}
val i = searchFrom(0)
```
- 这个递归去掉了循环，每一个continue都换成了一次以i+1为入参的递归调用

## 第八章 函数和闭包
---

### 局部函数

- 我们可以在某个函数内部定义函数，就像局部变量一样，这样局部函数只在包含他的代码块中可见，实现了与类中私有方法相同的效果。
例：
```
def processFile(filename: String, width: Int) = {
	def processLine(line: String) = { //局部函数可以访问包含它们的函数的参数
		if(line.length > width)
			println(filename + ": " + line.trim)
	}
	val source = Source.fromFile(filename) //从文件名创建一个名为source的Source对象
	for (line <- source.getLines()){ //getLines()返回一个每次迭代从文件读取一行并去掉换行符的迭代器
		processLine(filename, width, line)
	}
}
```

### 一等函数*

- 函数字面量被编译成类，并在运行时实例化为函数值。因此，函数字面量和函数值的区别在于，函数字面量存在于，函数字面量存在于源码，而函数值以对象的形式存在于运行时

- 一个函数字面量的简单示例：`(x: Int) => x + 1`

- `=>`表示该函数将左侧的内容转换成右侧的内容，因此这是一个将任何整数x **映射** 成 (x + 1)的函数

- 函数值是对象，所以还可以将他们存放在变量中。同时他们也是函数，也可以用常规的圆括号来调用他们：
```
var increase = (x: Int) => x + 1 //可以将函数字面量赋值给变量
val n = increase(10)  //可以像一般的函数一样调用
increase = (x: Int) => x + 999 //因为increase是var类型，还可以重新赋值
```

- 如果在函数字面量中有多于一条语句，可以将函数体用花括号括起来

- 所有的集合类(List,Set,Array,Map)都提供了foreach方法，**它接受一个函数作为入参，并对它的每个元素调用这个函数**

- 同时，集合类还有个filter方法。这个方法从集合中选出那些满足条件的元素。这个指定条件由函数表示,例如：`(x: Int) => x > 0`这个方法可以被用来过滤。 **这个函数将所有的正整数映射成true，所有其他的整数映射成false**

### 函数字面量的简写形式

- 一种更为简要的方法是省去参数类型声明：`someNumbers.filter((x) => x > 0)`

- 同时圆括号也可以去掉，因为可以省略掉自动推断类型的参数的圆括号：`someNumbers.filter(x => x > 0)`

### 占位符语法

- 为了让函数字面量更加精简，还可以使用下划线作为占位符，用来表示一个或多个参数，只要满足每个参数只在函数字面量中出现一次即可。例如：`_ > 0` 是一个非常短的表示法，表示一个检查某个值是否大于0的函数

- 例子：`someNumber.filter(_ > 0)`

- 可以将下划线当成是表达式中需要被"填"的"空"。函数每次被调用，这个空都会被一个入参给填上

- 如果someNumber被初始化为`List(11,10,9,8)`，那么filter方法首先把 `_ > 0`中的空替换成11，即 11 > 0，然后替换成10，以此类推，直到List末尾


- 有时候当你用下划线作为参数占位时，编译器可能没有足够的信息来推断缺失的参数类型。

- 例如：
```
scala> val f = _ + _
<console> error: missing parameter type for expanded
function ((x$1, x$2) => x$1.$plus(x$2))
...
```

- 这种情况下，可以用冒号来给出类型，就像这样：
```
scala> val f = (_: Int) + (_: Int)
f: (Int, Int) => Int = <function0>
scala> f(5,10)
res0: Int = 15
```

- 注意，`_ + _`将会展开成一个接收两个参数的函数字面量。这就是为什么只有当每个参数在函数字面量中出现不多不少正好一次的时候才能使用这样的精简写法。多个下划线意味着多个参数，而不是对单个参数的重复利用。

### 部分应用的函数

- 下划线还能替换掉整个参数列表，例如：
```
scala>def sum(a:Int, b:Int, c:Int) = a + b + c
sum: (a:Int, b:Int, c:Int)Int
scala>val a = sum _
a:(Int, Int, Int) => Int = <function3>
scala> a(1,2,3)
res0: Int = 6
```

- 后面的a 即是基于sum创建的一个部分应用函数


### 特殊的函数调用形式

#### 重复参数

- scala允许你标示出的参数的最后一个参数可以被重复，这样我们可以对函数传入一个可变长度的参数列表。这样一个重复参数的表示，需要在参数的类型之后加上一个`*`号：
```
scala> def echo(args: String) =
	for (arg <- args) println(arg)
echo: (args: String*)Unit
```
这样echo就可以接受任意多个String类型的参数(可以是0个)

- 但是如果要将一个适合类型的数组以这种重复参数的形式传入的时候，需要写成如下形式：
```
scala> var arr = Array("a","v","gf")
arr:Array[String] = Array(a,v,gf)
scala> echo(arr: _*)
a
v
gf
```
这种表示法告诉编译器将arr的每个元素作为参数传给echo，而不是将所有元素放在一起作为单个实参传入

#### 尾递归

- 例子：
```
def approximate(guess: Double): Double =
	if (isGoodEnough(guess)) guess
	else approximate(improve(guess))
```
在合适的isGoodEnough和improve函数的实现下，这个函数就是一个递归函数。而这个递归调用在最后一步的函数称为尾递归(tail recursive)函数

- scala编译器对尾递归函数有特殊的优化，能够检测到尾递归并将他替换为跳转到函数的最开始，并在跳转之前更新参数的值

- 也就是说，我们完全可以用尾递归的方法来代替循环而不用付出任何额外的开销

- 尾递归不会在每次调用时构建一个新的栈，所有的调用都会在同一个栈中进行

- 如下有个例子：
```
def boom(x: Int): Int =
	if(x == 0) throw new Exception ("boom!")
	else boom(x - 1) + 1
```
这个函数不是一个尾递归的，因为 **它在递归调用之后还执行了一个递增操作**

- 但是scala中尾递归是受限的，更高级形式的尾递归实现十分困难。scala只能对那些直接尾递归的函数做优化


## 第九章 控制抽象
---

### 减少代码重复

- 例子：
```
def filesMatching(query: String,
	matcher: (String, String) => Boolean) = {
	for (file <- filesHere; if matcher(file.getName, query))
		yield file
}
```
- 在这个方法中，if子句用matcher来检查文件名是否满足条件，这个检查具体做什么，取决于具体的matcher。matcher本身是一个函数，因此类型声明中有一个`=>`符号。这个函数接受两个字符串类型的参数(分别是文件名和查询条件)，返回一个布尔值，因此这个参数的类型为`(String, String) => Boolean`

- 下面三个方法分别使用三种不同的参数matcher来实现不同的文件查找功能:
```
def filesEnding(query: String) =
	filesMatching(query, _.endsWith(_))
```
```
def filesContaning(query: String) =
	filesMatching(query, _.contains(_))
```
```
def filesRegex(query: String) =
	filesMatching(query, _.matches(_))
```
- 其中，`_.endsWith(_)`的含义与下面的代码是一样的`(fileName: String, query: String) => fileName.endsWith(query)` 两个下划线按顺序作为传入的两个参数的占位符









<br>
> 最后更新于2018.7.23
