---
layout:     post
title:      "C++学习笔记——数值类型,char和string的相互转化问题"
date:       2018-10-08 16:10:00
categories: Computer Programes
tags: ๑C++
---

## C++提供了一些功能强大的函数来高效地完成这些转化
---

### string转char

1. 使用`c_str()`方法

- 示例：
```
string s = "abcd";
char p[10];
p = (char*)s.c_str();
```

- 上面的强制类型转换在 **不修改字符串内容的情况下** 是可以省略的。因为`c_str()`方法的返回值类型为`const char*`，返回的是一个不可修改的指向该字符串的指针。

2. 使用`data()`方法

-  `data()`方法与`c_str()`方法用法几乎一致，这里不再赀述。

3. 使用`copy()`方法

- `copy()`方法与上面两种有所不同，它是拷贝函数，这只是他的一种用法。

- 实例:
```
string s = "abcd";
char p[5];
s.copy(p, 4, 0);  //4代表拷贝四个字符，0代表写入的位置
*(p + 4) = '\0';  //拷贝的字符串需要手动加上结束标记
```

### char转string

- 对于已经存在的`char*`，可以直接赋值给string类型的数据

### 数值类型转string

- C++库有直接的转换函数`to_string()`

- `to_string()`函数有多个重载函数，支持目前所有的数据类型转换为string类型。

- 需要引入头文件`#include<string>`

-
```
#include<string>
...
int a = 10;
string s = to_string(a);
...
```

### 数值类型转char

- 这里就需要用到强大的转换函数`itoa()`。

- 还有`ltoa`,`ultoa`等函数可以将 **任意类型(整型、长整型、浮点型等)的数字** 转换为字符串。

- 需要引入头文件`stdlib.h`

- 示例：
```
#include<iostream>
#include<stdlib.h>
using namespace std;
int main(){
  int i = 100;
  char p[10];
  itoa(i, p, 10);   //说明：第一个参数为待转换的数字，第二个参数为待存储数值的char数组指针，第三个参数为待转换数字的进制，这里为十进制。
  cout << p << endl;
}
```
> itoa并不是一个标准的C函数，它是Windows特有的，如果要写跨平台的程序，请用sprintf。

### 字符串转数值类型

- 函数原型为 `int atoi (const char * str);`    //参数为指针类型，如果为string需要在变量名前加取址符。

- `atoi()` 函数会扫描参数`str`字符串，跳过前面的空白字符（例如空格，tab缩进等，可以通过`isspace()`函数来检测），直到遇上数字或正负符号才开始做转换，而再遇到非数字或字符串结束时(`\0`)才结束转换，并将结果返回。

- ANSI C 规范定义了 `stof()、atoi()、atol()、strtod()、strtol()、strtoul()`共6个可以将字符串转换为数字的函数。另外在 C99 / C++11 规范中又新增了5个函数，分别是 `atoll()、strtof()、strtold()、strtoll()、strtoull()`。这里根据名称就可以对应看出各个函数的转换目标。
