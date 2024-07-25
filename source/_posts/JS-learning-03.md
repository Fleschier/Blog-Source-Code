---
layout:     post
title:      "JavaScript 对象部分 "
date:       2019-01-15 11:46:00
categories: Computer Software
tags:   [๑FrontEnd, ๑JS]
description: "学习记录"
---

## window对象
---

- ![](/images/JavaScript/model.png)

- window对象处于对象链的顶端,因为它是Web浏览器中查看所有内容的主要容器. **只要打开浏览器,即使窗口没有加载文档,window对象也在内存的当前模型中定义好了**

- 除了文档所在的窗口内容外,窗口的影响范围还包括窗口的尺寸和包围内容区域的所有"元素".滚动条,工具栏和菜单栏所在的区域叫做窗口的窗框.不是每个浏览器都可以完全控制浏览器主窗口的窗框,但可以便捷地创建其他窗口,随意地设置其大小,指定要显示的窗框元素.

- 每个框架都可以看做一个window对象,因为每个框架都可以存放不同的文档.脚本在其中一个文档上运行时,它把拥有这个文档的框架作为对象层次结构图中的window对象.

### 访问窗口的属性和方法

- ```
window.propertyName
window.methodName([Parameters])
```
在脚本引用指向包含文档的窗口时,window对象有一个同义词self,以上的引用也等价于:
```
self.propertyName
self.methodName([Parameters])
```

### 创建窗口

- 脚本并不创建主浏览器窗口,用户在创建主窗口的时候需要启动浏览器.但是在主窗口打开后,脚本就可以生成大量子窗口.

- 生成新窗口的方法是:`window.open()`.这个方法最多包含三个参数,来定义窗口属性.

- 例子:`var subWindow = window.open("define.html","def","height=200,width=300");`
这个语句将新建的窗口赋值给了变量subWindow.(**这个语句打开了一个具有指定大小的新窗口,这个窗口包含的html文档为define.html,并且与当前页面处于同一个服务器目录下**)

- 如果要关闭此子窗口,则调用`subWindow.close()`即可.而调用`window.close()/self.close()或者close()`就会关闭主窗口.

### window对象的属性和方法

#### window.alert()方法

- 可以直接使用`alert()`来调用这个方法(省略前面的window).这个window方法会生产一个对话框,显示作为参数传送的文本.OK按钮允许用户关闭这个对话框.

#### window.confirm()方法

- 这个方法也是弹出一个对话框,但是有两个按钮(大多数平台上为Ok和Cancel),称为确认对话框.**更重要的是,这个方法有返回值:单击OK返回值为true,单击Cancel返回值为false**. 可以将这个方法的计算值作为if或if..else结构中的条件语句.

- 例子:
```
if (confirm("Are you sure to start over?")){
  location.href = "index.html";
}
```

#### window.prompt()方法

- window对象的最后一种对话框是提示对话框,它显示了预置的信息,并提供一个文本域供用户输入响应.这个对话框有两个按钮:OK和Cancel.

- window.prompt()方法有两个参数,第一个参数是呈现给用户的提示信息;第二个参数是一个字符串,它在文本域中显示为默认的答案.如果不希望显示默认答案就传入一个空字符串(空双引号).

- 用户单击按钮时,这个方法就会返回一个值.不管用户在文本域中输入什么,单击Cancel按钮都会返回null值,单击OK则返回输入的字符串值.这个信息也可以用在判断中,`null值等同于false,空字符串也看做false`.

#### load事件

- window对象会响应几个系统和用户事件,最常见的是页面加载完毕时触发的事件.**这个事件等待图像, Java applet和插件程序的数据文件完全下载到浏览器中**.使用load事件调用函数的优点在于,它确保所有document对象都存在于浏览器的DOM中.

- 可以通过如下方式调用onload方法:
```
window.addEventListener('load', functionName, false);
window.attachEvent('onload', functionName);
//其中functionName是页面下载完成后要运行的函数的名称.可以多次调用addEventListener和attachEvent,把多个函数添加到页面加载完毕要执行的列表中.
```

- 还可以把该事件直接应用于元素:
```
window['onload'] = functionName;
window.onload = functionName;
```
但是这种用法表示,页面加载完毕后,只执行一个函数,并替代已赋予window对象的其他事件处理程序.

## location对象
---

- 这个对象表示载入窗口的URL.它和document对象不同:文档是页面的内容,而位置是页面的URL.

- 脚本大多数只使用该对象的一个属性:`href`,它定义了完整的URL.

- 如果要加载的页面在另一个窗口或框架中,就必须在语句中包含窗口的引用.例如:用脚本打开一个新窗口,并将它的引用赋值给变量newWindow,将页面载入子窗口,如下:
`newWindow.loaction.href = "http://www.example.com"`

## navigator对象
---

- navigator.userAgent属性返回一个包含浏览器和操作系统的诸多细节的字符串.

## document对象
---

### document.getElementById()方法

- 此方法的唯一参数是带引号的字符串,该字符串包含要引用的元素的ID.

- 例子:`var oneTable = document.getElementById('salesResults');`.在赋值语句后,变量就表示对象,可用于获取和设置该对象的属性,或者调用此类对象的方法.

### document.getElementByTagName()方法

- 可以使用getElementByTagName()方法方便地收集一组共享同一个标记名称的页面元素.例如,要获得页面上所有的图像:`var aImages = document.getElementByTagName('img');`

- 然后可以通过数组的方法来获取数组的长度:`aImages.length`,然后每个对象就可以使用数组的偏移量来访问.

### document.forms[]属性

- 比较下面两个表达式:
```
var aForms = document.forms;
var aForms = document.getElementByTagName('form');
```
**一个重要的区别是,document.forms集合允许按名称直接引用某个表单,而不仅仅是按照数组的偏移量来访问.**

- 因为有些时候按照下标号引用表单未必可行.动态网页可能根据上下文包含数量可变的表单,所以表单在页面上的位置可能随上下文而变化.

- 支持脚本编程的浏览器允许通过表单名或ID(即分配给`<form>标记的name或者id属性`)更直接地引用表单:
```
<form id='formId' name='fromName' ...>

//第一种方法是使用getElementById方法:
document.getElementById("formId")

//第二种方法是使用数组语法,将表单名称或者ID作为数组的字符串下标:
document.forms["formId"]
document.forms["formName"]

//第三种按名称引用form对象的简短方式是把表单的名称附加为document对象的属性:
document.fornName
```

### document.images[]属性

- 文档利用特殊的数组属性来跟踪表单,同样,document对象也通过`<img>`标记保存插入文档的图像集合(数组).通过document.images数组引用的图像可以用img元素名称中的数字或字符串下标来得到.

### document.createElement()和document.createTextNode()方法

- 在HTML文档中添加新元素至少需要两个步骤:
1. 为文档创建新元素.
2. 在页面的树形结构中,将其插入到需要的位置.

- document.createElement()方法可以在浏览器的内存中创建一个全新的元素对象.指定要创建的元素时,应将元素的标记名作为该方法的字符串参数:
`var newEle, = document.createElement("p");`

- 还可以给元素添加一些属性值,为此应在元素成为文档的一部分之前,向新建对象赋值:`newElem.setAttribute("class","intro");`

- 可将这个元素插入文档中的任何位置,例如末尾:
`document.body.appendChild(newElem);`

### document.write()方法

- document.write()方法是给文档写入内容的另一种方式.他的优点是可以临时应急,缺点如下:
1. 只有页面第一次加载到浏览器中时,document.write()才能给一个网页添加内容.以后调用该方法都会替代整个页面.
2. document.write()会将旧文本块插入文档,编写出草率的程序和错误的标记,将标记与脚本内容混合在一起,不利于开发的分层.
3. document.write()不能用于XHTML,XHTML这种文档类型不允许第一次解析期间修改其内容.

> 注:XHTML---可扩展超文本标记语言（英语：eXtensible HyperText Markup Language，XHTML），是一种标记语言，表现方式与超文本标记语言（HTML）类似，不过语法上更加严格。从继承关系上讲，HTML是一种基于标准通用标记语言（SGML）的应用，是一种非常灵活的置标语言，而XHTML则基于可扩展标记语言（XML），XML是SGML的一个子集。XHTML 1.0在2000年1月26日成为W3C的推荐标准。

## 表单和表单元素
---

### form对象

- 表单以及其中的输入控件是DOM对象,其独特的属性是文档中其他对象所没有的.例如,表单对象的action属性告诉浏览器,在提价表单时,将输入的值发送到什么地方.select控件(下拉列表)的selectedIndex属性指出用户选择了哪个选项.

#### 访问表单属性

-  在创建表单时,可以使用HTML页面中的标准标记,也可以使用JavaScript中的DOM方法.无论采用哪种方法,都可以设置name,target,action,method和enctype特性.这些都是form对象的属性.

- 用法的例子:
```
var sURL = document.getElementById('formName').action;
document.forms[0].action = "http://www.example.com/cgi/login.pl";
```

#### from.elements[]属性

- elements[]属性是表单中所有输入控件的集合.这个数组中各项的顺序根据HTML标记在源代码中的顺序而定.使用ID直接引用单个元素通常更有效,但有时候需要遍历所有元素时会需要这样访问.

- 下面的代码段查看表单中所有的控件元素,并将文本域的内容设置为空字符串.
```
var oForm = document.getElementById('registration-form');
  if(!oForm) return false;
for(var i = 0; i < oForm.elements.length; i++){
  if(oForm.elements[i].type == "text"){
    oForm.elements[i].values = "";
  }
}
```

### 将表单控件作为对象

- 在所有浏览器的DOM中,嵌套在`<form>`标记中的HTML元素有三种是脚本对象.多数对象都在页面源代码的`<input>`标记中,只有赋给`<input>`标记的type特性的值能确定元素是文本框,密码输入域,隐藏域,按钮,复选框还是单选框.其他两种表单控件textarea和select有各自的标记.

- 要将某个表单控件作为对象进行引用,可以使用其id或tagName直接引用,或者使用DOM level 0语法,将引用构造为一个以document开头,后跟form和控件的层次结构.
```
document.getElementById(controlName)
或者
document.formName.controlName
```

- 例如有个简单的表单:
```
<form id="searchForm" action="cgi-bin/search.pl">
  <p>
    <input type="text" id="entry" name="entry">
    <input type="submit" id="sender" name="sender" value="Search">
  </p>
</form>
```CPU
对于文本输入控件,以下引用实例都是有效的:
```
document.getElementById("entry")
document.searchForm.entry
document.searchForm.elements[0]qitak
document.forms["searchForm"].elements["entry"]
document.forms["searchForm"].entry
```
