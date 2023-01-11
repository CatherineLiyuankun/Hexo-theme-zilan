---
title: 2022 CKAD K8s v1.25 考试真题整理
catalog: true
date: 2022-08-02 22:52:43
subtitle: Kubernates-Certified Kubernetes Application Developer
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

## 考试内容

[Important Instructions: CKA and CKAD](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad)

- 考试包括 15-20 项performance-based tasks。
  - 2022.12 实测是16道题
- 考生有 2 小时的时间完成 CKA 和 CKAD 考试。
  - 因为从06/2022开始环境升级（贬义），考试环境更难用了，变的很卡，所以时间变得比较紧张。容易做不完题，建议先把有把握的，花费时间不多的题先做掉
    - [CKS CKA CKAD changed Terminal to Remote Desktop ](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e)
- CKAD考试66分以上即可通过，考试不通过有一次补考机会。

![CKA](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKA/CKA_exam_syllabus.png)
![CKAD](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKA/CKAD_exam_syllabus.png)

You're only allowed to have one other browser tab open with:

- https://kubernetes.io/docs
- https://kubernetes.io/blog
- https://helm.sh/docs

### More items for CKAD than CKA

- Define, build and modify container images, `Dockerfile`
- Understand multi-container Pod design patterns (init containers)
- Understand `Jobs` and `CronJobs`
- Implement `probes` and health checks
- Understand [`SecurityContexts`](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)
- [`canary deployment`](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#canary-deployments)
  - [考题10 - 2022 Rollout Canary](./Kubernates-Certified-Kubernetes-Application-Developer-CKAD.html#%E8%80%83%E9%A2%9810-2022-rollout-canary)
- `ResourceQuota`

## 如何备考

### [k8s练习环境](./Kubernates-Certified-Kubernetes-Administrator-CKA.html#k8s%E7%BB%83%E4%B9%A0%E7%8E%AF%E5%A2%83)(同CKA)

### CKAD练习题

有几个练习库，建议将每个题目都自己亲自操作一遍，一定要操作。

- CKAD在线练习环境：https://killercoda.com/killer-shell-ckad
- [Git - StenlyTU - K8s Practice Training for CKA, CKAD and CKS](https://github.com/StenlyTU/K8s-training-official)
- [bbachi/CKAD-Practice-Questions](https://github.com/bbachi/CKAD-Practice-Questions)
  - 对应博客[2019.11 Practice Enough With These 150 Questions for the CKAD Exam](https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552)
    <!-- - [CKAD考试真题-练习题150道](https://www.cnblogs.com/peteremperor/p/12785335.html) 同第一个链接一样 -->
    - 同第一个链接一样，中文版 [2020 CKAD 考试习题练习104道](https://blog.csdn.net/tanjunchen/article/details/104865939?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166039499316782248541148%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166039499316782248541148&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-104865939-null-null.142^v40^pc_search_integral,185^v2^control&utm_term=CKAD%E8%80%83%E8%AF%95%E9%A2%98&spm=1018.2226.3001.4187)
- [dgkanatsios/CKAD-exercises](https://github.com/dgkanatsios/CKAD-exercises)
- Oreilly视频课程-附带练习环境（链接已失效Katacoda has ended public service）： https://www.katacoda.com/liptanbiswas/courses/ckad-practice-challenges


题库里面题目是更简单一些，真的考题会是这些练习题的组合，把里面的题目都能熟练操作，就差不多了。

### CKAD课程

- 【需付费】CKAD考试-对应官方课程[Kubernetes for Developers (LFD259)](https://training.linuxfoundation.org/training/kubernetes-for-developers/)
- 【需付费】Udemy CKAD 课程
  - [Certified Kubernetes Application Developer (CKAD)](https://www.techbeatly.com/kk-ckad) – by Mumshad Mannambeth
  - [Kubernetes Certified Application Developer (CKAD) with Tests](https://www.techbeatly.com/kk-ckad-ud) – by Mumshad Mannambeth – Udemy
- 【需付费】Oreilly视频课程: (For beginner or Advanced) [Certified Kubernetes Application Developer (CKAD) Sander van Vugt](https://learning.oreilly.com/videos/certified-kubernetes-application/9780137841509/).
  - [Certified Kubernetes Application Developer (CKAD) Crash Course](https://learning.oreilly.com/live-events/certified-kubernetes-application-developer-ckad-crash-course/0636920315803/)
    - 附带练习环境Practice: [Certified Kubernetes - CKAD Labs](https://learning.oreilly.com/playlists/ea6ea0fc-d8e2-422c-94dd-a0a8f608d224/)

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
➜ k -n mercury logs cleaner-576967576c-cqtgx --container logger-con

## decode base64
base64 -d filename
echo "YWRtaW4=" | base64 -d
admins$

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

## 查看某个namespace的resource quota
$ kubectl describe quota --namespace=rq-demo
## 或者
$ kubectl describe resourcequotas -n rq-demo

## rollout
k -n mercury rollout history deploy cleaner --revision 1

```


```bash
# 常用
## 创建pod
kubectl run pod1 --image=httpd:2.4.41-alpine $do --port=80 > 2.yaml
kubectl get pod sat-003 -o yaml > 7-sat-003.yaml # export
kubectl delete pod pod1 --force --grace-period=0
## 创建service
kubectl expose deployment d1 --name=服务名 --port=服务端口 --target-port=pod运行端口 --type=类型 --protocol=TCP
kubectl expose pod pod名 --name=服务名 --port=服务端口 --target-port=pod运行端口 --type=类型
## 创建secret
kubectl create secret generic db-credentials --from-literal db-password=passwd
## modify a pod yaml to deployment yaml
### put the Pod's metadata: and spec: into the Deployment's template: section:

## Ingress
# 1 注意namespace
# spec:
  # ingressClassName: nginx   # 2 ingressClassName

# metadata:
  # name: minimal-ingress
  # annotations:
  #   nginx.ingress.kubernetes.io/rewrite-target: /   #3 annotation

## NetworkPolicy
注意 
  egress:
    - to:
        - ipBlock:
            cidr: 10.0.0.0/24
      ports:                   # &
        - protocol: TCP
          port: 5978

  egress:
    - to:
        - ipBlock:
            cidr: 10.0.0.0/24
    - ports:                  # ||
        - protocol: TCP
          port: 5978
```

## [经验总结](http://liyuankun.top/Kubernates-Certified-Kubernetes-Administrator-CKA.html#%E7%BB%8F%E9%AA%8C%E6%80%BB%E7%BB%93)(同CKA)

## [Pre Setup](http://liyuankun.top/Kubernates-Certified-Kubernetes-Administrator-CKA.html#pre-setup)(同CKA)

## CKAD 真题

2021 年的考题，基于k8s 1.20
2022.12 的考题，基于k8s 1.25

### 2021考题1 - Creating a Pod and Inspecting it

1. Create the namespace ckad-prep.
2. In the namespace ckad-prep create a new Pod named mypod with the image nginx:2.3.5. Expose the port 80.
3. Identify the issue with creating the container. Write down the root cause of issue in a file named pod-error.txt.
4. Change the image of the Pod to nginx:1.15.12.
5. List the Pod and ensure that the container is running.
6. Log into the container and run the ls command. Write down the output. Log out of the container.
7. Retrieve the IP address of the Pod mypod.
8. Run a temporary Pod using the image busybox, shell into it and run a wget command against the nginx Pod using port 80.
9. Render the logs of Pod mypod.
10. Delete the Pod and the namespace.

```bash
# 1. create the namespace.
$ kubectl create ns ckad-prep

# 2. create a new Pod
$ kubectl run mypod -n ckad-prep --image=nginx:2.3.5 --port=80 
# 或者：
# $ kubectl run mypod --namespace=ckad-prep --image=nginx:2.3.5 --port=80 
pod/mypod created
```

```bash
# 3. Write down root cause in pod-error.txt
$ kubectl get pod -n ckad-prep
NAME    READY   STATUS             RESTARTS   AGE
mypod   0/1     ImagePullBackOff   0          1m

$ kubectl describe pod mypod -n ckad-prep
...
Events:
  Type     Reason     Age                  From               Message
  ----     ------     ----                 ----               -------
  Normal   Scheduled  12m                  default-scheduler  Successfully assigned ckad-prep/mypod to controlplane
  Normal   Pulling    10m (x4 over 12m)    kubelet            Pulling image "nginx:2.3.5"
  Warning  Failed     10m (x4 over 12m)    kubelet            Failed to pull image "nginx:2.3.5": rpc error: code = NotFound desc = failed to pull and unpack image "docker.io/library/nginx:2.3.5": failed to resolve reference "docker.io/library/nginx:2.3.5": docker.io/library/nginx:2.3.5: not found
  Warning  Failed     10m (x4 over 12m)    kubelet            Error: ErrImagePull
  Warning  Failed     10m (x6 over 12m)    kubelet            Error: ImagePullBackOff
  Normal   BackOff    2m9s (x41 over 12m)  kubelet            Back-off pulling image "nginx:2.3.5"

# 或者
$ kubectl describe pod mypod -n ckad-prep | grep err -i
      Reason:       ErrImagePull
  Warning  Failed     17s (x3 over 57s)  kubelet            Failed to pull image "nginx:2.3.5": rpc error: code = NotFound desc = failed to pull and unpack image "docker.io/library/nginx:2.3.5": failed to resolve reference "docker.io/library/nginx:2.3.5": docker.io/library/nginx:2.3.5: not found
  Warning  Failed     17s (x3 over 57s)  kubelet            Error: ErrImagePull
  Warning  Failed     3s (x3 over 56s)   kubelet            Error: ImagePullBackOff

$ kubectl describe pod mypod -n ckad-prep | grep err -i > pod-error.txt
```

```bash
# 4. Change the image of the Pod to nginx:1.15.12
$ kubectl edit pod mypod -n ckad-prep

spec:
  containers:
  - image: nginx:1.15.12 # 从nginx:2.3.5改为nginx:1.15.12

pod/mypod edited

# 5. List the Pod and ensure that the container is running.
$ kubectl get pod -n ckad-prep
NAME    READY   STATUS    RESTARTS   AGE
mypod   1/1     Running   0          19m

# 6. Log into the container and run the ls command. Write down the output. Log out of the container.
$ kubectl exec mypod -n ckad-prep -- ls
# 或者
$ kubectl exec mypod -it -n ckad-prep  -- /bin/sh
/ # ls
bin  boot  dev	etc  home  lib	lib64  media  mnt  opt	proc  root  run  sbin  srv  sys  tmp  usr  var
/ # exit

# 7. Retrieve the IP address of the Pod mypod.
$ kubectl get pod -n ckad-prep -o wide
NAME    READY   STATUS    RESTARTS   AGE   IP            NODE           NOMINATED NODE   READINESS GATES
mypod   1/1     Running   0          29m   192.168.0.6   controlplane   <none>           <none>
```

```bash
# 8. Run a temporary Pod using the image busybox, shell into it and run a wget command against the nginx Pod using port 80.
# 用#7 里面得到的IP
$ kubectl run busybox --image=busybox --rm -it --restart=Never -n ckad-prep -- /bin/sh
/ # wget -O- 192.168.0.6:80
Connecting to 192.168.0.6:80 (192.168.0.6:80)
writing to stdout
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
-                    100% |***************************************************************************************************|   612  0:00:00 ETA
written to stdout
/ # exit
```

```bash
# 9. Render the logs of Pod mypod.
$ kubectl logs pods/mypod -n ckad-prep
192.168.0.7 - - [25/Dec/2022:10:47:23 +0000] "GET / HTTP/1.1" 200 612 "-" "Wget" "-"

# 10. Delete the Pod and the namespace.
$ kubectl delete pods/mypod -n ckad-prep
pod "mypod" deleted

$ kubectl delete ns ckad-prep
namespace "ckad-prep" deleted
```

### 2021考题2 - Configuring a Pod to Use a ConfigMap

1. Create a new file named `config.txt` with the following environment variables as key/value pairs on each line.
   - `DB_URL` equates to `localhost:3306`
   - `DB_USERNAME` equates to `postgres`
2. Create a new ConfigMap named `db-config` from that file.
3. Create a Pod named `backend` that uses the environment variables from the ConfigMap and runs the container with the image `nginx`.
4. Shell into the Pod and print out the created environment variables. You should find `DB_URL` and `DB_USERNAME` with their appropriate values.

```bash
# 1. Create a new file named `config.txt`
$ echo -e "DB_URL=localhost:3306\nDB_USERNAME=postgres" > config.txt
或者
$ vim config.txt
DB_URL=localhost:3306
DB_USERNAME=postgres

# 2. Create a new ConfigMap `db-config`
$ kubectl create configmap db-config --from-file config.txt
configmap/db-config created

# 3. Create a Pod `backend`
$ kubectl run backend --image nginx --dry-run=client -o yaml > 1.yaml
$ vim 1.yaml
```

参考官网[config](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#configure-all-key-value-pairs-in-a-configmap-as-container-environment-variables)

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: backend
  name: backend
spec:
  containers:
  - image: nginx
    name: backend
    resources: {}
    envFrom:         # Add
    - configMapRef:  # Add
        name: db-config  # Modify to configmap name: db-config
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

```bash
$ kubectl apply -f 1.yaml 
pod/backend created
```

```bash
# 4. Shell into the Pod and print out the created environment variables. You should find `DB_URL` and `DB_USERNAME` with their appropriate values.
$ kubectl exec backend -it -- /bin/sh
/ # env
config.txt=DB_URL=localhost:3306
DB_USERNAME=postgres
...
/ # exit

# 或者
$ kubectl exec backend -- env | grep DB
config.txt=DB_URL=localhost:3306
DB_USERNAME=postgres
```

### 2021考题3 - Configuring a Pod to Use a Secret

1. Create a new Secret named `db-credentials` with the key/value pair `db-password=passwd`.
2. Create a Pod named `backend` that defines uses the Secret as environment variable named `DB_PASSWORD` and runs the container with the image `nginx`.
3. Shell into the Pod and print out the created environment variables. You should find `DB_PASSWORD` variable.

```bash
# 1.
$ kubectl create secret generic db-credentials --from-literal=db-password=passwd
secret/db-credentials created
$ kubectl get secrets
NAME              TYPE      DATA   AGE
db-credentials    Opaque    1      26s

# 2. 
$ kubectl run backend --image=nginx --restart=Never -o yaml --dry-run > pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: backend
  name: backend
spec:
  containers:
  - image: nginx
    name: backend
    env:                          # Add
      - name: DB_PASSWORD         # modify to DB_PASSWORD
        valueFrom:                # Add
          secretKeyRef:           # Add
            name: db-credentials  # secret name
            key: db-password      # secret key
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

```bash
# 2.2
$ kubectl create -f pod.yaml

# 3
$ kubectl exec -it backend -- /bin/sh
/ # env
DB_PASSWORD=passwd
/ # exit

# 或者
$ kubectl exec backend -- env
```

### 考题4 - Creating a Security Context for a Pod

#### 2021考题4

1. Create a Pod named `secured` that uses the image `nginx` for a single container. Mount an `emptyDir` volume to the directory `/data/app`.
2. Files created on the volume should use the filesystem group ID `3000`.
3. Get a shell to the running container and create a new file named `logs.txt` in the directory `/data/app`. List the contents of the directory and write them down.

参考官网：[Configure a Security Context for a Pod or Container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-pod)

```bash
# 1.1 Create a Pod named `secured`
$ kubectl run secured --image=nginx -o yaml --dry-run > secured.yaml
```

```yaml
# secured.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: secured
  name: secured
spec:
  securityContext:        # Add
    fsGroup: 3000         # Add 2 filesystem group ID `3000`
  containers:
  - image: nginx
    name: secured
    volumeMounts:                   # Add 1.3 mount emptyDir
    - name: data-vol                # Add 1.3 mount emptyDir
      mountPath: /data/app          # Add 1.3 mount emptyDir
    resources: {}
  volumes:                  # Add 1.2 emptyDir
  - name: data-vol          # Add 1.2 emptyDir
    emptyDir: {}            # Add 1.2 emptyDir
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

```bash
# 2. Create a Pod named `secured`
$ kubectl create -f secured.yaml
pod/secured created

# 3 
$ kubectl exec -it secured -- sh
/ # cd /data/app
/ # touch logs.txt
/ # ls -l
-rw-r--r-- 1 root 3000 0 Mar 11 15:56 logs.txt
/ # exit
```

#### 2022 考题4 Security Context

> 只记住了大概

deployment 或者pod
- user ID `10000`
- Privilege escalation forbidden

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo
spec:
  securityContext:
    runAsUser: 10000          #  user ID `10000`
  volumes:
  - name: sec-ctx-vol
    emptyDir: {}
  containers:
  - name: sec-ctx-demo
    image: busybox:1.28
    command: [ "sh", "-c", "sleep 1h" ]
    volumeMounts:
    - name: sec-ctx-vol
      mountPath: /data/demo
    securityContext:
      allowPrivilegeEscalation: false  # Privilege escalation forbidden
```

### 考题5 - Defining a Pod’s Resource Requirements

#### 2021 考题5 ResourceQuota

1. Create a resource quota named `apps` under the namespace `rq-demo` using the following YAML definition in the file `rq.yaml`.

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: app
spec:
  hard:
    pods: "2"
    requests.cpu: "2"
    requests.memory: 500m
```

2. Create a new Pod that exceeds the limits of the resource quota requirements. Write down the error message.
3. Change the request limits to fulfill the requirements to ensure that the Pod could be created successfully. Write down the output of the command that renders the used amount of resources for the namespace.

```bash
# 1.
$ kubectl create namespace rq-demo
$ vim rq.yaml

metadata:
  name: apps

$ kubectl create -f rq.yaml --namespace=rq-demo
resourcequota/app created

$ kubectl get resourcequota/apps -n rq-demo
NAME   AGE     REQUEST                                                 LIMIT
apps   4m43s   pods: 0/2, requests.cpu: 0/2, requests.memory: 0/500m

$ kubectl describe quota --namespace=rq-demo
Name:            app
Namespace:       rq-demo
Resource         Used  Hard
--------         ----  ----
pods             0     2
requests.cpu     0     2
requests.memory  0     500m
```

参考官网：[resource-quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: mypod
  name: mypod
spec:
  containers:
  - image: nginx
    name: mypod
    resources:
      requests:
        memory: "1G"
        cpu: "400m"
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

```bash
# 2. 注意即使yaml文件里面加了metadata.namespace, 创建的命令仍然要加`-n`或者`--namespace`，否则新建的pod不在这个namespace上
$ kubectl create -f pod.yaml -n rq-demo
Error from server (Forbidden): error when creating "pod.yaml": pods "mypod" is forbidden: exceeded quota: app, requested: requests.memory=1G, used: requests.memory=0, limited: requests.memory=500m
```

3. Lower the memory settings to less than 500m (e.g. 200m) and create the Pod.

```bash
$ kubectl create -f pod.yaml --namespace=rq-demo
pod/mypod created
$ kubectl describe quota --namespace=rq-demo
Name:            app
Namespace:       rq-demo
Resource         Used  Hard
--------         ----  ----
pods             1     2
requests.cpu     400m  2
requests.memory  200m  500m
```

#### 2022 考题5 LimitRange

> 只记住了大概

有一个deployment，路径 `~/path/5.yaml`, namespace `namespace1` 因为resource不足，无法成功启动。
修改deployment：
- memory request "300Mi"
- memory limit 是所在namespace的一半

```bash
# 尝试get resourcequota, 但没得到东西
# k get resourcequota -n namespace1

# 尝试get resourcequota, 但没得到东西
k get limitranges -n namespace1
NAMESPACE   NAME              CREATED AT
default     mem-limit-range 

k k describe limitrange -n namespace1
Type        Resource  Min  Max  Default Request  Default Limit  Max Limit/Request Ratio
----        --------  ---  ---  ---------------  -------------  -----------------------
Container   memory    -    898Mi 256Mi            512Mi          -

```

```yaml
# pod 或者deployment
apiVersion: v1
kind: Pod
metadata:
  name: example-no-conflict-with-limitrange-cpu
spec:
  containers:
  - name: demo
    image: registry.k8s.io/pause:2.0
    resources:
      requests:
        memory: "300Mi"              # Add
      limits:
        memory: "449Mi"              # Add 898Mi 的一半
```

### 考题6 - Using a Service Account

1. Create a new service account named `backend-team`.
2. Print out the token for the service account in YAML format.
3. Create a Pod named `backend` that uses the image `nginx` and the identity `backend-team` for running processes.
4. Get a shell to the running container and print out the token of the service account.

```bash
# 1. Create a new service account
$ kubectl create serviceaccount backend-team
serviceaccount/backend-team created

## 参考https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#manually-create-a-long-lived-api-token-for-a-serviceaccount
# 加annotation
  annotations:
    kubernetes.io/service-account.name: backend-team

# 2.
$ kubectl get serviceaccount backend-team -o yaml --export
apiVersion: v1
kind: ServiceAccount
metadata:
  creationTimestamp: 2019-05-09T22:43:54Z
  name: backend-team
  namespace: default
  resourceVersion: "1888067"
  selfLink: /api/v1/namespaces/default/serviceaccounts/backend-team
  uid: ecd3b7ea-72ab-11e9-96c5-025000000001
secrets:
- name: backend-team-token-hskch
```

```bash
# 2.2 拿到对应的secret的encoded token
$ kubectl get secret backend-team-token-hskch -o yaml
apiVersion: v1
data:
...
  token:
ZXlKaGJHY2lPaUpTVXpJMU5pSXNJbXRwWkNJNkltNWFaRmRxWkRKMmFHTnZRM0JxV0haT1IxZzFiM3BJY201SlowaEhOV3hUWmt3elFuRmFhVEZhZDJNaWZ
RLmV5SnBjM01pT2lKcmRXSmxjbTVsZEdWekwzTmxjblpwWTJWaFkyTnZkVzUwSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOX
VZVzFsYzNCaFkyVWlPaUp1WlhCMGRXNWxJaXdpYTNWaVpYSnVaWFJsY3k1cGJ5OXpaWEoyYVdObFlXTmpiM1Z1ZEM5elpXTnlaWFF1Ym1GdFpTSTZJbTVsY
0hSMWJtVXRjMkV0ZGpJdGRHOXJaVzR0Wm5FNU1tb2lMQ0pyZFdKbGNtNWxkR1Z6TG1sdkwzTmxjblpwWTJWaFkyTnZkVzUwTDNObGNuWnBZMlV0WVdOamIz
VnVkQzV1WVcxbElqb2libVZ3ZEhWdVpTMXpZUzEyTWlJc0ltdDFZbVZ5Ym1WMFpYTXVhVzh2YzJWeWRtbGpaV0ZqWTI5MWJuUXZjMlZ5ZG1salpTMWhZMk5
2ZFc1MExuVnBaQ0k2SWpZMlltUmpOak0yTFRKbFl6TXROREpoWkMwNE9HRTFMV0ZoWXpGbFpqWmxPVFpsTlNJc0luTjFZaUk2SW5ONWMzUmxiVHB6WlhKMm
FXTmxZV05qYjNWdWREcHVaWEIwZFc1bE9tNWxjSFIxYm1VdGMyRXRkaklpZlEuVllnYm9NNENUZDBwZENKNzh3alV3bXRhbGgtMnZzS2pBTnlQc2gtNmd1R
XdPdFdFcTVGYnc1WkhQdHZBZHJMbFB6cE9IRWJBZTRlVU05NUJSR1diWUlkd2p1Tjk1SjBENFJORmtWVXQ0OHR3b2FrUlY3aC1hUHV3c1FYSGhaWnp5NHlp
bUZIRzlVZm1zazVZcjRSVmNHNm4xMzd5LUZIMDhLOHpaaklQQXNLRHFOQlF0eGctbFp2d1ZNaTZ2aUlocnJ6QVFzME1CT1Y4Mk9KWUd5Mm8tV1FWYzBVVWF
uQ2Y5NFkzZ1QwWVRpcVF2Y3pZTXM2bno5dXQtWGd3aXRyQlk2VGo5QmdQcHJBOWtfajVxRXhfTFVVWlVwUEFpRU43T3pka0pzSThjdHRoMTBseXBJMUFlRn
I0M3Q2QUx5clFvQk0zOWFiRGZxM0Zrc1Itb2NfV013
kind: Secret

# 2.3 拿到对应的secret的decoded token
$ kubectl describe secret backend-team-token-hskch -o yaml
...
Data
====
token:
eyJhbGciOiJSUzI1NiIsImtpZCI6Im5aZFdqZDJ2aGNvQ3BqWHZOR1g1b3pIcm5JZ0hHNWxTZkwzQnFaaTFad2MifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3Nl
cnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJuZXB0dW5lIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWN
jb3VudC9zZWNyZXQubmFtZSI6Im5lcHR1bmUtc2EtdjItdG9rZW4tZnE5MmoiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3
VudC5uYW1lIjoibmVwdHVuZS1zYS12MiIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6IjY2YmRjNjM2LTJlY
zMtNDJhZC04OGE1LWFhYzFlZjZlOTZlNSIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpuZXB0dW5lOm5lcHR1bmUtc2EtdjIifQ.VYgboM4CTd0pd
CJ78wjUwmtalh-2vsKjANyPsh-6guEwOtWEq5Fbw5ZHPtvAdrLlPzpOHEbAe4eUM95BRGWbYIdwjuN95J0D4RNFkVUt48twoakRV7h-
aPuwsQXHhZZzy4yimFHG9Ufmsk5Yr4RVcG6n137y-FH08K8zZjIPAsKDqNBQtxg-lZvwVMi6viIhrrzAQs0MBOV82OJYGy2o-
WQVc0UUanCf94Y3gT0YTiqQvczYMs6nz9ut-
XgwitrBY6Tj9BgPprA9k_j5qEx_LUUZUpPAiEN7OzdkJsI8ctth10lypI1AeFr43t6ALyrQoBM39abDfq3FksR-oc_WMw
ca.crt:     1066 bytes
namespace:  7 bytes

# 3.1 Create a Pod named `backend`
$ kubectl run backend --image=nginx --dry-run=client -o yaml > 6.yaml
$ vim 6.yaml 
```

参考官方文档[Configure Service Accounts for Pods](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#launch-a-pod-using-service-account-token-projection)

```yaml
# 6.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: backend
  name: backend
spec:
  serviceAccountName: backend-team  # Add
  containers:
  - image: nginx
    name: backend
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

```

```bash
# 3.2
$ k apply -f 6.yaml 
pod/backend created
$ k get pod/backend -o wide

# 4. print out the token from the volume source at /var/run/secrets/kubernetes.io/serviceaccount
$ kubectl exec -it backend -- /bin/sh
/ # cat /var/run/secrets/kubernetes.io/serviceaccount/token
eyJhbGciOiJSUzI1NiIsImtpZCI6IiJ9.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImJhY2tlbmQtdGVhbS10b2tlbi1kbTJmZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJiYWNrZW5kLXRlYW0iLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiIxNzM0MzVjMS00NDJmLTExZTktOGRjMy0wMjUwMDAwMDAwMDEiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6ZGVmYXVsdDpiYWNrZW5kLXRlYW0ifQ.DjWUxEMNUmQVoXd4b-eIjxboj3w3k7hS5hfV8mm8eoEPz3HJJMgjIpAaurcvo1pp2Ggpd1kIhQvfRqI6-u57f80N5UqXt_qATJfonat2NNXX8pXmFNoPig9LB-pbo8TN_pYGWNworXsxmK9w6V9eaRosIinRp0u-cvijQbsBw3lxWgGo9S4G-7f19mMKN1Pg2xS2J6fKX9IKvhHrUkM91nwcwmsO0use5B4TGbuRa9METiGsfEpegvzMPBbPl0B_T1ANH_pck0LFNtvKe0g1v5zpKx2lRF9WdFAqPsG7BJ1dEH88JtBHzD59OhxIPqtyT4sXKjACBN_ka5ZADMzPJg
```

### 考题7 - Implementing the Adapter Pattern

The adapter pattern helps with providing a simplified, homogenized view of an application running within a container. For example, we could stand up another container that unifies the log output of the application container. As a result, other monitoring tools can rely on a standardized view of the log output without having to transform it into an expected format.

1. Create a new Pod in a YAML file named `adapter.yaml`. The Pod declares two containers. 
   - The container `app` uses the image `busybox` and runs the command `while true; do echo "$(date) | $(du -sh ~)" >> /var/logs/diskspace.txt; sleep 5; done;`.
   - The adapter container `transformer` uses the image `busybox` and runs the command `sleep 20; while true; do while read LINE; do echo "$LINE" | cut -f2 -d"|" >> $(date +%Y-%m-%d-%H-%M-%S)-transformed.txt; done < /var/logs/diskspace.txt; sleep 20; done;` to strip the log output off the date for later consumption my a monitoring tool. Be aware that the logic does not handle corner cases (e.g. automatically deleting old entries) and would look different in production systems
2. Before creating the Pod, define an `emptyDir` volume. Mount the volume in both containers with the path `/var/logs`.
3. Create the Pod, log into the container `transformer`. The current directory should continuously write a new file every 20 seconds.

```bash
# 1.1
kubectl run adapter --image=busybox --restart=Never -o yaml --dry-run -- /bin/sh -c 'while true; do echo "$(date) | $(du -sh ~)" >> /var/logs/diskspace.txt; sleep 5; done;' > adapter.yaml

```

```yaml
# 1.2 adapter.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  name: adapter
spec:
  volumes:                # 2.1 `emptyDir` volume
    - name: config-volume # 2.1 `emptyDir` volume
      emptyDir: {}        # 2.1 `emptyDir` volume
  containers:
  - args:
    - /bin/sh
    - -c
    - 'while true; do echo "$(date) | $(du -sh ~)" >> /var/logs/diskspace.txt; sleep 5; done;' # 注意用单引号，因为命令里面有双引号
    image: busybox
    name: app           # 1.1 modify name to app
    volumeMounts:            # 2.2 Add
      - name: config-volume  # 2.2 Add
        mountPath: /var/logs # 2.2 Add
    resources: {}
  - image: busybox       # 1.2 Add
    name: transformer    # 1.2 Add
    args:                # 1.2 Add
    - /bin/sh            # 1.2 Add
    - -c                 # 1.2 Add
    - 'sleep 20; while true; do while read LINE; do echo "$LINE" | cut -f2 -d"|" >> $(date +%Y-%m-%d-%H-%M-%S)-transformed.txt; done < /var/logs/diskspace.txt; sleep 20; done;'             # 1.2 Add 注意用单引号，因为命令里面有双引号
    volumeMounts:             # 2.2 Add
      - name: config-volume   # 2.2 Add
        mountPath: /var/logs  # 2.2 Add
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

```

```bash
# 3
$ kubectl exec adapter --container=transformer -it -- /bin/sh
/ # ls -l
-rw-r--r--    1 root     root           205 May 12 20:43 2019-05-12-20-43-32-transformed.txt
-rw-r--r--    1 root     root           369 May 12 20:43 2019-05-12-20-43-52-transformed.txt
...
/ # cat 2019-05-12-20-43-52-transformed.txt
 4.0K	/root
 4.0K	/root
 4.0K	/root
 4.0K	/root
/ # exit

```

### 考题8 - Defining a Pod’s Readiness and Liveness Probe

1. Create a new Pod named `hello` with the image `bonomat/nodejs-hello-world` that exposes the port `3000`. Provide the name `nodejs-port` for the container port.
2. Add a Readiness Probe that checks the URL path `/` on the port referenced with the name `nodejs-port` after a `2` seconds delay. You do not have to define the period interval.
3. Add a Liveness Probe that verifies that the app is up and running every `8` seconds by checking the URL path `/` on the port referenced with the name `nodejs-port`. The probe should start with a `5` seconds delay.
4. Shell into container and `curl localhost:3000`. Write down the output. Exit the container. Retrieve the logs from the container. Write down the output.

```bash
# 1. Create a new Pod named `hello`
$ kubectl run hello --image=bonomat/nodejs-hello-world --port=3000 -o yaml --dry-run > pod.yaml
$ vim pod.yaml
```

参考官网： [livenessProbe](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#use-a-named-port)

```yaml
# 1.2 pod.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: hello
  name: hello
spec:
  containers:
  - image: bonomat/nodejs-hello-world
    name: hello
    ports:
    - name: nodejs-port           # Add 1.2 Provide the name `nodejs-port` for the container port
      containerPort: 3000
    readinessProbe:               # Add 2 Readiness
      httpGet:                    # Add 2 Readiness
        path: /                   # Add 2 Readiness
        port: nodejs-port         # Add 2 Readiness
      initialDelaySeconds: 2       # Add 2 Readiness
    livenessProbe:            # Add 3 livenessProbe
      httpGet:                # Add 3 livenessProbe
        path: /               # Add 3 livenessProbe
        port: nodejs-port     # Add 3 livenessProbe
      initialDelaySeconds: 5  # Add 3 livenessProbe
      periodSeconds: 8        # Add 3 livenessProbe
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

```bash
$ kubectl create -f pod.yaml
pod/hello created

# 4. 
$ kubectl exec hello -it -- /bin/sh
/ # curl localhost:3000
<!DOCTYPE html>
<html>
<head>
	<title>NodeJS Docker Hello World</title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link href="http://cdn.bootcss.com/bootstrap/3.3.2/css/bootstrap.min.css" rel="stylesheet">
	<link href="/stylesheets/styles.css" rel="stylesheet">
</head>
<body>
	<div class="container">
		<div class="well well-sm">
			<h2>This is just a hello world message</h2>
			<img a href="./cage.jpg"/>
			<img src="src/cage.jpg" alt="Smiley face" width="640">
		</div>
	</div>
</body>
</html>
/ # exit
 
$ kubectl logs pod/hello
Magic happens on port 3000
```

#### 2022 readiness probe

### 考题9 - Fixing a Misconfigured Pod

1. Create a new Pod with the following YAML.

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: failing-pod
  name: failing-pod
spec:
  containers:
  - args:
    - /bin/sh
    - -c
    - while true; do echo $(date) >> ~/tmp/curr-date.txt; sleep 5; done;
    image: busybox
    name: failing-pod
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

2. Check the Pod’s status. Do you see any issue?
3. Follow the logs of the running container and identify an issue.
4. Fix the issue by shelling into the container. After resolving the issue the current date should be written to a file. Render the output.

```bash
# 1 Create a new Pod
$ vim pod.yaml
$ kubectl create -f pod.yaml

# 2. Check the Pod’s status
# seems to be running without problems.
$ kubectl get pods
NAME          READY   STATUS    RESTARTS   AGE
failing-pod   1/1     Running   0          5s

# 3
$ kubectl logs failing-pod
/bin/sh: can't create /root/tmp/curr-date.txt: nonexistent directory
/bin/sh: can't create /root/tmp/curr-date.txt: nonexistent directory
/bin/sh: can't create /root/tmp/curr-date.txt: nonexistent directory
```

```bash
# 4.
$ kubectl exec failing-pod -it -- /bin/sh
/ # mkdir -p /root/tmp
/ # cd /root
~ # ls -l
total 4
drwxr-xr-x    2 root     root          4096 Dec 26 04:47 tmp
~ # chmod 777 /root/tmp
~ # cd /root/tmp
~/tmp # ls -l
total 4
-rw-r--r-- 1 root root 112 May  9 23:52 curr-date.txt
/ # cat ~/tmp/curr-date.txt
Thu May 9 23:59:01 UTC 2019
Thu May 9 23:59:06 UTC 2019
Thu May 9 23:59:11 UTC 2019
/ # exit

```

### 考题10 - 2022 Rollout Canary

Application "wonderful" is running in `default` Namespace.
You can call the app using `curl wonderful:30080` .
The application YAML is available at `/wonderful/init.yaml` .
The app has a Deployment with image `httpd:alpine` , but should be switched over to `nginx:alpine` .

1. The switch should not happen fast or automatically, but using the Canary approach:

- 20% of requests should hit the new image
- 80% of requests should hit the old image

2. For this create a new Deployment `wonderful-v2` which uses image `nginx:alpine` .

3. The total amount of Pods of both Deployments combined should be `10`.

参考官方文档[canary-deployments](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#canary-deployments)

```bash
$ k get deployments.apps
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
wonderful-v1   10/10   10           10          27s

$ k get deployments.apps wonderful-v1 -o yaml > v2.yaml
```

```yaml
# v2.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: wonderful
  name: wonderful-v2 # name
spec:
  replicas: 2        # Modify to 2
  selector:
    matchLabels:
      app: wonderful
  template:
    metadata:
      labels:
        app: wonderful
    spec:
      containers:
      - image: nginx:alpine  # Image
        name: nginx
```

```bash
$ k apply -f v2.yaml 
$ k get deployments.apps 
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
wonderful-v1   10/10   10           10          4m37s
wonderful-v2   2/2     2            2           4s

$ k edit deployments.apps wonderful-v1

```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: wonderful
  name: wonderful-v1
spec:
  replicas: 8     # Modify to 8
  selector:
    matchLabels:
      app: wonderful
  template:
    metadata:
      labels:
        app: wonderful
    spec:
      containers:
      - image: httpd:alpine
        name: httpd
```

```bash
$ k get deployments.apps 
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
wonderful-v1   8/8     8            8           5m38s
wonderful-v2   2/2     2            2           65s
```

### 考题11 - 2022 Helm Nanagement

### 考题12 - 2022 NetworkPolicy

记不太清了。。。
修改pod `pod1`，使得only to and from pod `frondend` and `db`
networkpolicy已经建好，不要增加，新建或者修改

这样的话，应该只需要根据已有networkpolicy，修改`pod1`的labels就可以了。

有个类似的题：

#### Restricting Access to and from a Pod

Let’s assume we are working on an application stack that defines three different layers: a `frontend`, a `backend` and a `database`. Each of the layers runs in a Pod. You can find the definition in the YAML file `app-stack.yaml`. The application needs to run in the namespace `app-stack`.

Task:

1. Create the required namespace.
2. Copy the Pod definition to the file `app-stack.yaml` and create all three Pods. Notice that the namespace has already been defined in the YAML definition.
3. Create a network policy in the YAML file `app-stack-network-policy.yaml`.
4. The network policy should allow incoming traffic from the `backend` to the `database` but disallow incoming traffic from the `frontend`.
5. Incoming traffic to the `database` should only be allowed on `TCP` port `3306` and no other port.

<details>
  <summary>3个 pod yaml文件</summary>
  <p>

    ```yaml
    kind: Pod
    apiVersion: v1
    metadata:
      name: frontend
      namespace: app-stack
      labels:
        app: todo
        tier: frontend
    spec:
      containers:
        - name: frontend
          image: nginx

    ---

    kind: Pod
    apiVersion: v1
    metadata:
      name: backend
      namespace: app-stack
      labels:
        app: todo
        tier: backend
    spec:
      containers:
        - name: backend
          image: nginx

    ---

    kind: Pod
    apiVersion: v1
    metadata:
      name: database
      namespace: app-stack
      labels:
        app: todo
        tier: database
    spec:
      containers:
        - name: database
          image: mysql
          env:
          - name: MYSQL_ROOT_PASSWORD
            value: example
    ```

  </p>
</details>

```bash
# 1 Create the namespace
$ kubectl create namespace app-stack
namespace/app-stack created

# 2. create all three Pods
$ vim app-stack.yaml
$ kubectl create -f app-stack.yaml
pod/frontend created
pod/backend created
pod/database created

$ kubectl get pods --namespace app-stack
NAME       READY   STATUS    RESTARTS   AGE
backend    1/1     Running   0          22s
database   1/1     Running   0          22s
frontend   1/1     Running   0          22s

# 3. Create the network policy.
$ vim app-stack-network-policy.yaml
$ kubectl create -f app-stack-network-policy.yaml
$ kubectl get networkpolicy --namespace app-stack
NAME                       POD-SELECTOR             AGE
app-stack-network-policy   app=todo,tier=database   5s
```

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: app-stack-network-policy
  namespace: app-stack
spec:
  podSelector:
    matchLabels:
      app: todo
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: todo
          tier: backend
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: todo
          tier: database
    ports:
      - protocol: TCP
        port: 3306

```


### 考题13 - 2022 Docker

1. 通过Dckerfile 创建image with name `name1`, tag `tag1` (不要publish)
2. export container to ~/somepath/name.tar

```bash
# 1 创建image
cd ~/path2Dockerfile/Dckerfile
podman build -t name1:tag1 .
podman image less

# run container
podman run -d name1:tag1
podman ps

# export container
podman export containerID > ~/somepath/name.tar
```

### 考题14 - 2022 `CronJobs`

1. 新建一个CronJobs ppi, 要求

- 每10分钟执行一次
- completion 2
- fail 4
- delete after 9s
- restartPolicy 为nerver

Cronjob 里面的container信息已给出：

```yaml
    name: pi
    image: perl:5.34.0
    command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]

```

2. 新建一个Job xxx, 来执行CronJobs。。。

```yaml
apiVersion: batch/v1 
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "*/10 * * * *"          #每10分钟执行一次， 记着前面加*/
  jobTemplate:
    spec:
      backoffLimit: 4             # fail 4， 注意不要加在spec下面，而是spec.jobTemplate.spec下
      completions: 2              # completion 2
      ttlSecondsAfterFinished: 9  # delete after 9s
      template:
        spec:
          containers:
          - name: pi              # 粘贴题目给出信息
            image: perl:5.34.0    # 粘贴题目给出信息
            command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"] # 粘贴题目给出信息
          restartPolicy: Never                                  # restartPolicy 为nerver
```

### 考题15 - 2022 service, ingress

namespace `namespace1`
一个路径`~/path`下，有`service.yaml`, `ingress.yaml`和 `deployment.yaml`。
现在无法访问 `curl http://xxxx/content-moment`，检查并修复问题。
不要修改`deployment.yaml`，deployment没有问题

```bash
cd ~/path
ls

k get service -n namespace1
content-moment-service

vim ingress.yaml
```

```yaml
# ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: minimal-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx             # 通过k get ingressclass -A 检查，发现没错，不需要改
  rules:
  - http:
      paths:
      - path: /app                    # 路径不对，改为/content-moment
        pathType: Prefix
        backend:
          service:
            name: content-moment-service-service # 改为content-moment-service
            port:
              number: 80
```

```yaml
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376        # 通过查看 deployment.yaml 里面的 containerPort, 发现这里错误，改为containerPort对应的port
```

## CKAD 练习题

### 练习题1 - Rollout Rolling

1. Application "wonderful" is running in `default` Namespace.
2. You can call the app using `curl wonderful:30080` .
3. The app has a Deployment with image `httpd:alpine` , but should be switched over to `nginx:alpine` .
4. Set the `maxSurge` to `50%` and the `maxUnavailable` to `0%` . Then perform a rolling update.
5. Wait till the rolling update has succeeded.

<details>
  <summary>Explanation</summary>
  <p>

    Why can you call `curl wonderful:30080` and it works?

    There is a NodePort Service `wonderful` which listens on port `30080` . It has the Pods of Deployment of app "wonderful" as selector.

    We can reach the NodePort Service via the K8s Node IP:

    ```bash
    curl 172.30.1.2:30080
    ```

    And because of an entry in `/etc/hosts `we can call:

    ```bash
    curl 172.30.1.2:30080
    ```

  </p>
</details>

<details><summary>Solution</summary>
<p>


```bash
k edit deploy wonderful-v1
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "2"
  creationTimestamp: "2022-12-26T07:00:45Z"
  generation: 2
  labels:
    app: wonderful
  name: wonderful-v1
  namespace: default
  resourceVersion: "2063"
  uid: 5cf0fc94-8bc5-47b2-bc71-2147880bf1ed
spec:
  progressDeadlineSeconds: 600
  replicas: 3
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: wonderful
  strategy:
    rollingUpdate:
      maxSurge: 50%              # Edit 4
      maxUnavailable: 0%         # Edit 4
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: wonderful
    spec:
      containers:
      - image: nginx:alpine     # Edit 3
        imagePullPolicy: IfNotPresent
        name: httpd
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
```

```bash
curl 172.30.1.2:30080
```

</p>
</details>





### 练习题2 - Rollout Green-Blue

Application "wonderful" is running in `default` Namespace.

You can call the app using `curl wonderful:30080` .

The application YAML is available at `/wonderful/init.yaml` .

The app has a Deployment with image `httpd:alpine` , but should be switched over to `nginx:alpine` .

1. The switch should happen instantly. Meaning that from the moment of rollout, all new requests should hit the new image.

   - 1.1 Create a new Deployment `wonderful-v2` which uses image `nginx:alpine` with `4` replicas. It's Pods should have labels `app: wonderful` and `version: v2`
   - 1.2 Once all new Pods are running, change the selector label of Service wonderful to `version: v2`
   - 1.3 Finally scale down Deployment `wonderful-v1` to `0` replicas

<details>
  <summary>Solution</summary>
  <p>

```bash
# 2.1 Create a new Deployment and watch these places:
cp /wonderful/init.yaml v2.yaml
vim v2.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: wonderful
  name: wonderful-v2    # Modify
spec:
  replicas: 4           # Modify
  selector:
    matchLabels:
      app: wonderful
      version: v2       # Modify 1.1
  template:
    metadata:
      labels:
        app: wonderful
        version: v2     # Modify 1.1
    spec:
      containers:
      - image: nginx:alpine    # Modify 1.1
        name: nginx
    # delete service part
```

```bash
$ k apply -f v2.yaml 
# Wait till all Pods are running, then switch the Service selector:
$ k get deployments.apps 
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
wonderful-v1   4/4     4            4           13m
wonderful-v2   4/4     4            4           4s

# 1.2
$ k get service
NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
wonderful    NodePort    10.98.188.152   <none>        80:30080/TCP   9m21s

$ k edit service wonderful
```

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: wonderful
  name: wonderful
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
    nodePort: 30080
  selector:
    app: wonderful
    version: v2     # Modify 1.2
  type: NodePort

```

Confirm with curl wonderful:30080 , all requests should hit the new image.

```bash
# 1.3 Finally scale down the original Deployment:
kubectl scale deploy wonderful-v1 --replicas 0
```

  </p>
</details>


## 参考文章

- CKAD 真题
  - [CKAD考试预备动员](https://blog.csdn.net/xixihahalelehehe/article/details/104332178?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166047629616782350895616%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166047629616782350895616&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~pc_rank_34-23-104332178-null-null.142^v40^pc_search_integral,185^v2^control&utm_term=CKAD%E8%80%83%E8%AF%95%E9%A2%98&spm=1018.2226.3001.4187)
    - [CKAD 1. Core Concepts(13%)考题答案](https://blog.csdn.net/xixihahalelehehe/article/details/108342028)
    - [CKAD 2. Configuration (18%)练习题](https://blog.csdn.net/xixihahalelehehe/article/details/108342510)
    - [CKAD 3. Multi-Container Pods (10%)练习题](https://blog.csdn.net/xixihahalelehehe/article/details/108350785)
    - [CKAD 4. Observability(18%)练习题](https://blog.csdn.net/xixihahalelehehe/article/details/108358664)
    - [CKAD 5. Pod Design (20%)练习题](https://blog.csdn.net/xixihahalelehehe/article/details/108365404)
    - [CKAD 6. Services & Networking (13%)练习题](https://blog.csdn.net/xixihahalelehehe/article/details/108420840)
    - [CKAD 7. State Persistence (8%)练习题](https://blog.csdn.net/xixihahalelehehe/article/details/108423635)
    - [CKAD 8. Bonus Exercises考试必背](https://blog.csdn.net/xixihahalelehehe/article/details/108424082)
  - [2021年全年CKAD真题 5道题](https://blog.csdn.net/marlon212/article/details/120245331?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166047524116782246432126%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=166047524116782246432126&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-4-120245331-null-null.nonecase&utm_term=CKAD&spm=1018.2226.3001.4450)
  - [2021 Kubernetes CKAD 1.20 - 真题 4道题](https://blog.csdn.net/itsaka/category_11115176.html)
    - [Kubernetes CKAD 1.20 - 真题 （第1题）Creating a Pod and Inspecting it](https://blog.csdn.net/itsaka/article/details/117590286)
    - [Kubernetes CKAD 1.20 - 真题 （第2题）Configuring a Pod to Use a ConfigMap](https://blog.csdn.net/itsaka/article/details/117590437)
    - [Kubernetes CKAD 1.20 - 真题 （第3题）Implementing the Adapter Pattern](https://blog.csdn.net/itsaka/article/details/117590502)
    - [Kubernetes CKAD 1.20 - 真题 （第4题）Defining a Pod’s Readiness and Liveness Probe](https://blog.csdn.net/itsaka/article/details/117590558)
  - [2022 K8S CKAD 1.23 考试 实验 模拟环境（一键导入）【需购买】](https://blog.csdn.net/vic_qxz/article/details/123361130?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166039499316782248581366%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166039499316782248581366&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~pc_rank_34-16-123361130-null-null.142^v40^pc_search_integral,185^v2^control&utm_term=CKAD%E8%80%83%E8%AF%95%E9%A2%98&spm=1018.2226.3001.4187)
- [Practical tips for passing CKAD certification exam](https://itnext.io/practical-tips-for-passing-ckad-exam-6cbdf2d35cb1)
