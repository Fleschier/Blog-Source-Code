---
layout:     post
title:      "Windows10蓝屏巨坑--已填"
date:       2018-11-14 17:40:00
categories: Computer System
tags:   ๑Windows
---

## win10蓝屏问题
---

- 最近一个月也不知道干了啥,Windows有时候就是莫名其妙地蓝掉...内心无比崩溃

> 而且是我在玩Fortinite的时候无限崩...

## 问题规律
---

- 最近在使用Android Studio开发, 但是莫名其妙就模拟器打不开, intel虚拟线程插件安装也报错,就很炸裂.

- 偶然间又打开了我的木木模拟器,结果马上蓝屏!!!

- 至此我发现了蓝屏的一点规律性---跟模拟器(虚拟化技术)有关!!

## 有了线索,问题便得以解决
---

- 经过几番搜索和尝试, 最终锁定了问题的源泉---Windows服务--**Hyper-V**

- 原来是Windows自己的虚拟化技术与别的虚拟化技术有冲突, 导致了蓝屏的问题.

## 解决
---

- Ctrl+R -> control.exe(控制面板) -> 启动或关闭Windows功能 -> 取消Hyper-V服务 ->重启电脑
