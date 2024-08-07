---
layout:     post
title:      "UEFI双系统的那些坑"
date:       2018-04-06 09:40:00
categories: Computer System
tags: [๑DualSystem, ๑Ubuntu, ๑Linux]
description: "问题记录"
---
> 不适合人类阅读的自我备忘笔记  

## 关于ubuntu 和 windows 双系统
---

- 在长时间使用Windows时候，难免会想要尝试新系统，而专业又是如此，于是我选择了linux中图形界面最为友好的ubuntu系统作为自己双系统的入门系统。

- 虽然网上的双系统教程多说的很是简单，但是大多数已经是几年前的文章了，其中所讲的一些计算机的硬件系统已经落伍了，就比如说，网上绝大多数的双系统引导模式是建立在bios支持legacy（传统模式）模式下的，然而我自己的bios只能在UEFI模式下引导系统启动.....作为一名计算机系的学生当然不服气啊，当然各种百度什么的，期间踩过的坑实在难为外人道也。

- 如果你的电脑支持legacy模式的话，自行百度一些教程就行了。装好ubuntu系统之后，进入bios将启动顺序整下，将Ubuntu启动器放在Windows boot manager前面就可以了。因为Ubuntu启动器可以调用Windows boot manager 而Windows不能启动Ubuntu。

- 但是，UEFI作为最新的计算机启动模式，肯定要比原来的更加快速，或者如果你也像我一样，电脑不支持legacy启动，那么下面将要介绍一个非常好用的第三方启动引导程序。

## 第三方启动引导程序——refind
---

- refind是一款功能非常强大的开机启动引导程序，它能够自定义开机界面。你可以吧系统图标，背景什么的换成你自己喜欢的风格。这里附上一张我采用的主题开机界面![](/images/linux-and-windows/opening-bg.jpg)如果你也喜欢这一风格，[这里是链接地址](https://github.com/EvanPurkhiser/rEFInd-minimal)。

- refind是一款免费的软件([官方下载地址](http://www.rodsbooks.com/refind/getting.html))，如果你高兴也可以给作者赞助。

- 如果使用UEFI引导方式启动系统的话，**在安装Ubuntu时要预留一个efi分区用来存放开机引导文件**，预留大概200MB-500MB即可。

### Ubuntu下安装

- 推荐在ubuntu下安装refind，简单到让人不敢相信。你只需要把软件下载下来，在终端运行里面的.shell文件，就会自动安装，无需任何额外的操作，重启系统，进入bios在启动顺序里将rEFInd调为第一个即可。

### Windows下安装

- 如果你非要不信邪，在Windows下尝试安装的话，我也不反对。首先你需要一个能够进入系统隐藏分区的软件——[DiskGenius](http://www.diskgenius.cn/)。推荐去官网下载正版而不要用盗版（然后去百度激活码...咳咳），毕竟牵涉到系统文件万一崩了别怪我没提醒。

- 第一步，找到你系统的esp分区![](/img/linux-and-windows/ubuntu-boot.jpg)

- 第二步，将下载的refind文件夹及其里面所有的东西全部复制进去。*（注意：虽然DiskGenius支持同时复制多个文件，但是文件夹没法复制，只能自己先手动创建）* **同时必须要自己创建一个refind.conf文件，可以什么都不写但是不能没有。** 然后原来的refind.conf-sample文件就可以删除了。![](/img/linux-and-windows/refind-info.jpg)

- 第三步，将一些不需要的文件删除，如果你在网上下载了一些主题的话，也一并把文件复制进去。

- 第四步，下载[bootice](https://bootice.en.softonic.com/?ex=REG-60.2)，打开DIskGenius给你放refind文件的那个分区取个卷标（随便什么都可以，下面有用）。打开bootice——UEFI——修改启动序列![](/img/linux-and-windows/bootice01.jpg)*(也可以顺手吧下面那个下次启动直接进入bios勾上，省的下次进bios要手动)*。点击添加，找到你之前分配盘符的那个盘（也就是esp分区），找到里面的refind文件夹，选择对应你系统的.efi文件，点击确定。![](/img/linux-and-windows/bootice02.jpg)重启系统，进入bios，将rEFInd启动项调整为第一个即可。*（没有对比就没有伤害，Windows下简直烦死，还不一定成功...）*

- 最后希望各位都能成功在UEFI模式下完成双系统的安装和引导。

## 双系统时间差的问题解决
---

- 这个问题出现在切换系统时，每次时间都会错误到0时区。

- 解决方法：Ubuntu下关闭UTC(世界协调时间):

1. `sudo vim /etc/default/rcS`

2. 找到`UTC=yes`，改为`UTC=no`即可

- [详细原因](https://blog.csdn.net/gatieme/article/details/51883981)

- **但是注意**：在 Ubuntu **16.04** 版本以前，关闭UTC的方法是编辑`/etc/default/rcS`，将`UTC=yes`改成`UTC=no`， 但在Ubuntu 16.04使用systemd启动之后，时间改成了由timedatectl来管理，所以更改方法是:
```
timedatectl set-local-rtc 1 --adjust-system-clock
```
- 之后重启应该就不会出现问题了。

<br>

> 最后更新于2018.10.15
