---
layout:     post
title:      "Windows10使用过程中遇到的一些坑"
date:       2018-07-23 20:40:00
categories: Computer System
tags:   ๑Windows
---

> 不适合人类阅读的学习笔记

## 解决windows下atom字体模糊的问题
---

- 这种情况是由windows下GPU的一些优化带来的问题，主要是会导致字体模糊。

- 也有人说是由于抗锯齿导致的问题

- 更改方法如下：

![](/images/Windows/atom.jpg)

## 关闭windows自动更新
---

- 首先`ctrl+s`呼出小娜，搜索`service`,出现服务这个匹配项。

- 在弹出的窗口中找到`Windows Update`的本地服务，右键 -> 属性，在弹出的窗口中，首先点击并停止服务，然后将启动类型由`自动`改为`手动`。

- 重启电脑即可。
