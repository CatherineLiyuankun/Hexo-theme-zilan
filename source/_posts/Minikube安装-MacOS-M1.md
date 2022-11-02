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

参考[从零开始Minikube MAC](https://www.jianshu.com/p/92034019d7d6)

Minikube支持安装在OSX， Windows， Linux.

## 安装在本地mac上

```bash
brew install minikube
```

## 安装docker

目前看只有Docker Desktop for Mac (macOS)可以下载， Docker.dmg


## 安装 kubectl(K8s的CLI工具)

```bash
brew install kubectl
```

## 安装hyperkit (适合MAC x86)

```bash
brew install hyperkit
```

### 问题：Mac M1: hyperkit not supported

如果在Mac M1上`brew install hyperkit`, 报错

```bash
brew install hyperkit

hyperkit: The x86_64 architecture is required for this software.
Error: hyperkit: An unsatisfied requirement failed this build.
```

解决方法：

## 安装qemu (适合MAC M1)

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
- [推荐一款Kubernetes神器“minikube”](https://zhuanlan.zhihu.com/p/112755080)
- [k8s官方文档-Minikube](https://kubernetes.io/zh-cn/docs/tutorials/hello-minikube/)
