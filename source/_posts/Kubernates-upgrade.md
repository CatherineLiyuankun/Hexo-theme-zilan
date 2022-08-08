---
title: Kubernates-upgrade
catalog: true
date: 2022-08-02 22:42:44
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

## 确定要升级到哪个版本

使用操作系统的包管理器找到最新的补丁版本 Kubernetes 1.24：

### Ubuntu、Debian 或 HypriotOS

```bash
apt update
apt-cache madison kubeadm
# 在列表中查找最新的 1.24 版本
# 它看起来应该是 1.24.x-00，其中 x 是最新的补丁版本
```

### CentOS、RHEL 或 Fedora

```bash
yum list --showduplicates kubeadm --disableexcludes=kubernetes
# 在列表中查找最新的 1.24 版本
# 它看起来应该是 1.24.x-0，其中 x 是最新的补丁版本
# 参考文章
```

## 升级master

控制面节点上的升级过程应该每次处理一个节点。 首先选择一个要先行升级的控制面节点。该节点上必须拥有 /etc/kubernetes/admin.conf 文件。

### kubeadm upgrade

#### 对于第一个控制面节点

##### Step 1 升级 kubeadm

Ubuntu、Debian 或 HypriotOS

```bash
# 用最新的补丁版本号替换 1.24.x-00 中的 x
apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.24.x-00 && \
apt-mark hold kubeadm
```

CentOS、RHEL 或 Fedora

```bash
# 用最新的补丁版本号替换 1.24.x-0 中的 x
yum install -y kubeadm-1.24.x-0 --disableexcludes=kubernetes
```

##### Step 2 `kubeadm version`

验证下载操作正常，并且 kubeadm 版本正确：

```bash
kubeadm version
```

##### Step 3 验证升级计划

```bash
kubeadm upgrade plan
```

##### Step 4 `kubeadm upgrade apply`

选择要升级到的目标版本，运行合适的命令。

```bash
# 将 x 替换为你为此次升级所选择的补丁版本号
sudo kubeadm upgrade apply v1.24.x
```

#### 对于其它控制面节点

与第一个控制面节点相同，但是使用：

```bash
sudo kubeadm upgrade node
```

而不是：

```bash
sudo kubeadm upgrade apply
```

此外，不需要执行 kubeadm upgrade plan 和更新 CNI 驱动插件的操作。

### 腾空节点

- 通过将节点标记为不可调度并腾空节点为节点作升级准备：

```bash
# 将 <node-to-drain> 替换为你要腾空的控制面节点名称
kubectl drain <node-to-drain> --ignore-daemonsets
```

### 升级 kubelet 和 kubectl

- 升级 kubelet 和 kubectl：

CentOS、RHEL 或 Fedora

```bash
# 用最新的补丁版本替换 1.24.x-00 中的 x
apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.24.x-00 kubectl=1.24.x-00 && \
apt-mark hold kubelet kubectl
```

Ubuntu、Debian 或 HypriotOS

```bash
# 用最新的补丁版本号替换 1.24.x-00 中的 x
yum install -y kubelet-1.24.x-0 kubectl-1.24.x-0 --disableexcludes=kubernetes
```

- 重启 kubelet：

```bash
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

### 解除节点的保护

通过将节点标记为可调度，让其重新上线：

```bash
# 将 <node-to-drain> 替换为你的节点名称
kubectl uncordon <node-to-drain>
```

# 参考文章

- [kubernetes-upgrade kubeadm](https://kubernetes.io/zh-cn/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)