---
layout:     post
title:      "Hexo插件live2d删除以及遇到的一些问题"
date:       2019-02-17 20:47:00
categories: Personal Blog
tags: ๑Blog
---

## 删除live2d插件
---

- 之前由于兴趣以及探索欲安装了live2d插件,但是在使用过程中不知道如何替换模型,也不是很懂怎么自己DIY模型,于是便放弃了这一插件.

- 首先删除`\themes\next\layout`下`_layout.swig`文件内的与live2d有关的代码

- 然后使用`npm uninstall hexo-helper-live2d`来删除这一momdule.

## 然而事情并没有结束
---

- 本以为这个事情就这样搞定了,直到最近我又`npm install`了一个插件,然后`npm audit fix`了一下,结果这个module就像幽灵一样又出现了!WTF?!

- 本着研究学习的想法捣鼓了半天也没用,只能按照原先删除的步骤再删除一遍

- 不过或许是`npm audit fix`这条命令的问题,查了一下:
> npm audit ： npm@5.10.0 & npm@6，允许开发人员分析复杂的代码，并查明特定的漏洞和缺陷。
npm audit fix ：npm@6.1.0,  检测项目依赖中的漏洞并自动安装需要更新的有漏洞的依赖，而不必再自己进行跟踪和修复。

- 官方还提供了其他的一些命令,比如:
```
(1)运行audit fix，但是只更新pkglock， 不更新node_modules：
$ npm audit fix --package-lock-only
```
```
(2)只更新dependencies中安装的包，跳过devDependencies中的包：
$ npm audit fix --only=prod
```
```
运行命令，得到audit fix将会更新的内容，并且输出json格式的安装信息，但是并不真的安装更新：
$ npm audit fix --dry-run --json
```
```
得到json格式的详细检测报告
$ npm audit --json
```

- 特此记录.
