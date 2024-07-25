---
layout:     post
title:      "JavaScript 入门"
date:       2019-01-12 17:46:00
categories: Computer Software
tags:   [๑FrontEnd, ๑JS]
description: "学习记录"
---

## 引例
---

```
//tell the browser to run this script when the page has finished loading
window.onload = insertDateTime;

//insert the data & time
function insertDateTime(){
  //ensure a DOM-aware user agent
  if(!document.getElementById) return;
  if(!document.createTextNode) return;

  //create a date-time object
  var oNow = new Data();

  //get the current date & time as a string
  var sDateTime = oNow.toLocaleString();

  //point to the target element where we want to insert the date & time
  var oTarget = document.getElementById('output');
  //make sure the target is found
  if(!oTarget) return;

  //delete everything inside the target
  while(oTarget.firstChild){
    oTarget.removeChild(oTarget.firstChild);
  }

  //use the date-time string to create a new text node for the page
  var oNewText = document.createTextNode(sDateTime);

  //insert the mew text into the span
  oTarget.appendChild(oNewText);
}
```

### 解析

#### 触发事件

- 脚本要把日期和事件插入到页面的段落中,但浏览器在读取和运行JavaScript代码之前,并没有读取HTML体.在JavaScript开始运行时,要插入新内容的段落甚至在浏览器的内存中不存在.

- 解决办法就是告诉JavaScript,在文档完全读入内存之前,不要执行插入操作.为此使用了`onload`事件.页面的元素(*在DOM中称为对象*)可以感知很多事件,例如 *鼠标单击或按下一个键.* 文档加载到浏览器中后,就会触发window对象的`onload`事件.

- `window.onload = insertDateTime;`告诉JavaScript,文档加载完毕后调用`insertDateTime()`函数.

#### 确保一个安全的环境

- ```
//ensure a DOM-aware user agent
if(!document.getElementById) return;
if(!document.createTextNode) return;
```
这里调用的`getElementById()`和`createTextNode()`是两个某些旧的JavaScript解释器不能理解的DOM方法.感叹号`!`表示"not",`return`告诉JavaScript停止运行当前的函数. 如果不包含这些保护措施,某些老式的浏览器或其JavaScript解释器就会在运行其后代码的时候崩溃.

#### 生成日期和时间

- 要插入这个文档中的文本是当前的日期和时间.JavaScript很容易完成这个插入操作:创建一个Date对象,并使用它的一个方法生成字符串:
```
//create a date-time object
var oNow = new Date()
//get the current date & time as a string
var sDateTime = oNow.toLocaleString();
```
这些代码把oNow变量设置为一个新的Date对象.之后使用其toLocaleString()方法输出一个文本字符串,它包含:`Thrusday, August 20, 2009 4:16:05 PM`

#### 确定目标

- 下一步就是把日期和事件插入文档中需要的位置.执行了以下操作:
1. 指向目标`span`元素
2. 删除该文本中已有的文本
3. 在元素中插入新的文本

- 为了指向`output span`,使用ID的方式来定位:
`var oTarget = document.getElementById('output');`
该语句通过ID(ouput)lai定位目标元素,并把该对象的`引用`存储在oTarget变量中.

- HTML规范指出,每个元素的ID在当前页面必须是唯一的,即使不小心在页面上使用了相同的ID,`getElementById()`方法也仅返回第一个ID实例.所以,这个方法仅定位一个元素.(本例中就是span元素)

- 如果`getElementById()`没有找到对应的ID,则将返回空值.为了避免由于疏忽导致的这类错误,采用`if(!oTarget) return;`这个测试语句.

- 也可以将这个错误变成警告提示:`if(!oTarget) return alert("Warning: output element not found!");`

#### 删除原来的内容

- 我们要删除span的文本,再插入新内容.在表示页面内容的DOM中,span是其所有子元素的父元素.span现在只有一个子元素:单词"now".

- 为了删除span的内容,执行一个简单的循环.只要还有要删除的元素,该循环就一次删除一个子元素:
```
//delete everything inside the target
while(oTarget.firstChild){
  oTarget.removeChild(oTarget.firstChild);
}
```
在本例中这个循环只会执行一次.

#### 插入日期和时间

- 最后在DOM中创建一个包含所有所需文本的新节点,并插入span:
```
//use the date-time string to create a new text node for the page
var oNewText = document.createTextNode(sDateTime);

//insert the new text into the span
oTarget.appendChild(oNewText);
```
sDateTime是从Date对象中生成的字符串.

- 这里调用document对象关联的一个方法,该方法会创建一个新的文本节点,并把日期和事件字符串作为其值.此时该文本结点还不是可见文档内容的一部分,使用目标元素的appendChild()方法就可以插入它.
