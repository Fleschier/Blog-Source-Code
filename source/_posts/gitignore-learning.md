---
layout:     post
title:      "gitignore的使用及写法"
date:       2018-10-27 18:32:00
categories: Computer
tags: [๑Git, ๑Ubuntu, ๑Linux]
description: "学习记录"
---

## gitignore的作用
---

- 对于git同步到github来说，估计没有人会 `git add 文件名`这样的方式来添加到工作区的，都是`git add .`这样一次添加吧

- 但是，有时候我们直接add所有的文件会将一些我们不需要的生成的临时文件也加入进去，导致文件冗余。同时，更有可能的是我们在push的时候失败，由于一些不支持的文件类型或者文件大小过大。

- 这时候我们就需要gitignore脚本来过滤我们需要上传的文件。

## 命名格式以及位置
---

- 命名统一为`.gitignore`

- windows下由于不能文件名为空，则可以先命名为`.gitignore.`，回车确定之后windows会自动将最后一个点去掉。

- `.gitignore`文件放在根目录下即可。

## 内容写法
---

- gitignore本质上是一个按正则表达式匹配文件名/文件夹名的文件。

### 语法：(与正则表达式几乎一致)

- 空行或是以`#`开头的行即注释行将被忽略

- 以斜杠 `/`结尾表示目录

- 以星号`*`通配多个字符

- 以问号 `?` 通配单个字符

- 以方括号 `[]` 包含单个字符的匹配列表

- 以叹号 `!` 表示不忽略(跟踪)匹配到的文件或目录

- [参考](https://www.cnblogs.com/jingtyu/p/6831772.html)

## 添加github仓库
---

- github上有一个为各种环境和编程语言提供gitignore模板的项目——[https://github.com/github/gitignore](https://github.com/github/gitignore)

> 他的项目介绍是：This is GitHub’s collection of .gitignore file templates. We use this list to populate the .gitignore template choosers available in the GitHub.com interface when creating new repositories and files.(意思大概就是可以用它来实现在创建repository的时候可以选择初始化一个.gitignore文件，并且可以选择一个模板)

- 我们在创建github仓库的时候尽量先预先创建好.gitignore文件，因为一旦push之后，添加了新的.gitignore貌似也是不起作用的，非常麻烦，所以要养成写.gitignore的好习惯。
