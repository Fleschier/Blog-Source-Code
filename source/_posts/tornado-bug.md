---
layout:     post
title:      "Tornado建站踩坑记录"
date:       2019-03-10 16:07:00
categories: Computer Programs
tags: [๑Python, ๑FrontEnd, ๑Tornado]
---

## 直入主题
---

- 被一个bug搞了一下午: 服务启动后localhost始终加载不出静态文件(诸如CSS,JS脚本,图片什么的).

- 仔细校验了文件中的路径,绝对路径和相对路径都试了,都是没用.

## 问题解决
---

- **如果有教程推荐你建的文件目录里有`statics`,相信我,你如果有机会见到它一定会砍死它**

- 错误的文件结构:
```
/.
|
handlers      //后端 Python 程序，主要处理来自前端的请求，并且操作数据库
|
templates   //存放html文件包括模板html文件
|
statics   //存放静态文件的目录
|
methods   //存放通用方法的目录,主要是供给handlers里面的程序调用
|
XXX.py    //python程序
...
```
> 如上的目录文件,你就算写死了,网站也不会加载出你的静态文件的

- **正确的目录结构**:
```
/.
|
handlers      //后端 Python 程序，主要处理来自前端的请求，并且操作数据库
|
templates   //存放html文件包括模板html文件
|
static      //存放静态文件的目录
|
methods   //存放通用方法的目录,主要是供给handlers里面的程序调用
|
XXX.py    //python程序
...
```
> 咋一看是不是一样啊,再仔细看看,static是没有s的.

- *只要你敢加上这个s,你就走远了...*

### 后记
---

- 这里感谢这位博主的文章,最终问题得以解决 [tornado 静态文件路径绑定细节](https://blog.csdn.net/uestc_v/article/details/83152390)

- 人生苦短, 我用python~
