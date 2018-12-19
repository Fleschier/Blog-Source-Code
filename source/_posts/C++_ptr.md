---
layout:     post
title:      "C++学习笔记——指针"
date:       2018-12-19 14:10:00
categories: Computer Programs
tags: ๑C++
---

## 典型错误
---

- ```
long * fellow;
*fellow = 23333;
```

- fellow的确是一个指针,但是它指向的地址还没确定,那么23333会被存放到哪里呢?我们也不知道,这就会引发一个编译错误.

- **指针使用的金科玉律: 一定要在对指针解除引用运算符(*)之前,将指针初始化为一个确定的,适当的地址.**

> --------from C++ Primer Plus

## 指针和数字
---

- 例子:
```
int * pt;
pt = 0xB8000000;
```
在这里左边是一个int类型的指针,而右边是一个 **整数**, 0xB8000000是老式计算机系统中组合段的偏移地址,但是在这条语句中编译器并不知道这是个地址,因此C++编译器会报错.

- 正确的写法应该是:
```
int * pt;
pt = (int *) 0xB8000000;    
```

## 使用new来分配内存
---

- 在C语言中,只能用库函数malloc()来分配内存,C++也支持这样做,但是有更好的选择---new运算符.

- new运算符同时要配合delete来使用

- 例子:
```
int * pt = new int;
...
delete pt;
```
这将释放pt指向的内存块,但不会删除指针pt本身,它的值也没有改变.

- 一点要配对地使用new 和 delete,否则会发生内存泄漏(memory leak).

- 不要尝试释放已经释放的内存块,这会导致很严重的不确定性.

- 不能使用delete来释放声明变量所获得的内存:(**也就是delete只能用来删除new分配的内存**)
```
int * ps = new int;   //ok
delete ps;      //ok
delte ps;     //not ok now
int jugs = 5;       //ok
int * pi = &jugs;   //ok
delete pi;      //not allowed now, memory not allocated by 'new'
```

## 使用new创建动态数组
---

- ```
int num = 100;
int * psome = new int[num];
//可以使用psome[0]这样的形式来访问数组元素,与普通的数组无异
...
delete []psome;
```
**delete的方括号告诉程序,应该释放整个数组,而不是仅仅是指针指向的元素**

- C++将数组名解释为地址(一般情况)

- 数组名被解释为其第一个元素的地址,而对数组名应用取地址符时,得到的是整个数组的地址.
```
short tell[10];
cout << tell << endl;   //display &tell[0]
cout << &tell << endl;  //display address of whole array
```
上面这个例子中,从数值上来说,这两个地址相同;但从概念上来说,`&tell[0]`(即tell)是一个2字节内存块地址,**而&tell是一个20字节内存块的地址**.因此,表达式tell+1将地址的值加2,而表达式&tell+1将地址的值加20.

- 换句话说:**tell是一个short指针(*short),而&tell是一个这样的指针,即指向包含20个元素的short数组(short(*)[20]).** 这种指针可以这样初始化:`short (*pas)[20] = &tell`.这里pas的类型为`short (*)[20]`

## 小结
---

- 应将内存地址赋值给指针.

- 可以是对已经赋值的变量名使用`&`来获得 *被命名的内存的地址*, 或者使用new运算符返回未命名的内存的地址,只有这两种情况可以赋值给指针.
