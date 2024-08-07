---
layout:     post
title:      "Welcome to Fleschier Blog"
date:       2018-04-5 22:47:00
categories: Personal Blog
tags: ๑Blog
description: "博客创建"
---

> “It's just a begining.”


## 前言

- 渐寒 的 博客终于开通了。

- 几经辗转，在github上发现了自定义的博客这一功能，终于可以自己写一些东西了。然而对于我这样一个对前端没啥了解的人来说，只能借用别人造好的轮子来自定义博客的风格。这一点等以后啥时候有兴趣学前端了再自己DIY吧。

---

## 正文

- 第一次自己写博客还是很有新鲜感的。

- 搭建自己在github上的博客需要创建一个名为*yourusername.github.io*的repository，然后你需要选择一款Jekyll主题来使你的博客更加个性化。*（当然像我一样的小白就先借用别人写好的框架来吧）*。在创建好repository之后最好先clone到本地，这样便于后面的更改直接在本地进行然后通过git来提交就好了。在github上选择一个别人写好的，你比较中意的主题，然后clone下来，将其中你需要的文件加到你自己的库当中。*（其中可能会包含别人写的文章啊，一些图片什么的，这些都可以删掉或者替换掉）*。这里附上一个相对比较详细的教程——[如何快速搭建自己的github.io博客](https://blog.csdn.net/walkerhau/article/details/77394659?utm_source=debugrun&utm_medium=referral)。
当然这里不可能把所有的细节都写清楚，有很多有趣的东西会在你尝试的过程中不断涌现出来，大胆的去尝试吧。


- 博文都是需要通过markdown编辑器来编写的。当然这也很简单，推荐使用的软件是[MarkdownPad2](http://markdownpad.com/)。如果需要激活秘钥什么的直接百度吧（滑稽）。这里需要补充一下的是，MarkdownPad2 这款软件使用时会产生bug，官方的说法是从 Win 8 开始就有这个问题了(我用的是win10)，解决办法就是安装 [Awesomium 1.6.6 SDK](http://markdownpad.com/download/awesomium_v1.6.6_sdk_win.exe)。如果还是不行就再安装 [Microsoft's DirectX End-User Runtimes (June 2010)](http://www.microsoft.com/en-us/download/details.aspx?id=8109)。下面是官方的原文：
>
LivePreview is not working - it displays an error message stating This view has crashed!
>  
This issue has been specifically observed in Windows 8. You may see an error message as shown here, and no HTML will be rendered when you type in the Markdown Editor pane.
>
To fix this issue, please try installing the Awesomium 1.6.6 SDK.
>
If you continue to experience issues, please install Microsoft's DirectX End-User Runtimes (June 2010).

- 对于提交的 XXX.markdown格式的文章，必须要放在`_posts`文件夹下，命名的格式必须为`YEAR-MONTH-DAY-title.markdown`
并且title也必须用-来连接而*不要用下划线，不要用下划线，不要用下划线...*

- 最后附上markdown的简单教程，很简单，一个小时之内上手完全没问题。[献给写作者的 Markdown 新手指南](https://www.jianshu.com/p/q81RER)。

## 关于多个标签
---

- 如果一篇博客归属于多个标签，则在tags一栏以 **空格** 分割各个标签。

## 使用jekyll本地预览网页
---

- 参考[我的另一个博客——Ubuntu下使用jekyll本地预览博客效果](https://fleschier.github.io/2018/07/08/Jekyll-usage/)

- [更详细的一个博客](https://github.com/uolcano/blog/issues/11)

## 关于表格对齐的问题
---

- 在表格的第二行：`|---|---|...|`这样的格式里，如果某个单元格写成`|---|`，则表示居中。如果写成`|:---|`则表示左对齐。

<br>

> 最后更新于2018.7.12
