---
title: Minikube安装-MacOS M1
catalog: true
date: 2022-11-02 20:14:52
subtitle:
header-img:
tags: 
- Cloud
- container
categories:
- TECH
- container
- Kubernetes
---

# Minikube 是什么

[Minikube Git](https://github.com/kubernetes/minikube)

> Minikube是一个可以快速构建一个单节点本地运行Kubernetes环境的一个工具，它专注于让快速创建本地Kubernetes环境，用于学习和开发。
> 抛去多集群有关的特性，Minukube构建的单节点集群，足以使用户探索和发现Kubernate的绝大多数主要功能。

# Minikube 安装

参考[Minikube 官方Installation文档](https://minikube.sigs.k8s.io/docs/start/)

Minikube支持安装在OSX， Windows， Linux.

本篇文章是按照安装MacOS来写的，其他操作系统请参考：

- [Minikube Linux 系统安装](https://www.zhaowenyu.com/minikube-doc/install/minikube-install-linux.html)
- [Minikube Windows 系统安装](https://www.zhaowenyu.com/minikube-doc/install/minikube-install-windows.html)

## 安装Minikube

### 通过Homebrew安装在本地mac上

最简单的安装方式Homebrew， 如果系统没有安装brew工具请参考[之前的文章](./%E7%A8%8B%E5%BA%8F%E5%91%98-MAC-%E9%87%8D%E6%96%B0%E8%A3%85%E6%9C%BA%E5%BF%85%E5%A4%872%E5%91%BD%E4%BB%A4%E8%A1%8C-%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE.html#%E5%AE%89%E8%A3%85homebrew)。

```bash
brew install minikube

# 查看minikube
which minikube

```

### 通过[Git安装](https://www.zhaowenyu.com/minikube-doc/install/minikube-install-macos.html)

## 安装docker

目前看只有[Docker Desktop for Mac (macOS)](https://docs.docker.com/desktop/install/mac-install/)可以下载.

## 安装 kubectl(K8s的CLI工具)

```bash
brew install kubectl

# 查看版本
kubectl version --client

```

## 安装虚拟机管理器

### 安装[hyperkit](https://minikube.sigs.k8s.io/docs/drivers/hyperkit/) (适合x86_64机器)

```bash
brew install hyperkit

# To check your current version, run: 
hyperkit -v

# If the version didn’t change after upgrading verify the correct HyperKit is in the path. run: 
which hyperkit

#Run to make sure the version matches minikube
docker-machine-driver-hyperkit version
```

#### 问题：Mac M1: hyperkit not supported

如果在Mac M1上`brew install hyperkit`, 报错

```bash
brew install hyperkit

hyperkit: The x86_64 architecture is required for this software.
Error: hyperkit: An unsatisfied requirement failed this build.
```

解决方法：

### 安装qemu (兼容MAC M1)

- [Mac M1: hyperkit not supported](https://github.com/kubernetes/minikube/issues/11885)
  - HyperKit is Intel-only, so the alternative to QEMU will be the new Virtualization.framework driver
    - `brew install qemu`
    - `minikube start --driver=qemu --memory=4Gb`

## 运行Minikube

```bash
minikube start --driver=hyperkit
```

或者

```bash
# Mac M1
minikube start --driver=qemu
```


## 参考文章

- [从零开始Minikube MAC](https://www.jianshu.com/p/92034019d7d6)
- [解决老版本MacOS安装问题-Mac OS 安装minikube](https://blog.csdn.net/Apple_wolf/article/details/125360717)
- [推荐一款Kubernetes神器“minikube”](https://zhuanlan.zhihu.com/p/112755080)
- [k8s官方文档-Minikube](https://kubernetes.io/zh-cn/docs/tutorials/hello-minikube/)
