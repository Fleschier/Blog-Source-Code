---
layout:     post
title:      "Ubuntu进阶记录 & Ubuntu-18"
date:       2018-05-10 09:47:00
categories: Computer System
tags:  [๑Ubuntu, ๑Linux]
description: "学习记录"
---

## Ubuntu18 使用体验
---

## 一些装机软件的安装
---

- 由于Ubuntu 18 自带了 gnome3.0桌面,所以我们只需要下载一个tweak-tool据可以自定义桌面了：
```
sudo apt-get update
sudo apt-get install gnome-tweak-tool
```

- 这次Ubuntu把标题栏改到了窗口的右侧，如果要改到左侧的话，打开tweak-tool转到窗口里面更改即可。

- 在更改用户主题之前，我们需要添加一个拓展插件才能使用自定义的主题
```
sudo apt-get install gnome-shell-extensions
```
或者在gnome拓展网站上搜索 shell extensions ，找到这个插件并且安装最后重启tweak-tool即可。

### Albert

- 一款很强大的快捷交互命令行。

- 勾选extention后可以执行强大的命令包括文件，程序，终端，计算器等等。

- 安装步骤：
1. ```
wget -nv -O Release.key \
  https://build.opensuse.org/projects/home:manuelschneid3r/public_key
sudo apt-key add - < Release.key
sudo apt-get update
```
2. ```
sudo sh -c "echo 'deb http://download.opensuse.org/repositories/home:/manuelschneid3r/xUbuntu_18.04/ /' > /etc/apt/sources.list.d/home:manuelschneid3r.list"
sudo apt-get update
sudo apt-get install albert
```

- [官网](https://albertlauncher.github.io/docs/installing/)

## 主题修改
---

- 在网上找好主题以及美化的图标之后，分别下载下来，在home下创建 `.themes` 和 `.icons`两个文件夹，把主题和图标分别放到两个文件夹下即可使用。

- [一个mac风格的主题](https://imcn.me/html/y2017/29004.html)

## gnome extensions recommend
---

### Ubuntu强大就强大在其可自定义的系统插件,这里罗列一下我自己使用的插件.

- Desktop Scroller: 可以在左右上下(用户自定义)屏幕边滑动鼠标滚轮来实现工作区的切换,十分便捷

- Drop Down Terminal: 从顶端展开的一个终端,可以跨工作区.

- Keep awake!: 手动激活按钮使电脑不会进入待机状态

- NetSpeed: 显示当前网速

- Place Status Indicator: 可以快速获取当前位置和切换位置

- Removable Drive Menu: 显示当前是否有挂载的设备,并且可以一键解除挂载

- Screenshot Tool: 屏幕截图工具

- User Themes: 可以自定义用户主题的拓展,必备.

- Blyr：使Overview有模糊背景效果

- Coverflow(Alt-Tab)：应用程序切换效果，类似Mac OS X

## 使用ppa源时可能遇到的问题以及解决方案
---

- 遇到 `sudo apt-get update` 时提示 *无法安全地用该源进行更新，所以默认禁用该源*,使用`sudo apt -o Acquire::AllowInsecureRepositories=true update`来强制更新不安全的源。

- 遇到没有签名的问题时，使用 `sudo apt-get update --allow-unauthenticated`


## Ubuntu18装机的坑
---

- ubuntu对独立显卡的支持很有问题，导致我在安装时一进去就卡死，后来找到了解决方法。

- 在进入安装界面之前(选择体验还是安装的那个界面)时侯按 e 进入启动参数编辑 ，找到 quiet splash 这一句，把它删掉，改为  `i915.modest=0  nouveau.modeset=0  nomodeset` (参数之间空格间隔) 然后 ctrl+x 就可以进入安装界面了。但是此时的安装界面分辨率是900*400的，贼坑，还好我只是覆盖安装之前的Ubuntu16，所以自动安装也还凑合，如果要手动分区安装的话就悲剧了...

- 同样的，在安装完成之后重启进入ubuntu系统之前(在那个紫色的界面时)还要按 e 进入启动参数编辑界面，更改同上，进入系统之后，找到 系统设置>软件和更新>附加驱动，安装Nvidia的独显驱动然后重启即可。

- 按下 alt + F7 之后就可以不受限制地自由移动窗口了。

- 详见我知乎上的[文章](https://www.zhihu.com/question/276308597/answer/388030874)

### 终端的字体

- 如果要自己更改一些字体的话，在tweak-tools 里面其他的字体都可以随便改，但是等宽字体不能随便该，否则终端的字体会出现交叠错乱的情况。终端的字体由等宽字体来控制，一定要选择以 "mono" 开头或者结尾的字体才不会出现问题。


## 相比较 Ubuntu 16.04LTS
---

- 网易云音乐比Ubuntu16更加坑了～我内心是万马奔腾的...

- ss-Qt5也用不了，翻墙只能靠命令行ssr了

- 搜狗输入法也是各种安装失败，我也懒得搞了，但是Ubuntu 18 的内置中文输入法手感贼舒服～搜狗装不上也就算了


## Ubuntu的问题查询
---

- 很多时候国内的一些论坛无法解决我们在使用Ubuntu时遇到的一些问题，这时候就需要去一些国外的论坛上找我们需要的解答。这里推荐一个网站——[askUbuntu](https://askubuntu.com)

## Ubuntu 18 下可以使用的 ssr
---

- [链接](https://github.com/erguotou520/electron-ssr/releases)

- 配置方法与windows几乎一致

## 关于网易云音乐安装之后必须要终端sudo才能打开的问题
---

- 首先sudo打开会有报错,但是会自动启动默认设置

- 根据报错我们可以进行对应的安装: `sudo apt-get install libcanberra-gtk-module`

- 然后修改网易云音乐的desktop文件，在exec那一行 `%U` 之前 加上 `--no-sandbox`然后保存退出，重启电脑即可愉快的使用了～～(注意修改文件之前先要切换到root用户)

- 另一种神奇的打开方式(不需要上面的操作):启动之后，点关机按钮，弹出来确认框，随后网易乐音乐页面也弹出来了，这时取消关机，可以正常使用云音乐~~~~~~~

-------

### 2019.3.21更新

- 最近又发现了一个 **完全解决问题** 的方法:

- 把`%U`那一行改为:`Exec=sh -c "unset SESSION_MANAGER && netease-cloud-music %U"`

#### 然后关于每次正常启动要重新登录的问题

- 把`.cache`文件夹下的`netease-cloud-music`全部删掉(这是缓存文件夹).然后查看`.config`文件夹下的`netease-cloud-music`的所有权是否是自己的当前用户.如果是root的话要改.

- 参考 -- [https://www.zhihu.com/question/277330447/answer/478510195](https://www.zhihu.com/question/277330447/answer/478510195)

- 然后终于可以美滋滋地使用了~

## 关于ibus输入法的问题
---

- 最近输入法中文一直有问题，没办法选词。

- [博客链接](https://blog.csdn.net/AshinLi/article/details/72773989)

- 终端打开ibus设置命令：`ibus-setup`

- 但是感觉上面这个办法并没有声什么卵用。。。。

- 所以我弃坑了，还是选择了搜狗输入法

### Ubuntu18 的搜狗输入法的安装

- 首先安装fcitx的相关依赖
```
sudo apt-get install fictx-bin
sudo apt-get install fictx-table
```

- 然后安装下载好的搜狗输入法deb包
`dpkg -i sougou...`
这里应该会提示缺少依赖，这时候可就需要执行修复依赖：
```
sudo apt-get update
sudo apt-get upgrade -f
```
系统会自动修复缺少的依赖包

- 然后我们就可以安装完搜狗输入法了。这时候在系统语言设置(右上角)里更改键盘输入法系统为fictx，然后把不用的输入法去掉。

- 最后重启电脑，打开fictx配置下搜狗输入法，把他调到第一个即可。

- 搜狗输入法支持登录一键同步，还是很好用的～

### 搜狗輸入法的新坑

- Ubuntu18 自从安装以来一直问题不断。

- 最近启动电脑发现搜狗输入法的候选词栏全变成了乱码。。。坑爹啊

- 后来百度了解决方法：

- 首先遇到高级全都勾上以便显示出所有的可更改项
进入fictx设置>>附加组件>>简繁转换>>点击配置>>勾上显示高级选项>>将`sogoupinyin:false`改为`sogoupinyin:true`

- 但是这个方法只管用一次...下次重启还要手动改~~垃圾

- 所以接下来这个方法貌似有用(亲测)

- 输入如下命令：(就是把你个人用户的一些配置删除掉然后重新创建)
```
cd ~/.config
sudo rm -rf SogouPY* sogou*
```
- 之后注销重新登录即可。

- **就目前个人测试的结果看来，登录个人中心是元凶，登录之后必炸...还是老老实实地用最基本的功能吧，期待早日更新吧。**

## 10.15更新

- [Ubuntu18.04详细配置、美化](https://zhuanlan.zhihu.com/p/41708902#2-%E7%BD%91%E6%98%93%E4%BA%91%E9%9F%B3%E4%B9%90)

- [gnome主题网站](https://www.gnome-look.org/)

<br>
> 最后更新于2018.5.14
