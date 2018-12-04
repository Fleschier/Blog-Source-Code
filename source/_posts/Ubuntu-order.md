---
layout:     post
title:      "Ubuntu终端常用命令"
date:       2018-04-6 16:47:00
categories: Computer System
tags: [๑Ubuntu, ๑Linux]
---

> 不适合人类阅读的备忘笔记  

## 命令
---

### 常用基本命令

- `ls -l` 的简略写法就是 `ll`，但是这个与`ls -a`又不同，后者用来显示隐藏文件和文件夹。

- 使用 `vim`修改文件时，如果想要不保存退出，使用`:q!`命令。

- ubuntu改文件名用 `mv name1 name2`即可

- `cp filename filepath` //拷贝文件

- `cp -r 源目录  指定目录` //拷贝一个文件夹到另一个目录

- 从hdfs上取文件到本地需要链接集群，然后 `hdfs dfs -get /.../filename  storepath`

- 查看路径：例如用`which python`查看python安装的路径

- `sudo apt-get remove + 软件名` 用于删除apt方式安装的软件

- `chmod [-可选参数][<权限范围>+/-/=<权限设置>] 文件/目录`  //改变文件权限

- `chown [-R] username filename/directoryname`  //更改文件或者文件夹所属用户

- `touch 文件名`命令用来创建一个空的文件

- 查看系统的所有PATH环境变量： `echo $PATH`

- `rm -rf` 强制 递归地删除某个文件或者文件夹的所有文件

- `dpkg -i filename.deb`  //安装 .deb 文件

### grep语句

- Linux grep命令用于查找文件里符合条件的字符串。

- 简单命令格式： `grep [option] pattern file`
- 完整格式： `grep [-abcEFGhHilLnqrsvVwxy][-A<显示列数>][-B<显示列数>][-C<显示列数>][-d<进行动作>][-e<范本样式>][-f<范本文件>][--help][范本样式][文件或目录...]`

- **例（最常用）**：`cat AR_log | grep "===="
`此句就是打印日志AR_log当中所有包含了"===="的行

- 在当前目录中，查找后缀有 file 字样的文件中包含 test 字符串的文件，并打印出该字符串的行。此时，可以使用如下命令：
```
grep test *file
```

### apt常用命令

- `apt-cache search package` 搜索包

- `apt-cache show package` 获取包的相关信息，如说明、大小、版本等

- `sudo apt-get install package` 安装包

- `sudo apt-get install package - - reinstall` 重新安装包

- `sudo apt-get -f install` 修复安装 "-f = ——fix-missing"

- `sudo apt autoremove` **卸载某个软件并且删除与之相关的多余依赖**

- `sudo apt-get update` 更新源

- `sudo apt-get upgrade` **更新已安装的包**

- `apt-cache depends package` 了解使用依赖

- `apt-cache rdepends package` 是查看该包被哪些包依赖

- `sudo apt-get build-dep package` 安装相关的编译环境

- `sudo apt-get clean && sudo apt-get autoclean` 清理无用的包

- `sudo apt-get check` 检查是否有损坏的依赖

### scp语句

- 语法： `scp [可选参数] file_source file_target `

- 例：`scp /home/fleshier/My_Programes/Programes/AssociationRuleDiscovery/target/AR.jar   root@192.168.1.201:/root`
此句就是吧一个本地的文件拷贝到远端的服务器上，用户是root，服务器地址是192.168.1.201，存放目录是 `/root`

- 如果指定了用户名（如上例），则需要输入密码，如果没有指定用户名，则回车后需要输入用户名和密码。

- 使用参数`-r`来实现递归拷贝

例：`scp root@192.168.1.201:/root/runAR.sh /home/fleschier/cloud\ computing/
`从远程服务器拷贝到本地

- 远程服务器的格式为 `用户名@IP地址:文件路径`

- 额外说明：如果远程服务器防火墙有为scp命令设置了指定的端口，我们需要使用 -P 参数来设置命令的端口号，命令格式如下：
```
#scp 命令使用端口号 4588
scp -P 4588 remote@www.runoob.com:/usr/local/sin.sh /home/administrator
```

### curl命令

- curl命令是个功能强大的网络工具，支持通过http、ftp等方式下载文件、上传文件。还可以用来抓取网页、网络监控等方面的开发，解决开发过程中遇到的问题。

- curl安装：`sudo apt-get install curl`

- get请求：`curl http://www.baidu.com` 回车之后，HTML内容打印在屏幕上；如果这里的URL指向的是一个文件或者一幅图都可以直接下载到本地。

- 更多详细参数——[curl命令详解](http://www.cnblogs.com/linjiqin/p/5484910.html)


### gem命令

- 安装命令 `gem install appname`

- Gem 是一个管理 Ruby 库和程序的标准包

- 所有的 gem 包，会被安装到 `/[Ruby root]/lib/ruby/gems/[ver]/` 目录下，这其中包括了 `Cache、doc、gems、specifications` 4个目录，`cache` 下放置下载的原生 gem 包，`gems` 下则放置的是解压过的 gem 包。

- 当安装过程中遇到问题时，可以进入这些目录，手动删除有问题的 gem 包，然后重新运行 `gem install [gemname]` 命令即可。

<br>
- 参考资料：[linux命令大全-菜鸟教程](http://www.runoob.com/linux/linux-command-manual.html)以及各大博客网站大佬们的博文。

### df命令

- df命令用来查看磁盘上的空间，默认以KB为单位

- 一般使用`df-h`命令来以KB以上的单位显示，可读性高

- [详解](http://man.linuxde.net/df)

### find命令

- 语法：`find path -option [ -print ] [-exec -ok command ] {} \;`

- [详解](http://www.runoob.com/linux/linux-comm-find.html)

### du命令

- 一般使用`du -h [--max-depth = k] /路径`来查看这个目录下的各个文件占用的空间

- `--max-depth`用来调节深度，一般k取1

- [详细教程](https://www.jianshu.com/p/1c22dcb17a2e)

### 压缩命令

#### 使用tar指令

- Tar压缩文件: `tar [-zxcvfpP] filename` 

- `tar -N 'yyyy/mm/dd' /path -zcvf target.tar.gz source`

- 参数说明：
``` 
-z  ：是否同时具有 gzip 的属性？ 
-x  ：解开一个压缩档案的参数指令！ 
-t  ：查看 tarfile 里面的档案！
-c  ：建立一个压缩档案的参数指令 
-v  ：压缩的过程中显示档案！ 
-f  ：使用档名，请留意，在 f 之后要立即接档名,不要再加参数
-p  ：使用原档案的原来属性（属性不会依据使用者而变） 
-P  ：可以使用绝对路径 
-N  ：比后面接的日期(yyyy/mm/dd)还要新的才会被打包进新建的档案中！
--exclude FILE：在压缩的过程中，不要将 FILE 打包！ 
```
##### 例子

- `tar -cvf directory.tar directory`
//只将目录整合打包成一个档案 

- `tar -zcvf directory.tar.gz directory` 
//除了将目录打包外，同时以 gzip 压缩 

- `tar -zcvf filename.tar.gz  /home/test/*`
//将`/home/test/` 这个目录下的档案全部打包并压缩成为一个 filename.tar.gz 的档案

- `tar -jcvf /tmp/etc.tar.bz2 /etc` //打包后，以 bzip2 压缩

- `tar -xvf  directory.tar` 
//解 tar 的封包，请注意，由于没有 gzip (.tar 而非 .tar.gz) 的作用，所以只要使用`–xvf` 即可！不需要加上 z ，否则会显示有问题

- `tar -zxvf directory.tar.gz` 
//解压

- `tar –ztvf directory.tar.gz`
//查看 tar 里面的档案信息

- `tar -zcvPf home.tar.gz /home`
//则建立起来的压缩档内档案为绝对路径 
//请注意，使用这个 P 的参数时，不要将 P 加在 f 后面，因为 f 之后要立即接档名才行！

### HDFS相关命令

- 基本所有与HDFS相关的命令都以`hdfs dfs`开头

- `-mkdir /dirname` 创建hdfs目录

- `-ls /dirname[/...]` 列出某个目录下的所有文件

- `-rm -r /dirname` 删除某个目录及其所有子文件

- `-get /hdfs路径  /本地路径` 从hdfs拿文件到本地(例如`hdfs dfs -get /data/test.txt /home/xxx/`)

- `-put /本地文件路径 /hdfs路径`与拿文件相反,将本地一个文件传到hdfs上
