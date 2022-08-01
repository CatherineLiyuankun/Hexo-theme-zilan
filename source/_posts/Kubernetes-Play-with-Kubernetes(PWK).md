---
title: Kubernetes - Play with Kubernetes（PWK）
catalog: true
date: 2022-03-05 22:30:33
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

## [Play with Kubernetes（PWK）](https://labs.play-with-k8s.com/)

### 1 浏览器进入官网[Play with Kubernetes](https://labs.play-with-k8s.com/)

### 2 点击“Sign in”， 使用GitHub或者Docker Hub 账号登陆，点击“Start”

### 3 左侧导航栏 点击“ADD NEW INSTANCE”

右侧出现控制台窗口。这是一个Kubernetes节点（node1）

### 4 执行命令查看节点上预装组件

```bash
$ docker version


$ kubectl version --output=yaml

$ whoami
root

```

### 5  `kubeadm init` 初始化一个新的集群

```bash
 1. Initializes cluster master node:

 kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr 10.5.0.0/16
    
Your Kubernetes control-plane has initialized successfully!
To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.0.23:6443 --token 221f6u.1r9leb1snw0fngbo \
    --discovery-token-ca-cert-hash sha256:dc7108dbbe961ecddada53f6597459e7bbccd046dc60900330d24ee94dbcb216 
Waiting for api server to startup
Warning: resource daemonsets/kube-proxy is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
daemonset.apps/kube-proxy configured

```

### 6  `kubectl get nodes` 查看集群信息

```bash
[node1 ~]$ kubectl get nodes
NAME    STATUS     ROLES                  AGE    VERSION
node1   NotReady   control-plane,master   111s   v1.20.1
```

节点状态`NotReady`是由于尚未配置Pod网络。

### 7 初始化Pod网络（集群网络）


```bash
2. Initialize cluster networking:

kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml

configmap/kube-router-cfg created
daemonset.apps/kube-router created
serviceaccount/kube-router created
clusterrole.rbac.authorization.k8s.io/kube-router created
clusterrolebinding.rbac.authorization.k8s.io/kube-router created

```

### 8  `kubectl get nodes` 查看集群信息

```bash
[node1 ~]$ kubectl get nodes
NAME    STATUS   ROLES                  AGE   VERSION
node1   Ready    control-plane,master   27m   v1.20.1

```

节点状态`Ready`
Pod网络已经初始化，控制层也已经Ready。

### 9 复制`kuberadm init`执行后打印出的`kuberadm join`命令

```bash
# 先复制好，但不执行
kubeadm join 192.168.0.23:6443 --token 221f6u.1r9leb1snw0fngbo \
    --discovery-token-ca-cert-hash sha256:dc7108dbbe961ecddada53f6597459e7bbccd046dc60900330d24ee94dbcb216
```

如果忘记保存此命令，可用如下命令获取：

```bash
kubeadm token create --print-join-command
```

### 10 左侧导航栏 点击“ADD NEW INSTANCE”

得到新节点node2

### 11 在node2控制台中执行9的`kuberadm join`命令

```bash
[node2 ~]$ kubeadm join 192.168.0.23:6443 --token 221f6u.1r9leb1snw0fngbo \
>     --discovery-token-ca-cert-hash sha256:dc7108dbbe961ecddada53f6597459e7bbccd046dc60900330d24ee94dbcb216

...
This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the control-plane to see this node join the cluster.
```

### 12 在node1控制台中执行 `kubectl get nodes`命令

```bash
[node1 ~]$ kubectl get nodes
NAME    STATUS   ROLES                  AGE     VERSION
node1   Ready    control-plane,master   41m     v1.20.1
node2   Ready    <none>                 2m13s   v1.20.1
```

node1为主节点（PWK页面蓝色图标），node2为工作节点（PWK页面灰色图标）。

### 查看kubectl配置

```bash
[node1 ~]$ kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://192.168.0.23:6443
  name: kubernetes
contexts:
- context:
    cluster: kubernetes
    user: kubernetes-admin
  name: kubernetes-admin@kubernetes
current-context: kubernetes-admin@kubernetes
kind: Config
preferences: {}
users:
- name: kubernetes-admin
  user:
    client-certificate-data: REDACTED
    client-key-data: REDACTED
```

### 查看当前使用的context

```bash
[node1 ~]$ kubectl config current-context
kubernetes-admin@kubernetes
```

### 改变当前使用的context

```bash
$ kubectl config use-context contextName
```

```bash

```


```bash
 1. (Optional) Create an nginx deployment:

 kubectl apply -f <https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/application/nginx-app.yaml>

```

## 安装后设置

### 设置使用Tab键

编辑/etc/profile, 在第二行加上source <(kubectl completion bash)

- 要让此设置生效，操作系统要安装bash-completion
- 注意小括号为英文版

```bash
$ head -3 /etc/profile
# /etc/profile
source <(kubectl completion bash) # 新增<与(中间没有空格

$ source /etc/profile
```

### 设置vim

创建/root/.vimrc

```bash
$ cat .vimrc
set paste
```

## 设置metric-server监控pod及node负载

### 安装metric-server

1. 所有node上下载镜像

```bash
$ docker pull mirrorgooglecontainers/metrics-server-amd64:v0.3.6
```

2. 所有node上tag操作，形成一个新镜像

```bash
$ docker tag mirrorgooglecontainers/metrics-server-amd64:v0.3.6 k8s.gcr.io/metrics-server-amd64:v0.3.6
```

3. master上下载metrics-server

```bash
$ curl -Ls https://api.github.com/repos/kubernetes-sigs/metrics-server/tarball/v0.3.6 -o metrics-server-v0.3.6.tar.gz
```

4. 解压`metrics-server-v0.3.6.tar.gz`, 进入目录 `/root/kubernetes-sigs-metrics-server-d1f4f6f/deploy/1.8+`

5. 修改metrics-server-deployment.yaml
6. 运行当前目录所有文件


```bash
$ kubectl apply -f .
```

### 查看负载

查看节点负载

```bash
$ kubectl top nodes --use-protocol-buffers
```

查看pod负载

```bash
$ kubectl top pods -n kube-system --use-protocol-buffers
```