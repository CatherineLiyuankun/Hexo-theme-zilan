---
title: Kubernates all you should know
catalog: true
date: 2021-12-22 22:11:07
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

# K8s基础知识

- [K8s 官方文档](https://kubernetes.io/docs/home/)
- [Kubernetes 知识合集（微信公众号）](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzIxMTE0ODU5NQ==&action=getalbum&album_id=2332884281821462529&scene=173&from_msgid=2650248506&from_itemidx=1&count=3&nolastread=1#wechat_redirect)
  - [新手必须知道的 Kubernetes 架构](https://mp.weixin.qq.com/s/uTBmNoXuiNyIkxRtPhsvOA)
  - [Kubernetes 架构核心点详细总结！](https://mp.weixin.qq.com/s/JpvlPBazyvy41AyX-RPwvQ)
  - [【云原生】一文细数kubernetes常见20道问题](https://mp.weixin.qq.com/s/n3QYIGuM1io1ubE3KC1hrw)
- 知乎文章
  - [一关系图让你理解K8s中的概念，Pod、Service、Job等到底有啥关系](https://zhuanlan.zhihu.com/p/105006577?utm_medium=social&utm_oi=56834706636800&utm_psn=1578874624045264896&utm_source=wechat_session)
  - [Kubernets原理的分解讲解](https://zhuanlan.zhihu.com/p/500443105?utm_medium=social&utm_oi=56834706636800&utm_psn=1578889599430103040&utm_source=wechat_session)
  - [主流 Kubernetes 发行版梳理，看完就会选了](https://zhuanlan.zhihu.com/p/56031304?utm_medium=social&utm_oi=56834706636800&utm_psn=1578890535669833728&utm_source=wechat_session)
  - [想学习云原生/云原生边缘计算相关技术，需要哪些计算机基础知识？](https://www.zhihu.com/question/434475807/answer/2409751479?utm_campaign=shareopn&utm_content=group2_Answer&utm_medium=social&utm_oi=56834706636800&utm_psn=1578891774508052480&utm_source=wechat_session)

### kubectl context

> 注：所谓 kubectl context，就是用来告诉kubectl 命令“去连接哪个集群”的一系列配置。
> A kubectl context contains connection information to a Kubernetes cluster. Different kubectl contexts can connect to different Kubernetes clusters, or to the same cluster but using different users or different default namespaces.

## K8s书籍

- 英文名：《Docker Deep Dive》中文名：《深入浅出Docker》（很薄, 深入浅出)
- 英文名：《The Kubernetes book》中文名：《Kubernetes修炼手册》 （很薄，适合初学者快速了解基本概念）
- 《Kubernetes in Action》 （厚度合适，比第一本更详细一些）
- 《CKA/CKAD 应试指南》 （适合考试辅助）
- 《Kubernetes权威指南》 （这本太厚，不推荐第一次学习看，适合当字典翻阅）

## K8s课程

> - If you are touching Kubernetes for the first time, start with this Mumshad Mannambeth Udemy course with practical labs https://www.udemy.com/course/learn-kubernetes
> - If you are familiar with Kubernetes: this Udemy course from Mumshad Mannambeth will be your best friend: https://www.udemy.com/course/certified-kubernetes-application-developer/
> This course contains: 26 practical labs, 2 lightings labs, 6 mini-mock and 2 mock exams. And are all with the solution in videos.

### Oreilly视频课程

- [CKA和CKAD](https://learning.oreilly.com/beta-search/?q=ckad%20sander%20van%20vugt&type=*&publishers=Pearson&order_by=relevance)
  - [Certified Kubernetes Administrator (CKA) Crash Course](https://learning.oreilly.com/live-events/certified-kubernetes-administrator-cka-crash-course/0636920315766/)
    - 附带练习环境Practice: [Certified Kubernetes - CKA Labs](https://learning.oreilly.com/playlists/d6e3fe86-067c-4dc7-a36d-698802d0bdee/)
  - [Certified Kubernetes Application Developer (CKAD) Crash Course](https://learning.oreilly.com/live-events/certified-kubernetes-application-developer-ckad-crash-course/0636920315803/)
    - 附带练习环境Practice: [Certified Kubernetes - CKAD Labs](https://learning.oreilly.com/playlists/ea6ea0fc-d8e2-422c-94dd-a0a8f608d224/)

可以配置成Oreilly课程对应的lab环境：
> To work through the labs in this course, you will need to install and configure your own lab environment.
> 
> Different lab installation options are possible, but it is recommended to use `Minikube`, on a virtual machine that runs the latest version of Ubuntu LTS desktop.

Prepare the `Minikube` based lab setup before start of the course can follow the instructions that are provided in the **"Setup Guide"** in the course [CKAD GitHub repository](https://github.com/sandervanvugt/ckad/blob/master/SetupGuide.pdf), [CKA GitHub repository](https://github.com/sandervanvugt/cka)

# k8s安装部署

部署方式 | 类型 | 作用 | 环境需求
---------|----------|---------|---------
 Minikube | 工具 | 快速搭建一个`单节点`的K8s，仅用于尝试Kubernetes或日常开发的用户使用。[部署地址](https://kubernetes.io/docs/tasks/tools/#minikube). 参考另一篇博客[Minikube安装-MacOS M1](./Minikube%E5%AE%89%E8%A3%85-MacOS-M1.html) | 环境：centos 7.4 +<br/>硬件需求：CPU>=2c ,内存>=2G
 kubeadm | 工具【官方推荐】 | kubeadm init和kubeadm join，用于快速部署K8s集群。[部署地址](https://kubernetes.io/docs/reference/setup-tools/kubeadm/). 参考文章：1[使用kubeadm快速部署一套K8S集群](https://zhuanlan.zhihu.com/p/445917469?utm_medium=social&utm_oi=56834706636800&utm_psn=1578882975642624000&utm_source=wechat_session) 2 [Kubernetes集群部署-01](https://zhuanlan.zhihu.com/p/403821493?utm_medium=social&utm_oi=56834706636800&utm_psn=1578893327369469952&utm_source=wechat_session)
 官方下载发行版的二进制包 | 二进制包【建议生产环境使用】 | 手动部署每个组件，组成Kubernetes集群。[下载地址](https://github.com/kubernetes/kubernetes/releases)
 虚拟机提供商 |Google Compute Engine、Amazon EC2、Microsoft Azure等||
 kops | 是用于在 AWS 上安装 Kubernetes 的一个“武断”（opinionated）的工具，所谓 “武断”，是说在用它安装的时候没有太多可定制的空间。如果需要一个高度可定制化的集群，建议使用 kubeadm。[Installing Kubernetes with kOps](https://kubernetes.io/docs/setup/production-environment/tools/kops/)

## k8s练习环境(非生产环境)

### [Play with Kubernetes（PWK）](https://labs.play-with-k8s.com/)

需要使用一个 GitFub 或 Docker Fub 账号完成登录，并完成一些简单的操作来搭建一个持续4h的集群。不太稳定，有时会报错。
[PWK部署k8s集群](./Kubernetes-Play-with-Kubernetes(PWK).html)

### 桌面版Docker

是一个来自Docker 公司的免费桌面应用，只需要下载并运行安装程序。桌面版 Docker 是在自己的 macos 或 Windows 中部署本地开发环境的最佳方式。只需几个步骤就可以轻松地部署一个用于开发和测试的**单节点**的 Kubernetes 集群。

桌面版Docker通过创建一个虚拟机，然后在虚拟机中启动一个单节点的Kubernehs集群来实现。同时它还会完成 kubectl 容户端的配置，以便连接集群。最后，还有一个简单的图形界面用来执行诸如切换 kubectl context 的基本操作。

1. 打开 Docker 主页，选择 Products ＞ 桌面版 Docker。
2. 单击macOs 或 Windows 对应的下载按钮，
可能需要登录 Docker Store，账号和桌面版Docker 软件一样都是免费的。
3. 打开下载的安装程序，并按步骤安装。
安装完成后，会有一个鲸鱼因标出现在 Windows 任务栏或 macos 的菜单栏中，
4. 单击鲸鱼图标（可能需要右击），进人设置界面，然后在 Kubernetes 页签中启用Kubernetes

此时可以打开终端查看集群信息。

```
$ kubectl get nodes
```

现在已经有一个本地的Kubernetes 集群了。

### Magic Sandbox

只需要注册一个账号并登录，即可马上得到一个完整可用的多节点私有集群。其中还有一些内置课程和上手实验。

### 在线环境-killercoda(考试练习推荐)

- CKA在线练习环境：https://killercoda.com/killer-shell-cka
- CKAD在线练习环境：https://killercoda.com/killer-shell-ckad
- CKS在线练习环境：https://killercoda.com/killer-shell-cks

- 临时考试模拟环境（1小时有效期）：https://killercoda.com/kimwuestkamp/scenario/cks-cka-ckad-remote-desktop

- 模拟考试环境： https://killer.sh/ 包含CKA,CKAD,CKS （需付费，官方考试已包含两次session，每个session 36个小时有效期）
  - 模拟考题：[CKA Simulator Kubernetes 1.24](https://killer.sh/attendee/f8c336a9-658e-4342-a59e-13850ff20813/content)
  - [CKA Simulator Preview Kubernetes 1.25](https://killer.sh/course/preview/e84d0e31-4fff-4c42-8afd-be1bdbc0d994)
  - [CKAD Simulator Preview Kubernetes 1.25](https://killer.sh/course/preview/052229bd-1062-44a4-8aae-f50d0770165a)
  - [CKS Simulator Preview Kubernetes 1.25](https://killer.sh/course/preview/bf573045-49c8-44c3-b2e5-8eec7b8eaab3)

### 在线环境-Oreilly

需购买课程, 或配置本地环境
- [Certified Kubernetes - CKA Labs](https://learning.oreilly.com/playlists/d6e3fe86-067c-4dc7-a36d-698802d0bdee/)
- [Certified Kubernetes - CKAD Labs](https://learning.oreilly.com/playlists/ea6ea0fc-d8e2-422c-94dd-a0a8f608d224/)

## 托管的Kubernetes集群

- AWS: Elastic Kubernetes Service (EKS).
- Microsoft Azure: Azure Kubernetes Service ( AKS).
- DigitalOcean: DigitalOcean Kubernetes.
- IBM Cloud: IBM Cloud Kubernetes Service.
- Google Cloud Platform: Google Kubernetes Engine ( GKE ).

> 大多数的主流云平台提供托管的 Kubernetes （hosted Kubernetes）服务。采用这种方式，控制平面（control plane， 即master）的相关组件是由云平台管理的。
> 
> 例如，云服务供应南会确保控制平面的高可用和高性能，并负责使控制平面保持更新。另外，用户失去对版本的部分控制，定制化的能力也会受到限制。
> 
> 抛开优缺点不谈，托管的Kubernetes 服务是最开箱即用的生产级别的Kubemetes了。事实上，Google Kubernetes 引擎GKE可以让用户在几个简单的单击之后就能完成生产级别的Kubernetes 集群和 Istio 服务网格（ Service Mesh）的部署。其他云厂商也有类似的服务。
> 
> 在考虑选择以上某项服务来搭建自己的Kubernetes 集群时，尝试问自己：自行搭建和管理 Kubernetes 集群能否实现时问和其他资源的最大化利用？如果答案不是“当然是”，那么我强烈建议考虑托管的服务。

### 使用Google Kubernetes Engine托管Kubernetes集群

如果你想探索一个完善的多节点Kubernetes集群，可以使用托管的Google Kubernetes Engine（GKE）集群。这样，无须手动设置所有的集群节点和网络，因为这对于刚开始使用Kubernetes的人来说太复杂了。使用例如GKE这样的托管解决方案可以确保不会出现配置错误、不工作或部分工作的集群。

#### 配置一个Google Cloud项目并且下载必需的客户端二进制

在设置新的Kubernetes集群之前，需要设置GKE环境。因为这个过程可能会改变，所以不在这里列出具体的说明。阅读https://cloud.google.com/containerengine/docs/before-begin中的说明后就可以开始了。

整个过程大致包括：

1. 注册谷歌账户，如果你还没有注册过。
2. 在Google Cloud Platform控制台中创建一个项目。
3. 开启账单。这会需要你的信用卡信息，但是谷歌提供了为期12个月的免费试用。而且在免费试用结束后不会自动续费。
4. 开启Kubernetes Engine API。
5. 下载安装Google Cloud SDK（这包含 gcloud 命令行工具，需要创建一个Kubernetes集群）。
6. 使用 gcloud components install kubectl 安装 kubectl 命令行工具。

注意 某些操作（例如步骤2中的操作）可能需要几分钟才能完成。

#### 创建一个三节点Kubernetes集群

完成安装后，可以使用下面代码清单中的命令创建一个包含三个工作节点的Kubernetes集群。

#### 在GKE上创建一个三节点集群

```bash
$ gcloud container clusters create kubia --num-nodes 3 --machine-tvpe fl-micro
Creating cluster kubia... done
Created [https://container.googleapis.com/y1/proiects/kubial-1227/zones/europe-west1-d/clusters/kubia]
kubeconfig entry generated for kubia.
NAME ZONE MST VER MASTER IP  TYPE NODE VER NUM NODES STATUSkubia eu-wld 1.5.3 104.155.92.30 fl-micro 1.5.3:  RUNNING
```

现在已经有一个正在运行的Kubernetes集群，包含了三个工作节点。你在使用三个节点来更好地演示适用于多节点的特性，如果需要的话可以使用较少数量的节点。

# K8s Certificate 考试认证

- KCNA
  - [KCNA考试只有选择题](https://training.linuxfoundation.org/certification/kubernetes-cloud-native-associate/)
- [CKA (Certified Kubernetes Administrator)考试指南](./Kubernates-Certified-Kubernetes-Administrator-CKA.html)
  - [CKA机试 - 实战](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/)
  - CKA is intended for `DeVops, Engineers and Cloud Architects` and Architects. CKA certification is much more difficult than CKAD.
- [CKAD(Certified Kubernetes Application Developer)考试指南](./Kubernates-Certified-Kubernetes-Application-Developer-CKAD.html)
  - [CKAD机试 - 实战](https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/)
  - 适合开发人员。CKAD is intended for `developers` who will use Kubernetes as an orchestrator in their development projects and cloud engineers.
- CKS (Certified Kubernetes Security Specialist)
  - [CKS机试 - 实战](https://training.linuxfoundation.org/certification/certified-kubernetes-security-specialist/#)
  - 安全专家。CKS is intended for `security` experts, DevOps experts, Cloud Architects, Security Architects. CKS is a very difficult certification, and it takes a lot of time to be prepared.

## 参考文章

- [How I got CKAD Certification (2021) in 3 Weeks](https://www.linkedin.com/pulse/how-i-got-ckad-certification-2021-3-weeks-abdelahad-satour/)