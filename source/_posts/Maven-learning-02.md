---
layout:     post
title:      "Maven构建项目的pom.xml文件详解"
date:       2018-11-07 20:50:00
categories: Computer Programming
tags:   [๑Maven, ๑Apache]
---

## Maven仓库
---

- Maven仓库分为本地仓库,中央仓库和远程仓库.

- 中央仓库可以查询和获取大量常用的库----[地址](https://search.maven.org/#browse)

- 远程仓库是当我们在中央仓库也获取不到需要的库时,才会用到的. 一般也不会用到远程仓库.

### 仓库搜索顺序

- 首先,maven会在本地仓库中搜索依赖的库,如果没有就去中央仓库,如果中央仓库也找不到,但是pom文件里设置了远程仓库,则去远程仓库中获取,否则就会报错,找不到依赖的文件.

## Maven项目的创建
---

- 我们一般使用intellij IDEA来创建maven项目

- 其中的gourpId一般的命名格式为: 组织名，公司网址的反写 + 项目名称

### 项目模板

- Maven 使用 **archetype(原型)** 来创建自定义的项目结构，形成 Maven 项目模板。

- 我们在intellij IDEA中新建maven项目时,可以选择从创建一个archetype,这样maven会自动为pom.xml文件添加一些dependency

## Maven快照(SNAPSHOT)
---

- 快照是一种特殊的版本，指定了某个当前的开发进度的副本。不同于常规的版本，Maven 每次构建都会在远程仓库中检查新的快照。
> 对于版本，如果 Maven 以前下载过指定的版本文件，比如说 data-service:1.0，Maven 将不会再从仓库下载新的可用的 1.0 文件。若要下载更新的代码，data-service 的版本需要升到1.1。
快照的情况下，每次快照的更新，Maven 将自动获取最新的快照(data-service:1.0-SNAPSHOT)。

- 快照和版本是用于团队开发时的,快照是为了避免频繁地手动更新pom文件,也避免了版本号的滥用.
