---
layout:     post
title:      "JavaScript 基础 "
date:       2019-01-13 16:46:00
categories: Computer Software
tags:   [๑FrontEnd, ๑JS]
---

## 浏览器窗口中的DOM
---

- 所有现代浏览器的基本对象模型:
![](/images/JavaScript/model.png)

1. window对象: 在层次结构顶部的是window对象.这个对象代表显示HTML文档的浏览器窗口的内容区域.在多框架环境下,每个框架也是一个窗口.所有的文档动作都是在窗口内发生的,所以窗口是对象层次结构中最外部的元素,它包含文档.

2. navigator对象: 脚本从这个对象开始访问浏览器程序,主要是读取浏览器的品牌和版本.此对象为只读,以禁止流氓脚本对浏览器的不当操作.但如后面所述,不能依赖navigator对象获得当前浏览器的实际品牌,型号和版本.

3. screen对象: 这是另一个只读对象,它给脚本提供了运行浏览器的物理环境信息.例如,此对象显示了监视器的高度和宽度(像素值).

4. history对象: 尽管浏览器保留了最近浏览历史的内部细节(如单击后退显示的内容列表),但是脚本却无权访问这些细节.这一对象可以帮助脚本模拟后退或前进按钮的单击.

5. document对象: 每个载入窗口的HTML文档都会变成一个document对象.document对象包含脚本中的内容.除了每个HTML文档中都有的html,head和body元素对象外,文档中元素对象层次的具体标记和结构取决于文档的内容.

## 文档的载入
---

### 简单文档

- 空文档的对象映射:
![](/images/JavaScript/document.png)
```
<!DOCTYPE html>
<html>
 <head>
  <meta ...>
  <title></title>
 </head>
 <body>
  ...
 </body>
</html>
```

### 添加段落

- 添加段落标签, 在段落元素的开始和结束标记之间插入段落文本.在标记间插入的连续文本是DOM中的一种特殊的对象,称为文本结点.文本节点总是有一个容器元素,也就是说,文本结点是其父元素p的子元素.

![](/images/JavaScript/document1.png)

```
<!DOCTYPE html>
<html>
 <head>
  <meta ...>
  <title></title>
 </head>
 <body>
  <p>This is the one and only Paragraph</p>         //添加了段落标签和段落内容
 </body>
</html>
```

### 生成新元素

- 将部分段落文本包含在一个<em>标签中,表示要强调这些文本.这个插入操作对p元素对象的层次结构有很大的影响.**p元素从只有一个(文本结点)子元素变成有三个子元素:两个文本节点,和一个它们之间的元素**. 在W3C DOM中, **文本结点不能有任何子元素**,因此不能包含元素对象.em元素中的文本结点不再是p元素的子元素,而是em元素的子元素.

![](/images/JavaScript/document2.png)

```
<!DOCTYPE html>
<html>
 <head>
  <meta ...>
  <title></title>
 </head>
 <body>
  <p>This is the one and only Paragraph</p>         //添加了段落标签和段落内容
 </body>
</html>
```

## 对象
---

### 获取对象的属性

- 例如,下面的HTML标记定义了一个input元素对象,它指定了四个属性和属性值:
```
<input type="button" id="clicker" name="clicker" value="...">
```
不必为每个对象设置每个属性,多数属性都有默认值.假如HTML或脚本没有特殊要求,他们就自动设置为默认值.

- 为了访问对象的属性,需要使用和前面对象相同的圆点定位方式.属性是从属于对象的资源,所以属性的引用就是对象引用后加属性名.

- 对于刚才的例子,属性的引用如下:
```
document.getElementById("clicker").name
document.getElementById("clicker").value
...
```
> 如果JavaScript尝试引用不存在的元素的属性,就会失败或终止.因此引用之前最好先测试一下.

- 测试引用是否安全:
```
val oClicker = document.getElementById("clikcker");
  if(!oClicker) return;
var sName = oClicker.name;
```

- 在引用的过程中我们省略`window`部分(*完整为window.document.XXX*).因为一个窗口只能包含一个文档,所以文档中对象的引用可以省略window部分,但是不能省略document对象.

## 方法
---

- 方法的调用与大多数语言一样,需要在方法名后加一对圆括号.

- 参数之间以逗号间隔

## 事件
---

- 事件是文档执行中的动作,通常是用户活动的结果.

- 文档中的每个DOM对象几乎都接收某种类型的事件.我们只需要编写代码,告诉元素对象,只要接收到某种事件,就执行一个动作.这个动作就是执行其他的一些JavaScript代码.

- 具有事件处理能力的简单按钮:
```
//HTML: 1.html
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="content-type" content="text/html;charset=utf-8"
    <title>A Simple Button with an Event Handler</title>
    <script type="text/javascript" src="jab.js"></script>
  </head>
  <body>
    <form action="">
      <div>
        <button id="clicker">Click here</button>
      </div>
    </form>
  </body>
</html>
```
```
//JAVASCRIPT:jsb.js
//tell the browser to run this script when the page has finished loading
window.onload = applyBehavior;

//apply behavior to the button
function applyBehavior(){
  //ensure a DOM-aware user agent
  if(document.getElementById){
    //point to the button
    var oButton = document.getElementById('clicker');

    //if it exists, apply behavior
    if(oButton){
      oButton.onclick = behave;
    }
  }
}

//what to do when the button is clicked
function behave(evt){
  alert('Ouch! ');
}
```

- 事件的名称一般为事件的类型(例如click)以及前缀on构成,表示一接收到XXX事件就XXX.

## 把脚本链接到文档上
---

1. 放在外部文件中:`<script type="text/javascript" src="[/..../]example.js"></script>`

2. 内嵌在html中:
```
<script type="text/javascript">
  JavaScript code here
</script>
```

### script标记的位置

- 大多数情况下script标记放在`<head>`标签中,有时候会放在`<body>`标签.

- 放在`<head>`中的标记一般会影响页面中的非内容设置---所谓的html指令元素,例如`<meta>`标记和文档题目,这里也适合放置响应页面载入或用户动作的脚本.

- 如果需要在页面载入时运行脚本,以便生成页面内容,则脚本应放在文档的`<body>`部分

### 注释

- 单行注释用`//`,多行注释用`/**/`

## 脚本语句的执行时间
---

- 根据脚本要完成的功能,脚本运行的时间有四种选择:

1. 文档载入时
2. 文档载入后
3. 响应用户动作时
4. 其他脚本语句调用时

- 决定性因素是脚本语句在文档中的位置.

- 除了第一个,其他三种统称为延时脚本

### 页面载入后执行

- 假设定义了函数`function done(){alert("....")}`,则如果想要在页面加载完成是调用它,可以用`window.onload = done;`来实现在页面加载完成时调用`done`函数. **注意此语句右侧只有函数名,没有圆括号.**

## JavaScript值(数据)类型
---

|类型|示例|说明|
|---|---|---|
|String|"Test"|引号内的一系列字符|
|Number|4.5|不在引号内的数字|
|Boolean|false|逻辑真或假|
|Null|null|不包含任何内容,但仍然是一个值|
|Object||通过属性和方法定义的软件对象(数组也是对象)|
|Function||函数定义|

- 假如用户在表单的文本的输入域中输入数字,浏览器就把该数字存储为字符串类型.假如脚本要对这个数字执行算数操作,就需要将字符串转化为数字再进行操作.

## 变量
---

- 创建变量:`var valueName;`  `var`关键字用于声明和初始化变量,文档中任何变量都只需要使用一次var关键字.

- 变量赋值:`valueName = 45;`

- **JavaScript变量可以存储任何类型的值**.在声明变量的时候,不必定义变量包含的值的类型.

### 类型转换

- 两个数值相加:`3 + 3`,结果为6没有问题.

- 但如果其中一个数字是字符串,JavaScript就会将另一个值转换为字符串,**将这个加号操作从算数加变成字符串连接**:`3 + "3"`,结果为`"33"`. `3 + 3 + "3"`,结果为`"63"`.

#### 将字符串转化为数值

- JavaScript提供了两个内置函数:`parseInt()`和`parseFloat()`

- ```
parseInt("43")    //结果为42  
parseInt("43.33") //结果为43,这里做截断处理
```

- ```
parseFloat("43")  //结果为43
parseFloat("43.33")  //结果为43.33
```

#### 将数字转化为字符串

- 利用JavaScript的特性:`""+2500`,结果即为`"2500"`

## 控制结构
---

- if else与C++等用法一致

- for循环(i用var声明,其余与C++一致):
```
for(var i = startValue; i <= MaxValue; i++){
  ...
}
```

## 函数
---

- 函数的正式语法结构:
```
functoin functionName([Parameter1]...[,ParameterN]){
  statement[s]
}
```

### 局部变量和全局变量

- 在函数外声明的变量为全局变量,在函数体中定义的变量称为局部变量.

- 局部变量的作用域只局限于函数内部.

- 全局变量的作用域是 **当前载入浏览器窗口或框架的文档**.因此初始全局变量后,页面中所有的脚本语句可通过全局变量名直接访问其值.但是,一旦卸载页面,在页面中定义的所有全局变量都会从内存中清除.假如某个值需要在页面卸载后继续使用,则需要使用其他技术来保存它,比如将它存储为框架集文档中的全局变量,或将它存储在cookie中.

- 如果用`var`关键字在函数体中初始化了一个与全局变量同名的局部变量,则在函数体中该局部变量比全局变量优先级要高.

## 数组
---

- 创建:`var Arr = new Array(100);`

- 访问:`Array[0];`

### 数组中的document对象

- 例如,如果页面包含两个`<form>`标记对时,在文档中就会出现两组`<form>`标记.浏览器为文档使用一个from对象数组,对这些表单的引用如下:
```
document.forms[0]
document.forms[1]
```

- 也可以使用DOM方法`getElementByTagName()`访问这个数组:
```
var aForms = document.getElementByTagName('form');
aForms[0]
aForms[1]
```

- document对象的下标是由对象的载入顺序决定的,form对象的顺序由文档中`<form>`标记出现的顺序确定.
