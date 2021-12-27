---
title: Docker
catalog: true
date: 2021-12-22 22:10:03
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


# Docker 基本概念

镜像（`Image`）：Docker 镜像理解为一个包含了OS文件系统和应用的对象。是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。镜像不包含任何动态数据，其内容在构建之后也不会被改变。

容器（`Container`）：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的`类` 和 `实例` 一样，镜像是静态的定义，容器是镜像运行时的实体， 一个镜像可以运行为多个容器。容器可以被创建、启动、停止、删除、暂停等。

仓库（`Repository`）：仓库（Repository）类似Git的远程仓库，集中存放镜像文件。

三者关系：
![三者关系](https://ask.qcloudimg.com/http-save/yehe-7565276/joa65awgh4.png?imageView2/2/w/1620)

## 相关资料

`Moby`: [Docker开源项目](https://github.com/moby)，2017年正式命名为Moby(白鲸)， Github上的docker/docker库转移到[moby/moby](https://github.com/moby)。Apache协议2.0， Golang编写。
`Docker引擎`: `企业版（Enterprise Edition, EE）`， `社区版（Community Edition, CE）`， 每季度 企业版EE和社区版 CE都会发布一个稳定版本。 CE社区版又分为`稳定版（stable）` `抢先版（Edge）`，抢先版（Edge）每月发布。
`版本号`： 从2017年第一季度开始，YY.MM-xx格式， 例如18.06.0-ce（18年6月社区版）
`开放容器计划（The Open Container Initiative， OCI）`： 对容器基础架构中的基础组件进行标准化的管理委员会（在Linux基金会支持下运作）。 OCI已发布规范：`镜像规范`(类比铁轨尺寸)， `运行时规范`(类比相关属性).

# Doker安装

 方式 | Docker for Windows(DfW) | Docker for Mac(DfM) | Linux | Windows Server2016
---------|----------|---------|----------|---------
 类别 | 桌面安装 | 桌面安装 | 服务器安装 | 服务器安装
 要求 | 1 64位 2 Windows10 3 启用Hyper-v和容器特性 | MAC | Linux | Windows Server2016
 生产环境 | No，社区CE版本应用 | No，社区CE版本应用 | CE或EE |
 版本 | 稳定版（stable） 抢先版（Edge） |  |  |
 运行内核 | 默认Hyper-v虚拟机中的轻量级Linux，可切换为Native Windows 原生内核 | 轻量级Linux VM | Linux | Windows

Docker for Mac(DfM) 是一个流畅，简单并且稳定版的boot2docker.

# Docker 常用命令

![Docker 常用命令](https://ask.qcloudimg.com/http-save/yehe-7565276/6lldlbgfhn.png?imageView2/2/w/1620)

## 服务

查看Docker系统信息（信息比`docker version`更多）


```bash
$ docker system info
```

查看Docker版本信息，包含Client和Server信息。

```bash
$ docker version
Client:
 Cloud integration: v1.0.22
 Version:           20.10.11
 API version:       1.41
 Go version:        go1.16.10
 Git commit:        dea9396
 Built:             Thu Nov 18 00:36:09 2021
 OS/Arch:           darwin/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.11
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.9
  Git commit:       847da18
  Built:            Thu Nov 18 00:35:39 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.12
  GitCommit:        7b11cfaabd73bb80907dd23182b9347b4245eb5d
 runc:
  Version:          1.0.2
  GitCommit:        v1.0.2-0-g52b36a2
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

查看docker简要信息

```bash
$ docker -v
Docker version 20.10.11, build dea9396
```

```bash
docker --version
```

启动Docker

```bash
systemctl start docker
```

关闭docker

```bash
systemctl stop docker
```

设置开机启动

```bash
systemctl enable docker
```

重启docker服务

```bash
service docker restart
```

关闭docker服务

```bash
service docker stop
```

# 参考文章

- [一张脑图整理Docker常用命令](https://cloud.tencent.com/developer/article/1772136)
