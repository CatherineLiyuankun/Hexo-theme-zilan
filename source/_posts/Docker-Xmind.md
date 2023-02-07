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

# docker练习

## Create two Docker containers sharing the same PID namespace

https://killercoda.com/killer-shell-cks/scenario/container-namespaces-docker

Run two Docker containers `app1` and `app2` with the following attributes:

- they should run image `nginx:alpine`
- they should share the same `PID` kernel namespace
- they should run command `sleep infinity`
- they should run in the background (detached)

Then check which container sees which processes and make sense of why.

### Solution

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

## Container Namespaces Podman

https://killercoda.com/killer-shell-cks/scenario/container-namespaces-podman

Create two Podman containers sharing the same PID namespace
Run two `Podman` containers `app1` and `app2` with the following attributes:

- they should run image `nginx:alpine`
- they should share the same `PID` kernel namespace
- they should run command `sleep infinity`
- they should run in the background (detached)

Then check which container sees which processes and make sense of why.

### Solution

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

## Static Manual Analysis Docker

https://killercoda.com/killer-shell-cks/scenario/static-manual-analysis-docker

### Analyse K8s Pod YAML

Perform a manual static analysis on files `/root/apps/app1-*` considering security.
Move the less secure file to `/root/insecure`

#### Tip

Using a smaller base image to run the application can be more secure.
[Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices)

#### Solution

```bash
cd /root/apps/
ls
  app1-214422c7-Dockerfile  app2-2782517e-Dockerfile  app3-1c8650b1-Dockerfile
  app1-9df32ce3-Dockerfile  app2-5cde5c3d-Dockerfile  app3-4049a117-Dockerfile

# File `app1-214422c7-Dockerfile` uses multiple stages, a larger for building and a smaller for running.
FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go
FROM alpine   # uses multiple stages
COPY --from=0 /app .
CMD ["./app"]

# File `app1-9df32ce3-Dockerfile`
FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go
CMD ["./app"]

# 
mv /root/apps/app1-9df32ce3-Dockerfile /root/insecure
```

---

### Analyse K8s Deployment YAML
Perform a manual static analysis on files `/root/apps/app2-*` considering security.
Move the less secure file to `/root/insecure`

#### Tip

Running applications as not root inside a container can be more secure.

#### Solution

```bash
# File app2-2782517e-Dockerfile
FROM ubuntu:20.04
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go=2:1.13~1ubuntu2
COPY app.go .
RUN CGO_ENABLED=0 go build app.go
FROM alpine:3.12.0
RUN addgroup -S appgroup && adduser -S appuser -G appgroup -h /home/appuser
COPY --from=0 /app /home/appuser/
USER appuser  # File app2-2782517e-Dockerfile creates a new user and doesn't run the application as root.
CMD ["/home/appuser/app"]

# File app2-5cde5c3d-Dockerfile
FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go
FROM alpine:3.11.6
COPY --from=0 /app .
CMD ["./app"]

# File app2-2782517e-Dockerfile creates a new user and doesn't run the application as root.
mv /root/apps/app2-5cde5c3d-Dockerfile /root/insecure
```

---

### Analyse K8s StatefulSet YAML

Perform a manual static analysis on files `/root/apps/app3-*` considering security.
Move the less secure file to `/root/insecure`

#### Tip

Docker containers work with layers. Every FROM , COPY , RUN and CMD will create one layer.

#### Solution

```bash
# app3-1c8650b1-Dockerfile 
FROM ubuntu
COPY my.cnf /etc/mysql/conf.d/my.cnf
COPY mysqld_charset.cnf /etc/mysql/conf.d/mysqld_charset.cnf
RUN apt-get update && \
    apt-get -yq install mysql-server-5.6 &&
COPY import_sql.sh /import_sql.sh
COPY run.sh /run.sh
RUN /etc/register.sh $SECRET_TOKEN  # new layer
EXPOSE 3306
CMD ["/run.sh"]

# app3-4049a117-Dockerfile
FROM ubuntu
COPY my.cnf /etc/mysql/conf.d/my.cnf
COPY mysqld_charset.cnf /etc/mysql/conf.d/mysqld_charset.cnf
RUN apt-get update && \
    apt-get -yq install mysql-server-5.6 &&
COPY import_sql.sh /import_sql.sh
COPY run.sh /run.sh
RUN echo $SECRET_TOKEN > /tmp/token   # new layer
RUN /etc/register.sh /tmp/token       # new layer
RUN rm /tmp/token                     # new layer
EXPOSE 3306
CMD ["/run.sh"]

# File app3-4049a117-Dockerfile stores the temporarily used token at /tmp/token .
# This is persisted as layer in the container even though the file is later deleted.
# Therefore:
mv /root/apps/app3-4049a117-Dockerfile /root/insecure
```