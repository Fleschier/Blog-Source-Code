---
layout:     post
title:      "Python 面向对象编程"
date:       2018-11-25 12:47:00
categories: Computer Programs
tags: ๑Python
description: "学习记录"
---

## 模块与包
---

- 简单举例就是:
```
mypackage
├─ __init__.py
├─ abcd.py
└─ efgh.py
```

- 注意每个包下需要一个`__init__.py`文件

- 如果另一个py文件需要引用abcd.py,则写为`mypackage.abcd`

## python类
---
- 类不需要显式地申明类成员变量(与C++和Java不同)

- 类中所有的方法的第一个参数都是`self`, self代表类的实例而非类,并且在调用类方法时,self参数不必传入.

- `__init__()`方法是一种特殊的方法，被称为类的构造函数或初始化方法，当创建了这个类的实例时就会调用该方法

### python类内置属性

- `__dict__` : 类的属性（包含一个字典，由类的数据属性组成）

- `__doc__` :类的文档字符串

- `__name__`: 类名

- `__module__`: 类定义所在的模块（类的全名是'__main__.className'，如果类位于一个导入模块mymod中，那么className.__module__ 等于 mymod）

- `__bases__` : 类的所有父类构成元素（包含了一个由所有父类组成的元组）

#### 判断一个对象是否是一个类的实例

- 目前我所知的只有两个方法可行(python3):
```
a = myclass()
b = myclass()
type(a) == type(b) #a和b都是类实例
isinstance(a, myclass.__bases__)    #虽然__bases__返回的是父类元组,但是却能成功判断
```
