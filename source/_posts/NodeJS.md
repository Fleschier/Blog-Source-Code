---
layout:     post
title:      "Node.js学习笔记"
date:       2018-05-21 10:47:00
categories: FrontEnd
tags:   [๑JS, ๑FrontEnd]
description: "学习记录"
---

> 不适合人类阅读的学习笔记

- **javascript每个语句结尾不要忘了分号**

## Ubuntu 下的node.js环境搭建
---

- 首先去nodejs的官网下载最新的版本，解压缩。然后移动到 `/opt/`目录下 (纯粹个人习惯)

- 然后编辑路径：
```
sudo su
vim /etc/profile
```

- 然后在最后插入:(具体路径以实际为准)
```
export NODEJS_HOME=/opt/node-v8.11.2-linux-x64
export PATH=$NODEJS_HOME/bin:$PATH
```

- 最后执行`source /etc/profile` 或者重启电脑即可使之生效。

- 终端输入：`node -v`查看，如果能正确现实版本号，则说明配置成功。


## Hello world
---

- 在常用目录下新建一个`HelloWorld.js`纯文本文件，在其中写入：
```
'use strict';
console.log('Hello, world.');
```

- 第一行总是写上 `'use strict';` 是因为我们总是以严格模式运行JavaScript代码，避免各种潜在陷阱。

- 保存退出，执行 `node HellowWorld.js`即可得到结果。(终端输出“Hello,world.”)

- 在交互模式下，单行命令一般不用加分号(有时候加分号还会报错)

## 交互模式
---

- 在终端输入 `node` 即可进入 node.js的交互环境，我们可以直接输入javascript代码并直接执行。

- 进入交互模式实际上是进入了node的解释器，交互模式下node会直接打印每一个语句的结果，而写在js文件里的代码想要输出结果，必须自己用console.log()打印出来。(这与python，scala的命令行解释器特性一致)

## 使用严格模式
---

- 如果在JavaScript文件开头写上`'use strict'`;，那么Node在执行该JavaScript时将使用严格模式。但是，在服务器环境下，如果有很多JavaScript文件，每个文件都写上`'use strict'`;很麻烦。我们可以给Nodejs传递一个参数，让Node直接为所有js文件开启严格模式：`node --use_strict XXX.js`

## IDE开发环境
---

### 在集成开发环境intellij IDEA下使用nodejs

- 我们可以尝试获取免费的注册码。

- 上述注册码的[获取地址](http://idea.lanyus.com/)


#### hosts 文件路径

- 在 iOS 系统中中，hosts文件的位置为：`~/private/etc`

- 在 Windows 系统中，hosts文件的位置为：`C:\Windows\System32\drivers\etc`

- 在 Ubuntu 系统中，hosts文件的位置为：`/etc`

## jetbrains学生免费账号申请
---

- [Jetbrains学生免费账号申请](https://sales.jetbrains.com/hc/zh-cn/articles/207154369-%E5%AD%A6%E7%94%9F%E6%8E%88%E6%9D%83%E7%94%B3%E8%AF%B7%E6%96%B9%E5%BC%8F)

- 申请流程其实很简单，你需要一个你们学校的邮箱即可。然后验证通过之后会发送验证邮件，依次填写并且最终注册完账号即可激活。**有效期至毕业。**

- 成功激活：

![](/images/node.js/info.png)


## 模块
---

- 在Node环境中，一个.js文件就称之为一个模块（module）。

- 分模块的好处是编写代码不必从零开始。当一个模块编写完毕，就可以被其他地方引用。我们在编写程序的时候，也经常引用其他模块，包括Node内置的模块和来自第三方的模块。

- 例如，我们在一个js文件(hello.js)中写一个函数：
```
'use strict';
var s = 'Hello';
function greet(name) {
    console.log(s + ', ' + name + '!');
}
module.exports = greet;
```
- 函数greet()是我们在hello模块中定义的，你可能注意到最后一行是一个奇怪的赋值语句，它的意思是，把函数greet作为模块的输出暴露出去，这样其他模块就可以使用greet函数了。

- 其他模块对本模块的调用,此处写一个main.js：
```
'use strict';
// 引入hello模块:
var greet = require('./hello');
var s = 'Michael';
greet(s); // Hello, Michael!
```

- 引入hello模块用Node提供的require函数,引入的模块作为变量保存在greet变量中。`./hello`表明hello.js和main.js是在同一个目录下，这里需要写 **相对目录**。

### CommonJS规范

- 这个规范保证了各个模块之间的同名变量和函数不会冲突

- 一个模块想要对外暴露变量（函数也是变量），可以用`module.exports = variable;`，一个模块要引用其他模块暴露的变量，用`var ref = require('module_name');`就拿到了引用模块的变量。

- 输出的变量可以是任意对象、函数、数组等等

- 引入的对象具体是什么，取决于引入模块输出的对象

- javascript本身并不支持同名函数或者变量冲突的处理，而node.js实现这一功能的原理是，JavaScript是一个函数式编程语言，node.js将每个模块包装为一个函数，这样这个模块里的变量就都成为了局部变量，这样就避免了冲突。——[详细教程](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001434502419592fd80bbb0613a42118ccab9435af408fd000)

<br>
> 最后更新于2018.5.24
