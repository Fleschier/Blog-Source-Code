---
layout:     post
title:      "hexo重新构建博客"
date:       2018-09-03 17:25:00
categories: Personal Blog
tags:  ๑Blog
---

## 环境搭建
---

- 在使用hexo搭建博客之前，需要搭建好环境。需要git、node.js和hexo

- 详细搭建见——[链接](https://neveryu.github.io/2016/09/03/hexo-next-one/)

## hexo
---

- hexo有大量的主题可供选择，而且支持一键部署

- 但是hexo每次预览要重新生成页面，而jekyll是即时体现更改

### 安装

- `npm install -g hexo-cli`

### 常用命令

- 初始化： `hexo init  //在一个空文件夹下初始化`

- hexo一些命令：
```
$ hexo new "postName"  #新建文章
$ hexo new page "pageName" # 新建页面
$ hexo generate # 生成静态页面至public目录 =hexo g
$ hexo server # 开启预览访问端口(默认端口4000，'ctrl+c'关闭server) = hexo s
$ hexo deploy # 项目部署 = hexo d
$ hexo help # 查看帮助
$ hexo version # 查看Hexo的版本
```

## 一些问题记录
---

### 无法'hexo d':缺少插件

- 使用命令：`npm install hexo-deployer-git --save` (在博客的根目录下执行)

### 侧边栏文章索引错乱

- 尽量不要使用跳跃式的标题，比如使用了一个一号标题，然后使用了一个三号标题，接着又使用了一个一号标题，这样很容易就会出现错乱的现象。

- 标题应当逐级递增逐级递减，这样规范之后才会有清晰美观的显示效果。

#### 部署到git

- 部署到Github前需要配置`_config.yml`文件:
```
deploy:
	type: git
	repository: git@github.com:Fleschier/Fleschier.github.io.git
	branch: master
```

- 然后输入:`hexo d`

## 三部曲
---

- 修改然后预览
```
hexo clean
hexo g
hexo s --debug //运行预览同时实时生成错误报告
```

- 修改然后部署
```
hexo clean
hexo g
hexo d
```
