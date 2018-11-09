---
layout:     post
title:      "Ubuntu18 安装Docker"
date:       2018-11-8 18:40:00
categories: Docker
tags:   [๑Ubuntu, ๑Docker]
---

## 为什么用Docker
---

- 环境搭建一直是运维一件非常头疼的事情, 如果系统崩溃而重新安装系统,则所有的环境都需要重新搭建一遍,非常耗时而且恼人.

- 我使用的Ubuntu18下配置好了大量的环境,如果这时候要我重新安装一遍的话,就算我做了详细的记录,也至少是一下午的工作量.

- 而Docker相当于一个容器,与虚拟机不同,虚拟机模拟了一个完整的操作系统,非常消耗系统资源,而且就算不做任何操作,内存也必须被占用.而Docker是容器,基于Linux容器的概念,封装而成.

- Docker将运行在其中的软件隔离开来, 不占用额外的系统资源.

- Docker 将应用程序与该程序的依赖，打包在一个文件里面。运行这个文件，就会生成一个虚拟容器。程序在这个虚拟容器里运行，就好像在真实的物理机上运行一样。有了 Docker，就不用担心环境问题。

## Docker Hub
---

- Docker Hub是一个平台,注册之后我们可以下载使用别人搭建好的image,非常方便.

## Ubuntu18安装Docker
---

- 由于Docker被墙得厉害,导致经常性地连官网也进不去.

- 我们为了安装过程的顺利,首先切换到中国科技大的源:
```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
sudo apt update
```

- 安装需要的包:`sudo apt install apt-transport-https ca-certificates software-properties-common curl`

- 添加 GPG 密钥，并添加 Docker-ce 软件源:
```
curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu \
$(lsb_release -cs) stable"
```

- 更新缓存:`sudo apt update`

- 安装Docker-ce:`sudo apt install docker-ce`

- 测试Helloworld:`sudo docker run hello-world`

- 结果:
![](/images/Docker/docker-01.png)

- 添加当前用户到 docker 用户组，可以不用 sudo 运行 docker:
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

## docker pull之后文件的存放目录
---

- 使用`docker pull XXX`下载的文件存放在`/var/lib/docker/`中

- 其中目录结构如下:
![](/images/Docker/docker-02.png)

- `containers`中每个序列号都是一个镜像

- Docker是使用repositories JSON文件来记述镜像信息的，此JSON文件包含了仓库名、标签、以及标签对应的镜像ID。

## Uninstall Docker-ce
---
> 摘自官方文档

- Uninstall the Docker CE package:`sudo apt-get purge docker-ce`

- Images, containers, volumes, or customized configuration files on your host are not automatically removed. To delete all images, containers, and volumes:`sudo rm -rf /var/lib/docker`
