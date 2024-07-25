---
layout:     post
title:      "在VScode使用Anacoda自带的tensorflow插件问题记录"
date:       2019-04-16 11:05:00
categories: [Python,Tensorflow]
tags:   [๑Tensorflow, ๑VScode]
description: "VScode python默认使用pylint,而pylint识别不了tensorflow框架,在import的时候一直报错"
---

## 前言

- 首先需要明确是否安装了tensorflow.**虽然Anacoda说是集成了Tensorflow,但是下载的部分是不包括Tensorflow的,需要自己安装才行.**

---
- **最新更新:pylint的问题现在已经不存在了,要是检测不到tensorflow,主要原因可能就是tensorflow未安装或安装不正确.**

## 问题记录
---

- 最近在写项目使用tensorflow做深度学习,使用了Anacoda并结合VScode来进行开发.

- 但是遇到一个问题,就是VScode python默认使用pylint,而pylint识别不了tensorflow框架,在import的时候一直报错.

## StackOverflow的解释
---

- [原问题及回答](https://stackoverflow.com/questions/49601292/python-not-finding-tensorflow-module-under-anaconda)

- 有用的一个回答:

> are you using Visual Studio Code (VSC) or just pylint in general? I found out the reason why this is happening.
For VSC, the python extension, use pylint for intellisense of python. Pylint seems to have a bug with the sub-module. For me, the error only shows in VSC and not in prompt.
I solved this problem by doing the following steps:
Click "Code" -> Click "Preferences" -> Click "Settings"
Now in the settings, you have a search bar on top, search:
python.linting.pylintEnable and set it to false
Now there is alternative for linting, I am using the pep8 as a example here since it come with the anaconda, search this
python.linting.pep8Enabled and set it to true
Now pylint is not the default linter anymore, we are now using the pep8. Just to make sure, quit VSC and reopen it. there should not be any error anymore.
I am fairly sure this is a problem with pylint, instead of the TF you installed. By default, the Microsoft python extension in the VSC is using pylint as the linting tool. By changing it to pep8 or other we can avoid the error.
大致意思就是,pylint在解析库的时候不会遍历深层的子目录导致找不到tensorflow.**解决办法是不使用pylint,改为pep8**

- 方法: 在VScode的设置中搜索`python.linting`,将`pylint.Enabling`勾掉,将`pep8.Enabling`勾上即可.同时我们还会发现还有许多其他的选项可以采用,这里不一一尝试了.

## 后续问题
---

- 采用pep8之后,果然问题解决了,但是又多了一个新的毛病: 很多报错.

- 仔细一看,诸如什么"一行过长","逗号之后空格没加"等等小问题,到了这里都变成了Error,就让人看起来很难受.

- 搜索了半天,也没找到合适的解决方法(国内论坛真是垃圾,还得自己想办法).

- 最终找到了一篇日本的,虽然看不懂日语,但是代码命令还是一目了然的,试了一下既简单又好用(这™就是差距啊~)

- [原文链接(需要翻墙)](https://qiita.com/zaki-yama/items/d05adce9d23d67144fbf)

- 解决方法如下:
1. 在家目录的.config文件夹下新建一个叫pep8的文件:
```
vim ~ .config/pep8
```

2. 在其中写入:
```
[pep8]
ignore = E226,E302,E41,E265,E231,E303
max-line-length = 200
```
其中,`ignore`后面的是需要忽略的编号,你可以查阅官方文档或者直接看终端的报错信息,在报错的最后会有编号,把想要忽略的加进来即可.

3. 保存文件,重启VScode即可.
