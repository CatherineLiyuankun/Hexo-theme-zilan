---
title: 2023 CKS 考试真题整理
catalog: true
date: 2022-12-25 22:52:43
subtitle: Certified Kubernetes Security Specialist
header-img:
tags: 
- Cloud
- container
categories:
- TECH
- container
- Kubernetes
---

上一篇：[CKA考试真题](./Kubernates-Certified-Kubernetes-Administrator-CKA.html)
上一篇：[CKAD考试真题](./Kubernates-Certified-Kubernetes-Application-Developer-CKAD.html)

## 考试内容

[CKA 考试链接](https://training.linuxfoundation.org/certification/certified-kubernetes-security-specialist/#)

- 考试包括 15-20 项performance-based tasks。
  - 2023.1 实测是16道题
- 考生有 2 小时的时间完成 CKS 考试。
  - 因为从06/2022开始环境升级（贬义），考试环境更难用了，变的很卡，所以时间变得比较紧张。容易做不完题，建议先把有把握的，花费时间不多的题先做掉
    - [CKS CKA CKAD changed Terminal to Remote Desktop ](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e)
- CKS考试66分以上即可通过，考试不通过有一次补考机会。

### More items for CKS than CKA and CKAD

- Secret
- ...

## 如何备考

### [k8s练习环境](./Kubernates-Certified-Kubernetes-Administrator-CKA.html#k8s%E7%BB%83%E4%B9%A0%E7%8E%AF%E5%A2%83)(同CKA)

### CKS练习题

有几个练习库，建议将每个题目都自己亲自操作一遍，一定要操作。

- CKS在线练习环境：https://killercoda.com/killer-shell-cks

### CKS课程

- 【需付费】CKS考试-对应官方课程[Kubernetes for Developers (LFS260)](https://training.linuxfoundation.org/training/kubernetes-security-essentials-lfs260/) 感觉没必要买，只看官方文档就足够了。

### 常用命令

```bash
# 不熟
## 输出pod status
kubectl -n default describe pod pod1 | grep -i status:
kubectl -n default get pod pod1 -o jsonpath="{.status.phase}"
## Check the pod for error
kubectl describe pod podname | grep -i error
... Error: ImagePullBackOff
## a fast way to get an overview of the ReplicaSets of a Deployment and their images could be done with:
kubectl -n neptune get rs -o wide | grep deployname
NAME         DESIRED   CURRENT   READY   AGE    CONTAINERS   IMAGES         SELECTOR
deployname   3         3         3       9m6s   httpd        httpd:alpine   app=wonderful

## 创建job
kubectl -n neptune create job neb-new-job --image=busybox:1.31.0 $do > /opt/course/3/job.yaml -- sh -c "sleep 2 && echo done"
## If a Secret bolongs to a serviceaccount, it'll have the annotation kubernetes.io/service-account.name
kubectl get secrets -oyaml | grep annotations -A 1 # shows secrets with first annotation
## log
kubectl logs podname > /opt/test.log
## decode base64
base64 -d filename
## check service connection using a temporary Pod
## k run tmp --restart=Never --rm --image=nginx:alpine -i -- curl http://svcname.namespace:svcport
kubectl run tmp --restart=Never --rm --image=nginx:alpine -i -- curl http://svcname.namespace:80
## check that both PV and PVC have the status Bound:
k -n earth get pv,pvc
NAME                                            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                                 STORAGECLASS   REASON   AGE
persistentvolume/earth-project-earthflower-pv   2Gi        RWO            Retain           Bound    earth/earth-project-earthflower-pvc                           8m4s

NAME                                                  STATUS   VOLUME                         CAPACITY   ACCESS MODES   STORAGECLASS   AGE
persistentvolumeclaim/earth-project-earthflower-pvc   Bound    earth-project-earthflower-pv   2Gi        RWO                           7m38s

## We can confirm the pod of deployment with PVC mounting correctly:
k describe pod project-earthflower-586758cc49-hb87f -n earth | grep -A2 Mount:
    Mounts:
      /tmp/project-data from task-pv-storage (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-jj2t2 (ro)

## Verify everything using kubectl auth can-i
kubectl auth can-i create deployments --as system:serviceaccount:app-team1:cicd-token -n app-team1 # YES
```

```bash
# 常用
## 创建pod
kubectl run pod1 --image=httpd:2.4.41-alpine $do > 2.yaml
kubectl get pod sat-003 -o yaml > 7-sat-003.yaml # export
kubectl delete pod pod1 --force --grace-period=0
## 创建service
kubectl expose deployment d1 --name=服务名 --port=服务端口 --target-port=pod运行端口 --type=类型
kubectl expose pod pod名 --name=服务名 --port=服务端口 --target-port=pod运行端口 --type=类型
## 创建secret
kubectl create secret generic db-credentials --from-literal db-password=passwd
## modify a pod yaml to deployment yaml
### put the Pod's metadata: and spec: into the Deployment's template: section:

```

## [经验总结](http://liyuankun.top/Kubernates-Certified-Kubernetes-Administrator-CKA.html#%E7%BB%8F%E9%AA%8C%E6%80%BB%E7%BB%93)(同CKA)

## [Pre Setup](http://liyuankun.top/Kubernates-Certified-Kubernetes-Administrator-CKA.html#pre-setup)(同CKA)

## CKS 2021 真题 1.20

### 考题1 - Creating a Pod and Inspecting it


### 考题2 - Configuring a Pod to Use a ConfigMap

### 考题3 - Configuring a Pod to Use a Secret



### 考题4 - Creating a Security Context for a Pod



### 考题5 - Defining a Pod’s Resource Requirements



### 考题6 - 

### 考题7 - 

### 考题8 - 

### 考题9 - 

### 考题10 - 

### 考题11 - 

### 考题12 - 

### 考题13 - 

### 考题14 - 

### 考题15 - 

### 考题16 - 

### 考题17 - 

## 参考文章

- CKS 真题
  - [2022年11月最新CKS认证题库](https://huaweicloud.csdn.net/638db1b2dacf622b8df8c678.html)
  - [2022.10 CKS考试题库v1.24](https://huaweicloud.csdn.net/638db1a8dacf622b8df8c643.html?spm=1001.2101.3001.6650.5&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Eactivity-5-126962402-blog-123994683.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Eactivity-5-126962402-blog-123994683.pc_relevant_default&utm_relevant_index=6)
  - [2022.10 CKS 1.24真题解析](https://huaweicloud.csdn.net/638db200dacf622b8df8c7f0.html?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EYuanLiJiHua%7Eactivity-3-127131284-blog-123994683.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EYuanLiJiHua%7Eactivity-3-127131284-blog-123994683.pc_relevant_default&utm_relevant_index=4)
  - [2022.8 kubernets CKS内容及题库](https://blog.csdn.net/cloud_engineer/article/details/125709403?spm=1001.2101.3001.6650.7&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-7-125709403-blog-123994683.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-7-125709403-blog-123994683.pc_relevant_default&utm_relevant_index=8)
  - [2022.6 CKS认证考题+解析](https://blog.csdn.net/zfw_666666/article/details/125185751)
  - [2022.3 CKS 1.23 真题](https://blog.csdn.net/april_4?type=blog)
  - [2022.1 cks 试题](https://huaweicloud.csdn.net/63311d5fd3efff3090b52a1e.html?spm=1001.2101.3001.6650.9&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Eactivity-9-122525427-blog-123994683.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Eactivity-9-122525427-blog-123994683.pc_relevant_default&utm_relevant_index=10)
  - [2021.12 Kubernetes CKS 1.20 - 真题 15道题](https://huaweicloud.csdn.net/638db4efdacf622b8df8cc95.html)
  - [2021 Kubernetes CKS 1.20 - 真题 15道题](https://blog.csdn.net/itsaka/category_11111851.html)
- CKS其他
  - [CKS考试知识点链接](https://blog.csdn.net/u011127242/article/details/125822057)
