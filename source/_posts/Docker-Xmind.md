---
title: Docker-Xmind
catalog: true
date: 2021-12-27 22:11:54
subtitle:
header-img:
tags: 
- Cloud
- container
categories:
- TECH
- container
- Docker
---

# Docker Command[](http://liyuankun.top/Docker.html)

## 服务

### 查看Docker系统信息（信息比`docker version`更多）

- docker system info
  
### 查看Docker版本信息

- docker version

### 查看docker简要信息

- docker -v

### 启动Docker

- systemctl start docker

### 关闭docker

- systemctl stop docker

### 设置开机启动

- systemctl enable docker

### 重启docker服务

- service docker restart

### 关闭docker服务

- service docker stop

## 镜像

### 镜像仓库

- 检索镜像
  - `docker search 关键字`
- 拉取镜像
  - `docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]`

### 镜像管理

- 列出镜像
  - `docker image ls`
  - `docker images`

- 删除镜像
  - docker image rm <镜像Id>

- 导出镜像
  将镜像保存为归档文件
  - docker save
- 导入镜像
  - docker load

### Dockerfile构建镜像

Dockerfile 是一个文本格式的配 文件，用户可以使用 Dockerfile 来快速创建自定义的镜像。

Dockerfile 由一行行行命令语句组成，并且支持以＃开头的注释行.

- Dockerfile常见指令
下面是Dockerfile中一些常见的指令：

  - FROM：指定基础镜像

  - RUN：执行命令

  - COPY：复制文件

  - ADD：更高级的复制文件

  - CMD：容器启动命令

  - ENV：设置环境变量

  - EXPOSE：暴露端口

其它的指令还有ENTRYPOINT、ARG、VOLUME、WORKDIR、USER、HEALTHCHECK、ONBUILD、LABEL等等。

- 镜像构建
  - `docker build`
- 镜像运行
镜像运行，就是新建并运行一个容器。

  - `docker run [镜像ID]`


## 容器

### 容器生命周期

- 启动：启动容器有两种方式，一种是基于镜像新建一个容器并启动，另外一个是将在终止状态（stopped）的容器重新启动。

```bash
# 新建并启动
docker run [镜像名/镜像ID]
# 启动已终止容器
docker start [容器ID]
```

- 查看容器

```bash
# 列出本机运行的容器
$ docker ps
# 列出本机所有的容器（包括停止和运行）
$ docker ps -a
```

- 停止容器

```bash
# 停止运行的容器
docker stop [容器ID]

# 杀死容器进程
docker  kill [容器ID]
```

- 重启容器
  - `docker restart [容器ID]`

- 删除容器
  - `docker  rm [容器ID]`

- 进入容器
进入容器有两种方式：

```bash
# 如果从这个 stdin 中 exit，会导致容器的停止
docker attach [容器ID]

# 交互式进入容器
docker exec [容器ID]
```

进入容器通常使用第二种方式，`docker exec`后面跟的常见参数如下：

`－ d, --detach` 在容器中后台执行命令；
`－ i, --interactive=true I false` ：打开标准输入接受用户输入命令

### 导出和导入

- 导出容器

```bash
# 导出一个已经创建的容器到一个文件
docker export [容器ID]
```

- 导入容器

```bash
# 导出的容器快照文件可以再导入为镜像
docker import [路径]
```

### 其它

- 查看日志

```bash
# 导出的容器快照文件可以再导入为镜像
docker logs [容器ID]
```

这个命令有以下常用参数

```bash
 -f : 跟踪日志输出

--since :显示某个开始时间的所有日志

-t : 显示时间戳

--tail :仅列出最新N条容器日志
```

- 复制文件

```bash
# 从主机复制到容器
sudo docker cp host_path containerID:container_path 
# 从容器复制到主机
sudo docker cp containerID:container_path host_path
```

### Create two Docker containers sharing the same PID namespace

https://killercoda.com/killer-shell-cks/scenario/container-namespaces-docker

Run two Docker containers `app1` and `app2` with the following attributes:

- they should run image `nginx:alpine`
- they should share the same `PID` kernel namespace
- they should run command `sleep infinity`
- they should run in the background (detached)

Then check which container sees which processes and make sense of why.

#### Solution

```bash
# 1 Run first container
docker run --name app1 -d nginx:alpine sleep infinity

# We only see the processes of container app1
docker exec app1 ps aux

# Run second container in first containers PID namespace
docker run --name app2 --pid=container:app1 -d nginx:alpine sleep infinity

# We see processes of both containers in both containers
docker exec app1 ps aux
docker exec app2 ps aux
```

### Container Namespaces Podman

https://killercoda.com/killer-shell-cks/scenario/container-namespaces-podman

Create two Podman containers sharing the same PID namespace
Run two `Podman` containers `app1` and `app2` with the following attributes:

- they should run image `nginx:alpine`
- they should share the same `PID` kernel namespace
- they should run command `sleep infinity`
- they should run in the background (detached)

Then check which container sees which processes and make sense of why.

#### Solution

```bash
# Run first container
podman run --name app1 -d nginx:alpine sleep infinity

# We only see the processes of container app1
podman exec app1 ps aux

# Run second container in first containers PID namespace
podman run --name app2 --pid=container:app1 -d nginx:alpine sleep infinity

# We see processes of both containers in both containers
podman exec app1 ps aux
podman exec app2 ps aux
```

### 
