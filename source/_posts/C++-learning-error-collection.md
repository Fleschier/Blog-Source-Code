---
layout:     post
title:      "C++学习笔记——一些报错信息归因"
date:       2018-10-08 22:43:00
categories: Computer Programs
tags: ๑C++
description: "学习记录"
---

## Expression: public_stream != nullptr
---

- 出现这个原因的问题很简单，就是用fopen打开文件失败了，创建的文件指针为空引起的。

- 解决方法就是查看文件路径是否正确。

- 在最后`fclose`的时候，先判断一下文件指针是否为空。


## abort() has been called
---

- 出现这个错误的原因基本上是越界或者内存泄漏。

- 这里的越界包括指针越界和数组越界
