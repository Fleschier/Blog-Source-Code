---
layout:     post
title:      "前端学习——HTML"
date:       2018-06-17 11:46:00
categories: FrontEnd
tags:   [๑FrontEnd, ๑Html]
---

> 不适合人类阅读的学习笔记

## HTML基础
---

- 学习web前端开发基础技术需要掌握：HTML、CSS、JavaScript语言。(网页三件套大礼包～)

### 概念解析

-  HTML是网页内容的载体。内容就是网页制作者放在页面上想要让用户浏览的信息，可以包含文字、图片、视频等。

-  CSS样式是表现。就像网页的外衣。比如，标题字体、颜色变化，或为标题加入背景图片、边框等。所有这些用来改变内容外观的东西称之为表现。

- JavaScript是用来实现网页上的特效效果。如：鼠标滑过弹出下拉菜单。或鼠标滑过表格的背景颜色改变。还有焦点新闻（新闻图片）的轮换。可以这么理解，有动画的，有交互的一般都是用JavaScript来实现的。

### 一个html网页的基本结构

```
<html>
<head>
...
</head>
<body>
<h1>
...
</h1>
<p>
...
</p>
<img src="...">
...
</body>
</html>
```
#### 标签语法

- 标签由英文尖括号`<`和`>`括起来，如`<html>`就是一个标签。

- 每组标签都是一一对应的，且后一个标签以 `/`(正斜杠)开头，标志着这一个部分的结束。

- 标签与标签之间是可以嵌套的，但先后顺序必须保持一致，如：<div>里嵌套<p>，那么</p>必须放在</div>的前面。`<div> <p> ... </p> </div>`

- HTML标签不区分大小写，`<h1>`和`<H1>`是一样的，但建议小写，因为大部分程序员都以小写为准

### 代码注释

- html代码注释的语法如： `<!--注释文字-->`

## 标签详解

- `<html></html>`称为根标签，所有的网页标签都在`<html></html>`中。

- `<head>` 标签用于定义文档的头部，它是所有头部元素的容器。头部元素有`<title>、<script>、 <style>、<link>、 <meta>`等标签

- 在`<body>`和`</body>`标签之间的内容是网页的主要内容，如`<h1>、<p>、<a>、<img>`等网页内容标签，在这里的标签中的内容会在浏览器中显示出来。

- 其中，`<h1>`就是标题标签

- `<p>`就是段落标签，段落内容就写在`<p>`与`<\p>`之间

- `<img src= "..">`表示图片，src中填写图片保存的路径

### `<head>`标签

- 文档的头部描述了文档的各种属性和信息，包括文档的标题等。绝大多数文档头部包含的数据都不会真正作为内容显示给读者。

- 下面这些标签可以用在`<head>部分`：

```
<head>
    <title>...</title>
    <meta>
    <link>
    <style>...</style>
    <script>...</script>
</head>
```

- `<title>`标签：在`<title>`和`</title>`标签之间的文字内容是网页的标题信息，**它会出现在浏览器的标题栏中**。网页的title标签用于告诉用户和搜索引擎这个网页的主要内容是什么，搜索引擎可以通过网页标题，迅速的判断出网页的主题。每个网页的内容都是不同的，每个网页都应该有一个独一无二的title。

### `<p>`标签

- 每一对`<p></p>`标签表示一个段落，所以网页上每一段文字都要放在一对单独的`<p></p>`中。

### `<hx>`标签

- 上面的`<p>`标签是用来表示文章的段落的，那么文章的标题可以用`<hx>`来表示，**其中`x`为1-6的整数**，数字越小，代表越重要，字体也就越大。(这一点与markdown的用#号个数来表示几级标题是一致的)

### 文本修饰：`<strong>`,`<em>`和`<span>`标签

- `<em>`表示强调，`<strong>`表示更强烈的强调。并且在浏览器中`<em>`默认用 *斜体* 表示，`<strong>` 用 **粗体** 表示。

- `<span>`标签是没有语义的，它的作用就是为了设置单独的样式用的。

- 例子：

```
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>了不起的盖茨比</title>
<style>
span{
    color:blue;
}
</style>
</head>
<body>
    <p>
    1922年的春天，一个想要成名名叫尼克•卡拉威（托比•马奎尔Tobey Maguire 饰）的作家，离开了美国中西部，来到了纽约。那是一个道德感渐失，爵士乐流行，走私为王，股票飞涨的时代。为了追寻他的<span>美国梦</span>，他搬入纽约附近一海湾居住。
    </p>
    <p>
    菲茨杰拉德，二十世纪美国文学巨擘之一，兼具作家和编剧双重身份。他以诗人的敏感和戏剧家的想象为"爵士乐时代"吟唱华丽挽歌，其诗人和梦想家的气质亦为那个奢靡年代的不二注解。
    </p>
</body>
</html>
```
其中第一段中的“美国梦”被`<span>`标签标记，在`<style>`标签中，我们定义了`<span>`标签修饰的文本的格式为蓝色。

### `<q>标签`

- `<q></q>`标签表示引用，注意要引用的文本不用加双引号，浏览器会对q标签自动添加双引号。

- `<q></q>`适合一句话的引用。

### `<blockquote>`标签

- 相对于`<q></q>`，`<blockquote>...</blockquote>`适合用来引用一段长文字。

### 换行与空格

- 在 html 中是**忽略回车和空格**的，你输入的再多回车和空格也是显示不出来的

- 换行标签语法：

```
xhtml1.0写法： <br />
html4.01写法： <br>
```
现在一般用html4的写法

-  与以前我们学过的标签不一样，`<br />`标签是一个 **空标签** 。没有HTML内容的标签就是空标签，**空标签只需要写一个开始标签**，这样的标签有`<br />`、`<hr />`和`<img />`。

- 空格表示方法：`&nbsp;`。

### 水平分割线

- 在信息展示时，有时会需要加一些用于分隔的横线，这样会使文章看起来整齐些。效果如下
<hr>

- 语法：

```
html4.01版本 <hr>
xhtml1.0版本 <hr />
```
现在一般用html4的写法

- `<hr />`标签和`<br />`标签一样也是一个空标签，所以只有一个开始标签，没有结束标签。

- `<hr />`标签的在浏览器中的默认样式线条比较粗，颜色为灰色，可能有些人觉得这种样式不美观，没有关系，这些外在样式在我们以后学习了css样式表之后，都可以对其修改。

### `<address>`标签：为网页加入地址信息

- `<address></address>`标签默认为斜体。这个也可以通过CSS修改。

### `<code>`和`<pre>`标签

- 在网页上`<code></code>`标签用来标注一行代码。

- 如果是多行代码，可以使用`<pre>`标签。语法：`<pre>语言代码段</pre>`

- `<pre>` 标签的主要作用:预格式化的文本。被包围在 pre 元素中的文本通常会保留空格和换行符。

- 注意：`<pre>` 标签不只是为显示计算机的源代码时用的，在你需要在网页中预显示格式时都可以使用它，只是`<pre>`标签的一个常见应用就是用来展示计算机的源代码。

### `ul-li`标签

- 实例：

```
<ul>
  <li>精彩少年</li>
  <li>美丽突然出现</li>
  <li>触动心灵的旋律</li>
</ul>
```

- `ul-li`在网页中显示的默认样式一般为：每项`li`前都自带一个圆点：
![](/images/HTML/ul-li.png)

### `ol-li`标签

- 与`ul-li`标签类似，只是前面的圆点变成了从1开始的序号

### `<div>`标签

- 在网页制作过程过中，可以把一些独立的逻辑部分划分出来，放在一个`<div>`标签中，这个`<div>`标签的作用就相当于一个容器。

- 逻辑部分是页面上相互关联的一组元素。如网页中的独立的栏目版块，就是一个典型的逻辑部分。

- 一般一个网页都要用很多个`<div></div>`来划分成不同的逻辑部分。

### `<div>`标签的命名

- 为了使逻辑更加清晰，我们可以为这一个独立的逻辑部分设置一个名称，用`id`属性来为`<div>`提供唯一的名称，这个就像我们每个人都有一个身份证号，这个身份证号是唯一标识我们的身份的，也是必须唯一的。

- 语法：`<div  id="版块名称">...</div>`(只需要在开始的部分添加，结尾不变)

### `<table>`标签

- 创建表格的四个元素：table、tbody、tr、th、td

- 整个表格以`<table>`标记开始、`</table>`标记结束。

- 如果不加`<thead><tbody><tfooter>` , table表格加载完后才显示。加上这些表格结构， `tbody`包含行的内容下载完优先显示，不必等待表格结束后在显示，同时如果表格很长，用`tbody`分段，可以一部分一部分地显示。（通俗理解table 可以按结构一块块的显示，不在等整个表格加载完后显示。）

- `<tr>...</tr>`：表格的一行，所以有几对tr 表格就有几行。

- `<td>...</td>`：表格的一个单元格，一行中包含几对`<td>...</td>`，说明一行中就有几列。

- `<th>…</th>`：表格的头部的一个单元格，表格表头。

- 表格中列的个数，取决于一行中数据单元格的个数。

- table表格在没有添加css样式之前，在浏览器中显示是没有表格线的

### `<a>`标签

- `<a>`标签实现了超链接。

- 语法：`<a  href="http://...(网址)"  title="鼠标滑过显示的文本">链接显示的文本</a>`

- 设置链接在新建窗口中打开：`<a href="目标网址" target="_blank">链接显示的文本</a>`

### `<img>`标签

- 语法：`<img src="图片地址" [alt="下载失败时的替换文本"](一般可以不写) title = "提示文本">`

- src：标识图像的位置

- alt：指定图像的描述性文本，当图像不可见时（下载不成功时），可看到该属性指定的文本

- title：提供在图像可见时对图像的描述(鼠标滑过图片时显示的文本)

### 表单标签

- 表单是可以把浏览者输入的数据传送到服务器端，这样服务器端程序就可以处理表单传过来的数据。

- 语法：`<form   method="传送方式"   action="服务器文件">`

- <form> ：<form>标签是成对出现的，以<form>开始，以</form>结束。

- action ：浏览者输入的数据被传送到的地方,比如一个PHP页面(save.php)。

- method ： 数据传送的方式（get/post）。

- 例：

```
<form    method="post"   action="save.php">
        <label for="username">用户名:</label>
        <input type="text" name="username" />
        <label for="pass">密码:</label>
        <input type="password" name="pass" />
</form>
```

- 所有表单控件（文本框、文本域、按钮、单选框、复选框等）都必须放在 <form></form> 标签之间，否则用户的数据可能提交不上。

- method : post/get 的区别这一部分内容属于后端程序员考虑的问题。

### 文本输入框、密码输入框

- 文本输入框可以转化为密码输入框。

- 语法：

```
<form>
   <input type="text/password" name="名称" value="文本" />
</form>
```

- type：当type="text"时，输入框为文本输入框; 当type="password"时, 输入框为密码输入框。

- name：为文本框命名，以备后台程序ASP 、PHP使用。

- value：为文本输入框设置默认值。(一般起到提示作用)

### 文本域

- 语法：`<textarea  rows="行数" cols="列数">文本</textarea>`

- cols ：多行输入域的列数。

- rows ：多行输入域的行数。

- 注意这两个属性可用css样式的width和height来代替：col用width、row用height来代替。

- 在`<textarea></textarea>`标签之间可以输入默认值。

## Html5新元素一览
---

- [Html5新元素](http://www.runoob.com/html/html5-new-element.html)


<br>
> 最后更新于2018.6.17