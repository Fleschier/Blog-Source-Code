---
layout:     post
title:      "Maven构建项目的pom.xml主要标签解释"
date:       2018-11-07 20:46:00
categories: Computer Programs
tags:   [๑Maven, ๑Apache]
---

## Maven pom.xml文件标签详解
---

> [菜鸟教程-maven标签详解](http://www.runoob.com/maven/maven-pom.html),为了方便记录到自己的博客下.

## 记录
---

|标签|描述|
|---|---|
|project|工程的根标签|
|modelVersion|模型版本,一般设为4.0|
|groupId|工程组的标志,一个项目或者一个组织一般是唯一的|
|artifaciId|工程标识,是工程的名称|
|version|工程版本号,在artifact的仓库中用来区分不同的版本|
|build|该元素设置了项目脚本的源码目录,当构建项目的时候,构建系统会编译目录里的源码,该路径相对于pom.xml是相对路径|
|dependencies|该元素描述了项目相关的所有依赖。 这些依赖组成了项目构建过程中的一个个环节。它们自动从项目定义的仓库中下载。|
|dependency|上个标签的子目录,一个dependency包含一个依赖|
