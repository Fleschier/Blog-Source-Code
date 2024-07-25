---
layout:     post
title:      "BootStrap4-响应式建站"
date:       2019-04-09 11:46:00
categories: FrontEnd
tags:   [๑FrontEnd, ๑BootStrap]
description: "学习记录"
---

## 前言
---

- 最近学习需要,为了搭建网站方便,决定学习一下使用BootStrap.

- 目前最新的即为BootStrap4

- 参考教程-[菜鸟教程BootStrap4](http://www.runoob.com/bootstrap4/bootstrap4-tutorial.html)

> 本文仅为跟着教程自学梳理一遍,无他用.

## BootStrap4
---

- 使用CDN的库,也可以去官网下载文件到本地然后引入
```
<!-- 新 Bootstrap4 核心 CSS 文件 -->
<link rel="stylesheet" href="https://cdn.staticfile.org/twitter-bootstrap/4.1.0/css/bootstrap.min.css">

<!-- jQuery文件。务必在bootstrap.min.js 之前引入 -->
<script src="https://cdn.staticfile.org/jquery/3.2.1/jquery.min.js"></script>

<!-- popper.min.js 用于弹窗、提示、下拉菜单 -->
<script src="https://cdn.staticfile.org/popper.js/1.12.5/umd/popper.min.js"></script>

<!-- 最新的 Bootstrap4 核心 JavaScript 文件 -->
<script src="https://cdn.staticfile.org/twitter-bootstrap/4.1.0/js/bootstrap.min.js"></script>
```

- 一个简单的模板,注释在代码中:
```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <!-- 适配移动设备 -->
        <!-- width=device-width 表示宽度是设备屏幕的宽度。 -->
        <!-- initial-scale=1 表示初始的缩放比例。 -->
        <!-- shrink-to-fit=no 自动适应手机屏幕的宽度。 -->
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <!-- Bootstrap4 核心 CSS 文件 -->
        <link rel="stylesheet" href="https://cdn.staticfile.org/twitter-bootstrap/4.1.0/css/bootstrap.min.css">      
        <!-- jQuery文件。务必在bootstrap.min.js 之前引入 -->
        <script src="https://cdn.staticfile.org/jquery/3.2.1/jquery.min.js"></script>  
        <!-- popper.min.js 用于弹窗、提示、下拉菜单 -->
        <script src="https://cdn.staticfile.org/popper.js/1.12.5/umd/popper.min.js"></script>
        <!-- 最新的 Bootstrap4 核心 JavaScript 文件 -->
        <script src="https://cdn.staticfile.org/twitter-bootstrap/4.1.0/js/bootstrap.min.js"></script>
    </head>
    <body>
    </body>
</html>
```

### 两个容器类

1. `.container`,使得被修饰的容器为固定宽度
2. `.container-fluid`,使得显示为100%宽度,占据全部视口(viewport)
> *例如可用在`<div>`标签*

### 网格系统

- BootStrap提供的网格系统,会随着屏幕或视口(viewport)尺寸的增加,系统会自动分为最多十二列.也可以根据自己的需要重新定义列数.

#### 网格类

- `.col-`: 针对所有设备

- `.col-sm-`: 平板-屏幕宽度大于等于576px

- `.col-md-`: 桌面-屏幕宽大于等于768px

- `col-lg-`: >=992px

- `col-xl-`: >=1200px

- 以上的宽度要求均为最小宽度,最大宽度没有限制

##### 规则

- 网格的每一行需要放在`.container`或`.container-fluid`容器中,这样就可以自动设置一些外边距与内边距。

- 使用行来创建水平的列组。内容需要放置在列中，并且只有列可以是行的直接子节点。

- 预定义的类如 `.row` 和 `.col-sm-4` 可用于快速制作网格布局。

- **网格列是通过跨越指定的 12 个列来创建。** 例如，设置三个相等的列，需要使用用三个`.col-sm-4` 来设置。而设置4个相等的列,则使用四个`.col-sm-3`来创建.

- Bootstrap 3 和 Bootstrap 4 最大的区别在于 Bootstrap 4 现在使用 flexbox（弹性盒子） 而不是浮动。 Flexbox 的一大优势是，**没有指定宽度的网格列将自动设置为等宽与等高列.**

##### 例子

- 指定列的显示形式
```
<div class="row">
  <div class="col-*-*"></div>
</div>
<div class="row">
  <div class="col-*-*"></div>
  <div class="col-*-*"></div>
  <div class="col-*-*"></div>
</div>
```

- 其中第一个`*`表示需要响应的设备(见上文的5种设备),第二个`*`表示一个数字,显示在同一行的列数字之和需要为12.

- 让BootStrap自动处理
```
<div class="row">
  <div class="col"></div>
  <div class="col"></div>
  <div class="col"></div>
</div>
```
-  不在每个 col 上添加数字，让 bootstrap 自动处理布局，同一行的每个列宽度相等： 两个 "col" ，每个就为 50% 的宽度。三个 "col"每个就为 33.33% 的宽度，四个 "col"每个就为 25% 的宽度，以此类推。同样，你可以使用 `.col-sm|md|lg|xl`来设置列的响应规则。

##### 不等宽的例子

- ```
<div class="row">
  <div class="col-sm-4">.col-sm-4</div>
  <div class="col-sm-8">.col-sm-8</div>
</div>
```
并且,由于设置为`sm`,**则宽度不足576px时,两个列会自动上下堆叠显示**.其他的类推.

- 并且可以叠加使用:
```
<div class="container-fluid">
  <div class="row">
    <div class="col-sm-3 col-md-6 col-lg-4 col-xl-2">
      <p>RUNOOB</p>
    </div>
    <div class="col-sm-9 col-md-6 col-lg-8 col-xl-10">
      <p>菜鸟教程</p>
    </div>
  </div>
</div>
```
- 实例在平板、桌面、大桌面显示器、超大桌面显示器的宽度比例为分别为：`25%/75%、50%/50%、33.33%/66.67%、16.67/83.33%`, 在移动手机等小型设备上会堆叠显示。

- 总而言之,很灵活,并且不同的设备之间的类会一一对应,不会相互影响.


## 结尾
---

- 总之,BootStrap在建立网站的过程中非常好用,一些模板可以直接去网站上拷贝到本地修改即可使用.非常方便.
