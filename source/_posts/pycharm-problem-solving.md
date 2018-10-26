---
layout:     post
title:      "Ubuntu18 Pycharm无法识别安装的Python库的解决方案"
date:       2018-10-16 00:47:00
categories: Computer Programes
tags: ๑Python
---

> 凌晨更~

## pycahrm无法识别
---

- 我们有时候在需要使用一些第三方python库的时候，需要`pip install XXX`，然而愉快地安装完了之后，在pycharm中新建项目`import`却失败，提示找不到。

- 这个问题坑了好久，在终端里使用完全没有问题然而pycahrm里却不行。今天终于下定决心搞定这个问题。

## 首先从默认python版本下手
---

- 由于我使用的是ubuntu18.04，其默认的python版本是python2.7，而我在IDE里使用的是后来安装的python3.6版本，因此pip install的module不会被识别(*因为终端里`pip install` 命令使用的解释器版本是2.7，安装的module也只能被2.7版本的识别*)

- 首先执行`python --version`查看当前默认版本

- 然后查看当前已安装的所有版本`ls /usr/bin/python*`

- 接着修改系统信息：(**需要管理员权限**)
```
root@fleschier-GE5S:/home/fleschier# update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
root@fleschier-GE5S:/home/fleschier# update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
update-alternatives: 使用 /usr/bin/python3.6 来在自动模式中提供 /usr/bin/python (python)
```
`--install` 选项使用了多个参数用于创建符号链接。最后一个参数指定了此选项的优先级，如果我们没有手动来设置替代选项，那么具有最高优先级的选项就会被选中。这个例子中，我们为 `/usr/bin/python3.6` 设置的优先级为2，所以`update-alternatives` 命令会自动将它设置为默认 Python 版本。


- 参考[更改Ubuntu默认python版本的两种方法](https://blog.csdn.net/fang_chuan/article/details/60958329)

### 一个坑接着一个坑

- 默认python版本改完了，下面就是`pip`了

- 改完之后会发现，执行`pip`命令会提示没有这个module。。。好吧又是坑

- 解决方案：`sudo apt-get install python3-pip`

- 安装完成然后就可以使用pip的一系列命令了

### 更新pip版本

- `python -m pip install --upgrade pip`

- 参考[stackoverflow的一个问题](https://stackoverflow.com/questions/18363022/importerror-no-module-named-pip)

## 然后就是重新安装我们需要的库了
---

- 我这里要搞一个python绘图，需要matplotlib库

-  按照其官方的安装方法(*仍然需要管理员权限否则最后一步会失败提示权限不够*):`python -m pip install -U matplotlib`

- 或者是一般的安装`pip3 install moduleName`

## 最后
---

- 最后就是网上烂大街的解决方法，指定pycharm的编译器为python3.x，即可～
