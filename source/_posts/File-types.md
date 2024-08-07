---
layout:     post
title:      "一些文件类型记录"
date:       2018-04-15 16:47:00
categories: Computer
tags: ๑FileTypes
description: "学习记录"
---
> 不适合人类阅读的学习笔记  

## 一些特殊的符号收集
---

- [符号收集](https://blog.csdn.net/rhinemetal/article/details/6887172)

- [符号大全](http://www.fuhao123.com/fuhao/1.shtml)

## CSV文件（逗号分隔值文件格式）(XX.csv)
---

- .csv文件实际上就是一种文本文件，其**以纯文本形式存储表格数据**，一般以逗号或者制表符作为分隔符

### 规则
- 开头是不留空，以行为单位。（每行末尾只有换行符，没有别的分隔符）

- 可含或不含列名，含列名则居文件第一行。

- 一行数据不跨行，无空行。

- 以半角逗号（即,）作分隔符，列为空也要表达其存在。

- **不支持数字，不支持特殊字符**

> 实际上csv文件就类似于一个没有线的表格

## Markdown文件(XX.markdown / XX.md)
---
- Markdown 的目标是实现「易读易写」。可读性，无论如何，都是最重要的。一份使用 Markdown 格式撰写的文件应该可以直接以纯文本发布，并且看起来不会像是由许多标签或是格式指令所构成。Markdown 语法的目标是：成为一种适用于网络的书写语言。Markdown 不是想要取代 HTML，甚至也没有要和它相近，它的语法种类很少，只对应 HTML 标记的一小部分。Markdown 的构想不是要使得 HTML 文档更容易书写。在我看来， HTML 已经很容易写了。Markdown 的理念是，能让文档更容易读、写和随意改。HTML 是一种发布的格式，Markdown 是一种书写的格式。就这样，Markdown 的格式语法只涵盖纯文本可以涵盖的范围

- markdown可以直接在Atom中编辑和预览(ctrl + shift + m)

- markdown可以转换为pdf文件。你可以选择下载一些markdown编辑器来完成这个转化，但是，我在这里要推荐一个大佬的web应用(完美支持UTF-8中文编码，不会像其他的一些外国的网站转化时中文全部变成乱码的问题)，知乎上看到的。[在线markdown转化为PDF](http://www.mdtr2pdf.com/index_en.html)


## Appimage文件(XX.AppImage)
---

- AppImage是一种在Linux系统中用于分发便携式软件而不需要超级用户权限来安装它们的格式。[1] 它还试图让允许Linux的上游开发者来分发他们的程序而不用考虑不同Linux发行版间的区别。

### 特性
- AppImage不把Linux应用程序安装在文件系统相应的目录中。相反,它没有进行实际的安装。AppImage文件只是个压缩文件，在它运行时候挂载。

- 用AppImage打包的程序，一个程序就是一个文件。每一个文件都包含了该程序在其所要运行的目标平台上所需的运行库。AppImage文件是基于ISO 9660并经过zisofs压缩的包含有一个最小化的AppDir目录和一个极小的运行环境的文件。只要把这个文件添加到live CD中，这个程序便可被轻而易举地添加进live CD中。

- 用AppImage文件比安装一个应用程序更加简单。它不需要解压也不需要为系统环境做调整。使用主流Linux发行版的用户可以下载它，使其可执行，并且运行即可。

### 运行方法

- 添加可执行权限 `chmod a+x *.AppImage`

- 执行 `./*.AppImage`

- 或者 `右键 > 属性(properties) > 权限(Permissions) > 勾选Allow executing file as program`

- 之后直接运行即可

## DLL文件
---

- DLL是`Dynamic Link Library`的缩写，意为动态链接库。

>A DLL file, short for Dynamic Link Library, is a type of file that contains instructions that other programs can call upon to do certain things. This way, multiple programs can share the abilities programmed into a single file, and even do so simultaneously.

>Unlike executable programs, like those with the EXE file extension, DLL files can't be run directly but instead must be called upon by other code that is already running. However, DLLs are in the same format as EXEs and some may even use the .EXE file extension. While most Dynamic Link Libraries end in the file extension .DLL, others may use .OCX, .CPL, or .DRV.

- DLL文件存储了别的应用程序可以调用的做某项特定的事情的一系列操作，这样，多个程序就可以并发地执行一些操作，仅仅通过将这些操作写入一个文件。

- 操作系统有时候会因为中了流氓软件或者病毒而导致杀毒软件删除被感染的捆绑时清除dll文件，但是不到万不得已不要去第三方网页上下载缺失的dll文件——[Important Reasons NOT to Download DLL Files](https://www.lifewire.com/important-reasons-not-to-download-dll-files-2624455)。这篇文章详细地描述了直接下载缺失的DLL文件的可能的潜在危害。

- 如果电脑的DLL文件缺失导致某个软件不能运行之类的错误，尽量尝试重新安装这个软件而不是直接下载DLL文件来解决问题。

- 参考文档——[What Is a DLL File](https://www.lifewire.com/what-is-a-dll-file-2625852)
