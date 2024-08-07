---
layout:     post
title:      "git 与 github 随笔"
date:       2018-04-11 22:04:00
categories: Computer
tags: [๑Git, ๑Ubuntu, ๑Linux]
description: "git使用记录"
---
> 不适合人类阅读的随笔~

## 本地初始化仓库并添加远程仓库
---

- 示例：
```
git init //初始化本地仓库
git add .  //将本地所有文件加到仓库里
git commit -m "..." //设置提交信息
git remote add origin git@github.com: ...  //添加远程仓库
git push -u origin master
```

## 关于 多用fetch，merge少用pull
---

- 有一篇[文章](https://www.oschina.net/translate/git-fetch-and-merge)提到了pull的一些弊端，主要是数据会被直接覆盖掉，这样回溯会比较麻烦。

## 关于windows和Ubuntu下的可视化git管理工具
---

### windows
- windows下有一个非常好用的git管理工具，与github有很好的连接——[github desktop](https://desktop.github.com/)。界面美观，方便好用。

- 同时要搭配Windows下的[git](https://git-scm.com/download/win)来使用。

- 登录你的github账号之后，便可以非常轻松地clone，add，commit，push等操作。

- 左上角点开选择clone到本地的repo，右键选择open in explorer 即可进入存放本地文件的位置。对文件进行过修改之后，按照下面的同步步骤即可。

- 推荐使用命令行来实现同步。左上角点开后选择要修改的repo，右键选择 open in command 即可进入命令行。

- 一些简单的命令操作：
```
git add .  //把本地的所有修改add
git commit -m "..."  //commit本地的修改，“...”中写本次修改的备注（这个备注必须有）
git push   //将本地的修改同步到github上
```
这样修改同步就完成了，一共只需要三步即可。

### Ubuntu

- Ubuntu下找到一个甚至比Windows下的 github desktop更加好用的软件——[GitKraken](https://www.gitkraken.com/)

- 在上面不仅可以进行查看同步等操作，甚至可以看到之前在这个repo当中所有的人做出的任何修改，并且可以查看修改了哪些内容！*但是唯一美中不足的是有些更加NB的功能要开vip...*

- 比Windows更加便捷的是，这里想要进入对一个repo进行同步的命令行（终端）时，只需要在界面按下`Alt+T`的组合键就可以打开相应的终端了。

### atom
---
- 讲道理第一次使用atom时我还是很震惊的，居然有这么好用的软件。atom是一款编辑器，Linux和Windows平台都有，但是这个小小的编辑器整合了许多功能于一身，诸如代码编辑，github仓库文件的编辑以及直接add-commit-push一条线操作等等，还有许许多多的插件等待你去发现。

- Atom自带支持markdown文件的编辑和预览，组合键 `ctrl + shift + m` 弹出预览。

- atom的[下载地址](https://atom.io/)

<br>
> 最后更新于2018.4.19
