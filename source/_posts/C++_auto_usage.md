---
layout:     post
title:      "C++ auto关键字使用"
date:       2019-03-06 14:40:00
categories: Computer Programs
tags: ๑C++
---

## 简述
---

> auto的使用在C++11之后得以推广和支持

- 对于C++这门静态编程语言而言,所有的变量数据类型是需要明确声明的,在编译时即需要检查和确定.而诸如python这样的语言是动态判断变量类型的,在运行时才会确定数据类型.

- `auto`关键字赋予了C++强大的类型自动判断的能力,并且会在很长的类型声明的地方极大地简化我们的代码.

## 例子
---

- 例如:
```
//遍历vector,使用迭代器(原始版本)
for(std::vector<int>::iterator it = vec.begin(); it != it.end(); it++){
  ...
}
```
```
//简化版
for(auto it = vec.begin(); it != it.end(); it++){
  ...
}
```

- 还有一种遍历vector的简化写法(适合需要访问每个元素一遍的情况):
```
int main(){
  vector<int> vec;
  ....
  for(auto n: vec){   //这里n即为vec中的每个元素
    ...
  }
}
```

## 优点
---

- 简洁

- 在代码维护方面有一些"泛型"的好处,比如某个函数的返回值类型改变了,但是赋值的语句使用了`auto`关键字,那么便不再需要修改除函数以外的地方,减轻了代码的维护量.非常契合模板类等编程.

- 可以保存lambda表达式的类型的变量声明:
`auto ptr = [](double x){return 2*x;}; //类型为std::function<double(double))>函数对象`

## 注意点
---

- **使用`auto`声明的变量必须初始化**

- `auto`不能与其他类型组合使用,例如`auto int a;`是错误的.

- 函数和模板参数不能被声明为`auto`:
```
template<auto T>    //错误
```
> 因为auto本质上只是一个占位符,并不是一个数据类型,因此也不能用于类型转换和sizeof以及typeid等操作.

- `auto`会自动退化为指向数组的指针,除非被声明为引用
```
int arr[5];
auto x = a;
cout << typeid(x).name() << endl;   // result: int*
auto &y = a;
cout << typeid(y).name() << endl;   // result: int[5]
```
