---
layout:     post
title:      "hexo重新构建博客"
date:       2024-07-26 09:25:00
categories: Personal Blog
tags:  ๑Blog
description: "博客引擎升级"
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

## 添加页面
---

- 刚使用的主题是默认只有两个页面的，home和archive。要添加页面，需要在source中添加文件夹并创建index.md文件。

- 例如，添加tags页面：

1. 新建tags文件夹，并创建index.md
2. 在index.md中写入如下内容：
```
title: tags
date: 2016-09-05 23:41:32
type: "tags"
comments: false
```

1. 到_config.yml文件中将对应的路径添加进去(next主题默认是将这几个页面注释掉的，取消注释即可)
2. 重新建站即可看到效果

## 添加搜索引擎支持
---

- 首先登录google的[Search Console](https://www.google.com/webmasters/tools/home?hl=zh-CN)

- 因为hexo每次clean都会将验证的html删除，所以我们采用其他的验证方法。将Search Console给的meta标签的信息添加到主题的目录下`head.swig`文件中，这里使用的是Next主题,其他主题也是类似的，在`Hexo/themes/next/layout/_partials/head/head.swig`文件中原有meta标签后面添加刚才复制的meta标签。

- [百度搜索引擎](https://ziyuan.baidu.com/site/siteadd?siteurl=)

- 百度验证与google验证方法一致

- 重新deploy博客之后可以验证通过

- 一些细节补充见[博客](https://jactor-sue.github.io/how-githubio-blog-can-be-searched-by-google/)


### 安装插件

- 为Hexo安装`hexo-generator-sitemap`和`hexo-generator-baidu-sitemap`插件，在Hexo博客目录下运行：
```
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save
```

### 重新建站

- 配置Hexo的`_config.yml`文件，添加如下字段:
```
sitemap:
		path: sitemap.xml
baidusitemap:
		path: baidusitemap.xml
```

- 在博客的`_config.yml`文件中添加博客的url,**否则生成的站点地图在提交的时候会报错**。

- 例如我的：
```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://fleschier.github.io/
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
```

- 重新生成博客页面即可看到sitemap.xml文件和baidusitemap.xml文件

- 最后分别在google和百度搜索引擎界面提交各自的站点地图即可。

### 添加robots文件

- 可以在source文件夹下添加`robots.txt`文件来限制爬虫抓取网页的内容范围

- robots例子：
```
# hexo robots.txt
User-agent: *
Allow: /
Allow: /archives/
Allow: /tags/

Disallow: /vendors/
Disallow: /js/
Disallow: /css/
Disallow: /fonts/
Disallow: /vendors/
Disallow: /fancybox/

Sitemap: https://Fleschier.github.io/sitemap.xml
Sitemap: https://Fleschier.github.io/baidusitemap.xml
```

## 文章中的图片
---

- 由于换到hexo,图片的文件夹在themes文件夹下的source文件夹中,我们在博客中写图片路径时还是`/images/...`这样即可.

## md文章命名
---

- hexo文章的命名不需要日期。日期在文章的开头的date属性里写。

> 11.4日更
## hexo文章统计阅读量
---

- 使用leanCloud来完成访问统计

- 需要设置安全链接,参考[博客](https://leaferx.online/2018/02/11/lc-security/)

### 问题错误码429

- 出现这个问题的报错信息是`too many requests`,原因是我们使用leanCloud的免费版本线程数是十分受限的,在我们deploy的时候发送了太多的同步请求导致线程栈溢出而报错.

- 解决方案 ---[hexo-leancloud-counter-security 插件 Too many requests 错误](https://blog.csdn.net/weixin_42591190/article/details/80958675)

### 问题依旧存在
---

- *使用leanCloud deploy之后博客修改的内容迟迟没有生效不知为何,用git的方法deploy之后就能很快生效,难道只能两个方法各deploy一次?待续...*

### 更新

- 原来是我还缺少了一个步骤,就是需要在leanCloud的`云引擎>设置>deploy`中将自己的github仓库地址填入,并且将其deploy key添加到我们github的仓库deploy key 一栏中.如下

- ![](/images/hexo_blog/blog_deploy.png)

- ![](/images/hexo_blog/res.png)

- 最后不要忘了在leanCloud上点保存,并且生成生产环境:

- ![](/images/hexo_blog/res1.png)

- 但是好像还是不能同步到github...待更新

---

## 2024更新

> 时隔多年又重拾起来了技术博客的更新，就先从建站开始，更新一下流程和问题

### 网站搜索功能添加

- 需要安装`hexo-generator-searchdb`插件。
  
- 运行`npm install hexo-generator-searchdb --save`命令。

- 编辑博客根目录下的博客本地目录/_config.yml站点配置文件，新增以下内容到任意位置:
```
search:
  path: search.xml
  field: post
  format: html
  limit: 100000	# 注意如果文章字数较多的话这里的值要增加大一些，不然可能出现部署之后搜索样式错误的情况
```

- 编辑博客本地目录`/themes/hexo-theme-next/_config.yml`主题配置文件，启用本地搜索功能,将local_search:下面的`enable:`的值，改成`true`。

- 最后更新生成部署博客即可。

### 文章tag用图标代替#号

- 在主题配置文件搜索`tag_icon`，改为true即可。