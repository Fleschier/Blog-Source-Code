---
layout:     post
title:      "Docker使用"
date:       2018-11-8 20:40:00
categories: Docker
tags:   [๑Ubuntu, ๑Docker]
description: "学习记录"
---

> 需要的docker image可以从Docker Hub获取

## Docker images
---

- Docker images文件: Docker 把应用程序及其依赖，打包在 image 文件里面。只有通过这个文件，才能生成 Docker 容器。image 文件可以看作是容器的模板。Docker 根据 image 文件生成容器的实例。同一个 image 文件，可以生成多个同时运行的容器实例。

- 查看本机的image文件:`docker image ls`

- 删除某个image:`docker image rm [imageName]`

### 获取image

- `docker image pull 仓库路径/文件名`

### 运行

- `docker container run containID`

- 可以先用`docker image ls`查看所有的镜像文件. 同时`docker container run`当本地仓库不存在相对应的image时,会自动从远程仓库获取,所以上面pull的一步不是必须的.

### 终止

- 有些容器需要手动终止,使用命令:`docker container kill containID`

## Docker container
---

- image 文件生成的容器实例，本身也是一个文件，称为容器文件。也就是说，一旦容器生成，就会同时存在两个文件： image 文件和容器文件。而且关闭容器并不会删除容器文件，只是容器停止运行。

- 列出正在运行的容器:`docker container ls`

- 列出所有的容器: `docker container ls --all`

### 删除容器

- `docker container rm containerID`

- 删除之后的容器不会再出现在容器列表里

## 创建自己的docker容器
---

- 待更新

## 补充
---

- **注意**,`docker container run`命令是创建一个container,每运行一次就会多一个容器,如果要重复使用一个容器需要用:`docker container start`

- 查看容器的输出,即容器里面shell的标准输出:`docker container logs containerID`. 如果`docker run`命令运行容器的时候，没有使用`-it`参数，就要用这个命令查看输出。

- 进入一个正在运行的容器:`docker container exec -it containerID /bin/bash`.如果`docker run`命令运行容器的时候，没有使用`-it`参数，就要用这个命令进入容器。一旦进入了容器，就可以在容器的Shell执行命令了。

- 从容器中拷贝文件到本地:`$ docker container cp containID:[/path/to/file] [/dest/path/]`. 如果要拷贝到当前目录,则可以写为:`$ docker container cp [containID]:[/path/to/file] .`
