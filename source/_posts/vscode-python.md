---
layout:     post
title:      "VScode python编译错误问题记录"
date:       2019-03-05 21:43:00
categories: Computer Programs
tags: [๑VsCode, ๑Python]
---

## 问题
---

- 在Vscode上装完python环境后,在按F5运行后却报错了:
```
...
ImportError: No module named '_tkinter'
...
```

- python版本为3.6, pip版本为18

- 查阅了网上相关资料后发现是缺少包的原因,在终端中手动下载一下即可:
```
sudo apt-get install python3-tk
```
- 然后再运行python程序即可.
