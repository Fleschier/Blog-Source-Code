---
layout:     post
title:      "Java学习笔记——方法"
date:       2018-04-18 16:47:00
categories: Computer Programs
tags: ๑Java
description: "学习记录"
---

> 不适合人类阅读的学习笔记  

## 函数
---

- **Java中的函数没有默认参数，通过函数重载间接实现这个功能。**

- java没有在类外面定义的函数，所以一般都是方法。

### 工具类函数的使用

- 如果要自己写一些可以复用的工具函数，可以新建一个class：
```
class myUtils{
  static void func(...){...}
}
```
- 在这个类中将要用的工具函数用static来修饰，然后将函数的参数弄好之后，就可以在不用新建对象的情况下使用这个方法了。


<br>

> 最后更新于2018.6.6
