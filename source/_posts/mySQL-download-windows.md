---
layout:     post
title:      "Windows10使用navicat链接mySQL错误"
date:       2018-11-9 09:40:00
categories: Docker
tags:   [๑Windows, ๑mySQL]
---

## 错误代码
---

- 安装mysql8.0服务器端，连接Navicat会提示报错：
`1251 Client does not support authentication protocol requested by server; consider upgrading MySQL client`

- 网上一堆方法,但是很麻烦

## 根本原因
---

- 最后终于发现了发生这种情况的根本原因,就是加密方式的更新.

- 由于最新版的MySQL安装的时候,推荐使用了一种最新的加密方式,就是在安装过程中,Authentication Method这一配置过程，给了两个基于不同的加密方式. 第一个是推荐的,当时我也没多想就选了第一个,所以才导致了后面的状况.

## 解决
---

- 再次打开mysql的安装程序,*这里不需要卸载重装*,选择更改设置, 将Authentication Method的加密方式改为第二个兼容加密方式就可以在navicat正确链接了.
