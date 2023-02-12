---
title: 2023 CKS v1.26 考试真题整理
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

[CKS 考试链接](https://training.linuxfoundation.org/certification/certified-kubernetes-security-specialist/#)
[Important Instructions: CKS](https://docs.linuxfoundation.org/tc-docs/certification/important-instructions-cks)

- 考试包括 15-20 项performance-based tasks。
  - 2023.1 实测是16道题
- 考生有 2 小时的时间完成 CKS 考试。
  - 因为从06/2022开始环境升级（贬义），考试环境更难用了，变的很卡，所以时间变得比较紧张。容易做不完题，建议先把有把握的，花费时间不多的题先做掉
    - [CKS CKA CKAD changed Terminal to Remote Desktop](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e)
- CKS考试66分以上即可通过，考试不通过有一次补考机会。

Certifications- expire 36 months from the date that the Program certification requirements are met by a candidate.

### Certified Kubernetes Security Specialist (CKS)

The following tools and resources are allowed during the exam as long as they are used by candidates to work independently on exam tasks (i.e. not used for 3rd party assistance or research) and are accessed from within the Linux server terminal on which the Exam is delivered.
During the exam, candidates may:

- review the Exam content instructions that are presented in the command line terminal.
- review Documents installed by the distribution (i.e. /usr/share and its subdirectories)
- use the search function provided on <https://kubernetes.io/docs/> however, they may only open search results that have a domain matching the sites listed below
- use the browser within the VM to access the following documentation:  
  - Kubernetes Documentation:
    - <https://kubernetes.io/docs/> and their subdomains
    - <https://kubernetes.io/blog/> and their subdomains
  This includes all available language translations of these pages (e.g. <https://kubernetes.io/zh/docs/>)
  - Tools:
    - Trivy documentation <https://aquasecurity.github.io/trivy/>
    - Falco documentation <https://falco.org/docs/>
  This includes all available language translations of these pages (e.g. <https://falco.org/zh/docs/>)
  - App Armor:
    - Documentation <https://gitlab.com/apparmor/apparmor/-/wikis/Documentation>

You're only allowed to have one other browser tab open with:

- <https://kubernetes.io/docs>
- <https://github.com/kubernetes>
- <https://kubernetes.io/blog>
- <https://github.com/aquasecurity/trivy>
- <https://falco.org/docs>
- <https://gitlab.com/apparmor/apparmor/-/wikis/Documentation>

### CKS Environment

- Each task on this exam must be completed on a designated cluster/configuration context.
- Sixteen clusters comprise the exam environment, one for each task. Each cluster is made up of one master node and one worker node.
- An infobox at the start of each task provides you with the cluster name/context and the hostname of the master and worker node.
- You can switch the cluster/configuration context using a command such as the following:
- `kubectl config use-context <cluster/context name>`
- Nodes making up each cluster can be reached via ssh, using a command such as the following:
- `ssh <nodename>`
- You have elevated privileges on any node by default, so there is no need to assume elevated privileges.
- You must return to the base node (hostname cli) after completing each task.
- Nested `−ssh` is not supported.
- You can use `kubectl` and the appropriate context to work on any cluster from the base node. When connected to a cluster member via ssh, you will only be able to work on that particular cluster via kubectl.
- For your convenience, all environments, in other words, the base system and the cluster nodes, have the following additional command-line tools pre-installed and pre-configured:
  - `kubectl` with kalias and Bash autocompletion
  - `yq` and `jq` for YAML/JSON processing
  - `tmux` for terminal multiplexing
  - `curl` and `wget` for testing web services
  - `man` and man pages for further documentation
- Further instructions for connecting to cluster nodes will be provided in the appropriate tasks
- The CKS environment is currently running etcd v3.5
- The CKS environment is currently running Kubernetes v1.26
- The CKS  exam environment will be aligned with the most recent K8s minor version within approximately 4 to 8 weeks of the K8s release date.

### More items for CKS than CKA and CKAD

- Pod Security Policies(PSP) - removed from Kubernetes in `v1.25`
- [AppArmor](https://kubernetes.io/docs/tutorials/security/apparmor/)
- Apiserver
  - Apiserver Crash
  - Apiserver NodeRestriction
- ImagePolicyWebhook
- [kube-bench](https://github.com/aquasecurity/kube-bench)
- [Trivy](https://github.com/aquasecurity/trivy)

### [CKS 知识点&练习题总结](./Kubernetes-CKS-%E7%9F%A5%E8%AF%86%E7%82%B9-%E7%BB%83%E4%B9%A0%E9%A2%98.html)

## 如何备考

### [k8s练习环境](./Kubernates-Certified-Kubernetes-Administrator-CKA.html#k8s%E7%BB%83%E4%B9%A0%E7%8E%AF%E5%A2%83)(同CKA)

### CKS练习题

有几个练习库，建议将每个题目都自己亲自操作一遍，一定要操作。

- CKS在线练习环境：<https://killercoda.com/killer-shell-cks>
- [CKS Simulator Kubernetes 1.26](https://killer.sh/attendee/f65d95f1-170b-444d-8af0-bbf302f8c796/content)
- [Adminission pligin/Pod Security Policies 练习](https://killercoda.com/killer-shell-ckad/scenario/admission-controllers)

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
```

```bash
# CKS
## 创建secret
kubectl create secret generic db-credentials --from-literal db-password=passwd
## modify a pod yaml to deployment yaml
### put the Pod's metadata: and spec: into the Deployment's template: section:

## To verify that the token hasn't been mounted run the following commands:
kubectl -n one exec -it pod-name -- mount | grep serviceaccount
kubectl -n one exec -it pod-name -- cat /var/run/secrets/kubernetes.io/serviceaccount/token

### 创建 clusterrole，使用 psp
kubectl create clusterrole restrict-access-role --verb=use --resource=psp --resource-name=restrict-policy

## after modify /etc/kubernetes/manifests/kube-apiserver.yaml
systemctl restart kubelet

### 查询 sa 对应的 role 名称（假设是 role-1）
kubectl get rolebinding -n db -oyaml | grep 'service-account-web' -B 10

### grep
grep apple -A 10 # apple之后10行

grep apple -B 10 # apple之前10行

### secret used by pod
kubectl exec pod1 -- env
kubectl exec pod1 -- cat /etc/diver/hosts
```

## [经验总结](http://liyuankun.top/Kubernates-Certified-Kubernetes-Administrator-CKA.html#%E7%BB%8F%E9%AA%8C%E6%80%BB%E7%BB%93)(同CKA)

## [Pre Setup](http://liyuankun.top/Kubernates-Certified-Kubernetes-Administrator-CKA.html#pre-setup)(同CKA)

## CKS 2023 真题 1.26

### 考题1 - AppArmor 访问控制

#### Context

AppArmor is enabled on the cluster's worker node. An AppArmor profile is prepared, but not enforced yet.
You may use your browser to open one additional tab to access the AppArmor documentation.

AppArmor 已在 cluster 的工作节点上被启用。一个 AppArmor 配置文件已存在，但尚未被实施。

#### Task

On the cluster's worker node, enforce the prepared AppArmor profile located at `/etc/apparmor.d/nginx_apparmor` .
Edit the prepared manifest file located at `/home/candidate/KSSH00401/nginx-deploy.yaml` to apply the AppArmor profile.
Finally, apply the manifest file and create the pod specified in it.

在 cluster 的工作节点上，实施位于 `/etc/apparmor.d/nginx_apparmor` 的现有 AppArmor 配置文件。
编辑位于 `/home/candidate/KSSH00401/nginx-deploy.yaml` 的现有清单文件以应用 AppArmor 配置文件。
最后，应用清单文件并创建其中指定的 Pod 。

#### Solution

搜索 apparmor（使用 AppArmor 限制容器对资源的访问），接着再搜索字符串 “parser”
<https://kubernetes.io/zh/docs/tutorials/security/apparmor/>

```bash
### 远程登录到指定工作节点
ssh cka-node01

### 从profile文件查看策略名称
cat /etc/apparmor.d/nginx_apparmor

    profile nginx-profile flags=(attach_disconnected) {
    ...

### 加载 apparmor 配置文件
apparmor_parser /etc/apparmor.d/nginx_apparmor

### 查看策略名称，结果是 nginx-profile
apparmor_status | grep nginx-profile

### 回到控制节点，并更新 Pod 的注解
exit

vim /home/candidate/KSSH00401/nginx-deploy.yaml
    annotations:
      ### hello 是 Pod 里容器名称，nginx-profile 则是 apparmor_status 解析出来的结果
      container.apparmor.security.beta.kubernetes.io/hello: localhost/nginx-profile

### 如果 apply 后报错，则先删除保存并删除旧 Pod，改完后再创建新的
kubectl apply -f /home/candidate/KSSH00401/nginx-deploy.yaml
```

### 考题2 - Kube-Bench 基准测试

#### Context

A CIS Benchmark tool was run against the kubeadm-created cluster and found multiple issues that must be addressed immediately.

针对 kubeadm 创建的 cluster 运行 CIS 基准测试工具时， 发现了多个必须立即解决的问题。

#### Task

Fix all issues via configuration and restart theaffected components to ensure the new settings take effect.
通过配置修复所有问题并重新启动受影响的组件以确保新的设置生效。

Fix all of the following violations that were found against the API server:
修复针对 API 服务器发现的所有以下违规行为：
Ensure that the 1.2.7 --authorization-mode FAIL argument is not set to AlwaysAllow
Ensure that the 1.2.8 --authorization-mode FAIL argument includes Node
Ensure that the 1.2.9 --authorization-mode FAIL argument includes RBAC
Ensure that the 1.2.18 --insecure-bind-address FAIL argument is not set
Ensure that the 1.2.19 --insecure-port FAIL argument is set to 0

Fix all of the following violations that were found against the kubelet:
修复针对 kubelet 发现的所有以下违规行为：
Ensure that the 4.2.1 --anonymous-auth FAIL argument is set to false
Ensure that the 4.2.2 --authorization-mode FAIL argument is not set to AlwaysAllow
Use `Webhook` authn/authz where possible. 注意：尽可能使用 Webhook authn/authz。

Fix all of the following violations that were found against etcd:
修复针对 etcd 发现的所有以下违规行为：
Ensure that the 4.2.1 --client-cert-auth FAIL argument is set to true

#### Solution

```bash
$ ssh root@vms65.rhce.cc

# kube-bench run --target=master --check=1.2.7
kube-bench run --target=master | grep FAIL

### 修复针对 APIserver 发现的以下所有问题：
### 确保 1.2.7 --authorization-mode 参数不能设置为 AlwaysAllow
### 确保 1.2.8 --authorization-mode 参数包含 Node
### 确保 1.2.9 --authorization-mode 参数包含 RBAC
### 确保 1.2.18 --insecure-bind-address 参数不能设置
### 确保 1.2.19 --insecure-port 参数设置为 0
### 注意：修改 master 节点！
vim /etc/kubernetes/manifests/kube-apiserver.yaml
    #- --authorization-mode=AlwaysAllow 删除AlwaysAllow，加Node,RBAC
    - --authorization-mode=Node,RBAC
    #- --insecure-bind-address=0.0.0.0
    - --insecure-port=0

### 修复针对 kubelet 发现的以下所有问题：
### 确保 4.2.1 anonymous-auth 参数设置为 false
### 确保 4.2.2 --authorization-mode 参数不能设置为 AlwaysAllow，尽可能使用 Webhook authn/authz
### 注意：master 和 node 节点都要修改！
vim /var/lib/kubelet/config.yaml
    authentication:
      anonymous:
        enabled: false
    authorization:
      mode: Webhook

### 修复针对 etcd 发现的以下所有问题：
### 确保 4.2.--client-cert-auth 参数设置为 true
### 注意：修改 master 节点！
vim /etc/kubernetes/manifests/etcd.yaml
    - --client-cert-auth=true

### 加载并重启 kubelet 服务
### 注意：master 和 node 节点都要重启！
systemctl daemon-reload
systemctl restart kubelet
```

### 考题3 - Trivy 镜像扫描

#### Task

使用 Trivy 开源容器扫描器检测 namespace kamino 中 Pod 使用的具有严重漏洞的镜像。
查找具有 High 或 Critical 严重性漏洞的镜像，并删除使用这些镜像的 Pod。
注意：Trivy 仅安装在 cluster 的 master 节点上，在工作节点上不可使用。你必须切换到 cluster 的 master 节点才能使用 Trivy 。

Use the Trivy open-source container scanner to detect images with severe vulnerabilities used by Pods in the namespace `kamino`.
Look for images with `High` or `Critical` severity vulnerabilities, and delete the Pods that use those images.

Trivy is pre-installed on the cluster's `master` node only; it is not available on the base system or the worker nodes. You'll have to connect to the cluster's master node to use `Trivy`.

#### Solution

搜索 kubectl images（列出集群中所有运行容器的镜像）
<https://kubernetes.io/zh-cn/docs/tasks/access-application-cluster/list-all-running-container-images/>

```bash
### 需登录到控制节点操作
ssh cka-master01

### 查询命名空间 kamino 中 pod 使用的镜像
kubectl get pod -n kamino -o yaml | grep image:
# 或者
kubectl get pods -n kamino -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' | sort

### 假设镜像是 registry.aliyuncs.com/google_containers/coredns:1.7.0
### 使用 trivy 工具查询具有 HIGH 或 CRITICAL 漏洞的镜像
trivy --help
trivy image --severity HIGH,CRITICAL 'registry.aliyuncs.com/google_containers/coredns:1.7.0'

### 删除检测到的漏洞镜像对应的 pod（如果有控制器，得删除控制器）
kubectl delete pod -n kamino pod名称
```

### 考题4 - Sysdig & Falco

you may use you brower to open one additonal tab to access sysdig's documentation or Falco's documentaion

#### Task

Use runtime detection tools to detect anomalous processes spawning and executing frequently in the sigle container belonging to Pod `redis`. Two tools are avaliable to use:
使用运行时检测工具来检测 Pod tomcat 单个容器中频发生成和执行的异常进程。有两种工具可供使用：

- sysdig
- falco

The tools are pre-installed on the cluster's worker node only, they are not avaliable on the base system or the master node.
Using the tool of you choice (including any non pre-install tool) analyse the container's behavior for at least `30` seconds, using filers that detect newly spawing and executing processes, store an incident file at `/opt/KSR00101/incidents/summary`, containing the detected incidents one per line in the follwing format:
注：这些工具只预装在 cluster 的工作节点，不在 master 节点。
使用工具至少分析 30 秒，使用过滤器检查生成和执行的进程，将事件写到 `/opt/KSR00101/incidents/summary` 文件中，其中包含检测的事件, 每个单独一行
格式如下：

```yaml
   [timestamp],[uid],[processName]
```

保持工具的原始时间戳格式不变。
注：确保事件文件存储在集群的工作节点上。

```bash
# 方法一 sysdig
### 需登录到工作节点操作
ssh cka-node01

### 查看 sysdig 帮助
sysdig -h

### 查看 sysdig 支持的元数据
sysdig -l

### 查看指定容器ID
crictl ps | grep redis

### -M 分析容器30秒，-p 指定事件保存格式，--cri 指定容器运行时，并且保存到指定文件路径中
sysdig -M 30 -p "*%evt.time,%user.uid,%proc.name" --cri /run/containerd/containerd.sock container.id=xxxxx > /opt/KSR00101/incidents/summary
```

```bash
# 方法二 falco
### 需登录到工作节点操作
ssh cka-node01

### 
cd /etc/falco
ls

### 
vim /etc/falco/falco_rules.yaml
# Container is supposed to be immutable. Package management should be done in building the image.
- rule: Launch Package Management Process in Container
  desc: Package management process ran inside container
  condition: >
    spawned_process
    and container
    and user.name != "_apt"
    and package_mgmt_procs
    and not package_mgmt_ancestor_procs
    and not user_known_package_manager_in_container
  output: >
    Package management process launched in container %evt.time,%user.uid,%proc.name

### 查看指定容器ID
cat /var/log/sysdig | grep falco | grep "Package management" -i

# 
vim /opt/KSR00101/incidents/summary

```

### 考题5 - ServiceAccount

Context
A Pod fails to run because of an incorrectly specified ServiceAcccount.

#### Task

create a new ServiceAccount named `backend-sa` in the existing namespace `qa`, which must **not have access to any secrets**.

- Inspect the Pods in the namespace `qa`.
  - Edit the Pod to use the newly created serviceAccount `backend-sa`.
  - Ensure that the modified specification is applied and the Pod is running.
- Finally, clean-up and delete the now unused serviceAccount in the namespace `qa`.
在现有 namespace `qa` 中创建一个名为 `backend-sa` 的新 ServiceAccount， 确保此 ServiceAccount 不自动挂载secrets。
使用 `/cks/9/pod9.yaml` 中的清单文件来创建一个 Pod。
最后，清理 namespace `qa` 中任何未使用的 ServiceAccount。

#### Solution

搜索 serviceaccount（为Pod配置服务账号），接着再搜索字符串 “automount”
<https://kubernetes.io/zh-cn/docs/tasks/configure-pod-container/configure-service-account/>

```bash
### 创建 ServiceAccount
kubectl apply -f - <<EOF
apiVersion: v1
kind: ServiceAccount
metadata:
  name: backend-sa
  namespace: qa
automountServiceAccountToken: false
EOF

### 
k get pods -n qa
  web1-xxx1
  web2-xwx2
  web3-xwx3
k get deployment -n qa
  web1
  web2
  web3
# 发现这些pod都属于deployment

### 编辑 Pod 使用新创建的 serviceaccount
k edit deployment/web1 -n qa
k edit deployment/web2 -n qa
k edit deployment/web3 -n qa

...
template:
  spec:
    serviceAccountName: backend-sa # add
...

### 应用清单文件
kubectl apply -f /cks/9/pod9.yaml

### 把除了 backend-sa, 并且没有被使用的 serviceaccount 都删除
kubectl get secret -n qa
    backend-sa
    default
    contentsa

kubectl get rolebinding -n qa -o wide
kubectl get clustorrolebinding -n qa -o wide

kubectl delete -n qa serviceaccount contentsa

```

### 考题6 - 2022真题v1.20 Pod 安全策略-PodSecurityPolicy

2023的最新考试已经没有这道题了，替代的是Pod Security Standard

#### Context6

A PodsecurityPolicy shall prevent the creation on of privileged Pods in a specific namespace.
PodSecurityPolicy 应防止在特定 namespace 中特权 Pod 的创建。

#### Task6

Create a new `PodSecurityPolicy` named `restrict-policy`, which prevents the creation of privileged Pods.

Create a new `ClusterRole` named `restrict-access-role`, which uses the newly created PodSecurityPolicy `restrict-policy`.
Create a new `serviceAccount` named `psp-denial-sa` in the existing namespace `staging`.

Finally, create a new `clusterRoleBinding` named `dany-access-bind`, which binds the newly created ClusterRole `restrict-access-role` to the newly created serviceAccount `psp-denial-sa`.

创建一个名为 `restrict-policy` 的新的 PodSecurityPolicy，以防止特权 Pod 的创建。
创建一个名为 `restrict-access-role` 并使用新创建的 PodSecurityPolicy `restrict-policy` 的 ClusterRole。
在现有的 namespace `staging` 中创建一个名为 `psp-denial-sa` 的新 ServiceAccount 。
最后，创建一个名为 `dany-access-bind` 的 ClusterRoleBinding，将新创建的 ClusterRole `restrict-access-role` 绑定到新创建的 ServiceAccount `psp-denial-sa`。
你可以在一下位置找到模版清单文件： `/cks/psp/psp.yaml`

#### Solution6

搜索 runasany（Pod Security Policy）
<https://kubernetes.io/id/docs/concepts/policy/pod-security-policy/>
搜索 clusterrole（使用RBAC鉴权）
<https://kubernetes.io/zh-cn/docs/reference/access-authn-authz/rbac/>

```bash
### (1)创建 psp
vim /cks/psp/psp.yaml
apiVersion: policy/v1beta1
kind: PodSecurityPolicy
metadata:
  name: restrict-policy
spec:
  privileged: false
  seLinux:
    rule: RunAsAny
  supplementalGroups:
    rule: RunAsAny
  runAsUser:
    rule: RunAsAny
  fsGroup:
    rule: RunAsAny
  volumes:
  - '*'

kubectl apply -f /cks/psp/psp.yaml

### (2)创建 clusterrole，使用 psp
kubectl create clusterrole restrict-access-role --verb=use --resource=psp --resource-name=restrict-policy

### (3)创建 serviceaccount
kubectl create serviceaccount psp-denial-sa -n staging 

### (4)创建 clusterrolebinding
kubectl create clusterrolebinding dany-access-bind --clusterrole=restrict-access-role --serviceaccount=staging:psp-denial-sa

### (5)启用 PodSecurityPolicy（在控制节点上修改 apiserver 配置）
vim /etc/kubernetes/manifests/kube-apiserver.yaml
    - --enable-admission-plugins=NodeRestriction,PodSecurityPolicy

systemctl restart kubelet

```

### 考题6 - 2023真题V1.26 Pod Security Standard

Task weight: 8%
Use context: `kubectl config use-context workload-prod`

There is Deployment `container-host-hacker` in Namespace `team-red` which mounts `/run/containerd` as a hostPath volume on the Node where it's running. This means that the Pod can access various data about other containers running on the same Node.

To prevent this configure Namespace `team-red` to `enforce` the `baseline` Pod Security Standard. Once completed, delete the Pod of the Deployment mentioned above.

Check the `ReplicaSet` events and write the event/log lines containing the reason why the Pod isn't recreated into `/opt/course/4/logs`.

#### Answer

Making Namespaces use Pod Security Standards works via labels. We can simply edit it:

```bash
k edit ns team-red
```

Now we configure the requested label:

```yaml
# kubectl edit namespace team-red
apiVersion: v1
kind: Namespace
metadata:
  labels:
    kubernetes.io/metadata.name: team-red
    pod-security.kubernetes.io/enforce: baseline # add
  name: team-red
...
```

This should already be enough for the default Pod Security Admission Controller to pick up on that change. Let's test it and delete the Pod to see if it'll be recreated or fails, it should fail!

```bash
➜ k -n team-red get pod
NAME                                    READY   STATUS    RESTARTS   AGE
container-host-hacker-dbf989777-wm8fc   1/1     Running   0          115s

➜ k -n team-red delete pod container-host-hacker-dbf989777-wm8fc 
pod "container-host-hacker-dbf989777-wm8fc" deleted

➜ k -n team-red get pod
No resources found in team-red namespace.
```

Usually the ReplicaSet of a Deployment would recreate the Pod if deleted, here we see this doesn't happen. Let's check why:

```bash
➜ k -n team-red get rs
NAME                              DESIRED   CURRENT   READY   AGE
container-host-hacker-dbf989777   1         0         0       5m25s

➜ k -n team-red describe rs container-host-hacker-dbf989777
Name:           container-host-hacker-dbf989777
Namespace:      team-red
...
Events:
  Type     Reason            Age                   From                   Message
  ----     ------            ----                  ----                   -------
...
  Warning  FailedCreate      2m41s                 replicaset-controller  Error creating: pods "container-host-hacker-dbf989777-bjwgv" is forbidden: violates PodSecurity "baseline:latest": hostPath volumes (volume "containerdata")
  Warning  FailedCreate      2m2s (x9 over 2m40s)  replicaset-controller  (combined from similar events): Error creating: pods "container-host-hacker-dbf989777-kjfpn" is forbidden: violates PodSecurity "baseline:latest": hostPath volumes (volume "containerdata")
```

There we go! Finally we write the reason into the requested file so that Mr Scoring will be happy too!

```bash
# /opt/course/4/logs
Warning  FailedCreate      2m2s (x9 over 2m40s)  replicaset-controller  (combined from similar events): Error creating: pods "container-host-hacker-dbf989777-kjfpn" is forbidden: violates PodSecurity "baseline:latest": hostPath volumes (volume "containerdata")
```

Pod Security Standards can give a great base level of security! But when one finds themselves wanting to deeper adjust the levels like `baseline` or `restricted`... this isn't possible and 3rd party solutions like OPA could be looked at.

### 考题7 - NetworkPolicy - default-deny

#### Context

A default-deny NetworkPolicy avoids to accidentally expose a Pod in a namespace that doesn't have any other NetworkPolicy defined.
一个默认拒绝（default-deny）的 NetworkPolicy 可避免在未定义任何其他 NetworkPolicy 的 namespace 中意外公开 Pod。

#### Task

Create a new default-deny NetworkPolicy named `denynetwork` in the namespace `development` for all traffic of type `Ingress`.
The new NetworkPolicy must deny all ingress traffic in the namespace `development`.

Apply the newly created `default-deny` NetworkPolicy to all Pods running in namespace `development`.
You can find a skeleton manifest file at `/cks/15/p1.yaml`

为所有类型为 Ingress+Egress 的流量在 namespace testing 中创建一个名为 `denynetwork` 的新默认拒绝 NetworkPolicy。 此新的 NetworkPolicy 必须拒绝 namespace testng 中的所有的 Ingress + Egress 流量。
将新创建的默认拒绝 NetworkPolicy 应用与在 namespace testing 中运行的所有 Pod。
你可以在 `/cks/15/p1.yaml` 找到一个模板清单文件。

```bash
### 修改模板清单文件
vim /cks/15/p1.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: denynetwork
  namespace: testing
spec:
  podSelector: {}
  policyTypes:
  - Ingress

### 应用清单文件
kubectl apply -f /cks/15/p1.yaml
```

### 考题8 - NetworkPolicy

#### Task

create a NetworkPolicy named `pod-restriction` to restrict access to Pod `products-service` running in namespace `dev-team`.
Only allow the following Pods to connect to Pod `products-service`:

- Pods in the namespace `qa`
- Pods with label `environment: testing`, in any namespace

Make sure to apply the NetworkPolicy.
You can find a skelet on manifest file at `/cks/6/p1.yaml`

创建一个名为 `pod-restriction` 的 NetworkPolicy 来限制对在 namespace `dev-team` 中运行的 Pod `products-service` 的访问。只允许以下 Pod 连接到 Pod `products-service`：

- namespace `qa` 中的 Pod
- 位于任何 namespace，带有标签 `environment: testing` 的 Pod

注意：确保应用 NetworkPolicy。
你可以在`/cks/net/po.yaml` 找到一个模板清单文件。

#### Solution

搜索 networkpolicy（网络策略）
<https://kubernetes.io/zh-cn/docs/concepts/services-networking/network-policies/>

```bash
### (1)查看命名空间 qa 具有的标签
kubectl get namespace qa --show-labels

### (2)查看 pod 具有的标签
kubectl get pod products-service -n dev-team --show-labels

### 修改模板清单文件
vim /cks/net/po.yaml
```

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: pod-restriction  # name
  namespace: dev-team  # namespace
spec:
  podSelector:
    matchLabels:
      run: products-service  # (2)
  policyTypes:
  - Ingress
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          name: qa  # (1)
    - podSelector:  # 注意带 - ，表示或的关系
        matchLabels:
          environment: testing
      namespaceSelector: {}    ## 任何命名空间, 不带 - ，且的关系
```

```bash
### 应用清单文件
kubectl apply -f /cks/net/po.yaml
```

### 考题9 - RBAC

#### Context

绑定到 Pod 的 ServiceAccount 的 Role 授予过度宽松的权限。完成以下项目以减少权限集。
A Role bound to a Pod's serviceAccount grants overly permissive permissions.
Complete the following tasks to reduce the set of permissions.

#### Task

一个名为 `web-pod` 的现有 Pod 已在 namespace `db` 中运行。编辑绑定到 Pod 的 ServiceAccount `service-account-web` 的现有 Role， 仅允许只对 services 类型的资源执行 `get` 操作。

- 在 namespace `db` 中创建一个名为 `role-2` ，并仅允许只对 `namespaces` 类型的资源执行 `delete` 操作的新 Role。
- 创建一个名为 `role-2-binding` 的新 RoleBinding，将新创建的 Role 绑定到 Pod 的 ServiceAccount。
注意：请勿删除现有的 RoleBinding。

Given an existing Pod named `web-pod` running in the namespace `db`. Edit the existing Role bound to the Pod's serviceAccount `sa-dev-1` to only allow performing `list` operations, only on resources of type `Endpoints`.

- create a new Role named `role-2` in the namespace `db`, which only allows performing `update` operations, only on resources of type `persistentvolumeclaims`
- create a new RoleBinding named `role-2-binding` binding the newly created Role to the Pod's serviceAccount.

Don't delete the existing RoleBinding

#### solution

搜索 clusterrole（使用RBAC鉴权）
<https://kubernetes.io/zh-cn/docs/reference/access-authn-authz/rbac/>

```bash
### 查询 sa 对应的 role 名称（假设是 role-1）
kubectl get rolebinding -n db -oyaml | grep 'service-account-web' -B 10

### 修改 role 清单文件（仅允许对 services 类型的资源执行 get 操作）
kubectl edit role -n db role-1

apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: role-1
  namespace: db
  resourceVersion: "9528"
rules:
- apiGroups:
    - ""
  resources:
    - services
  verbs:
    - get

### 创建新角色 role-2（仅允许只对 namespaces 类型的资源执行 delete 操作）
kubectl create role role-2 -n db --verb=delete --resource=namespaces

### 创建 rolebinding，并绑定到 sa 上
kubectl create rolebinding role-2-binding --role=role-2 --serviceaccount=db:service-account-web

```

### 考题10 - kube-apiserver 审计日志记录和采集

#### Task

Enable audit logs in the cluster.
To do so, enable the log backend, and ensure that:

- logs are stored at `/var/log/kubernetes/audit-logs.txt`
- log files are retained for `10` days
- at maximum, a number of `2` auditlog files are retained
A basic policy is provided at `/etc/kubernetes/logpolicy/sample-policy.yaml`. it only specifies what not to log. The base policy is located on the cluster's `master` node.

Edit and extend the basic policy to log:

- `namespaces` changes at `RequestResponse` level
- the request body of pods changes in the namespace `front-apps`
- `configMap` and `secret` changes in all namespaces at the `Metadata` level
- Also, add a `catch-all` ruie to log all other requests at the `Metadata` level.

Don't forget to apply the modifiedpolicy.
`/etc/kubernetes/logpolicy/sample-policy.yaml`

在 cluster 中启用审计日志。为此，请启用日志后端，并确保：

- 日志存储在 `/var/log/kubernetes/audit-logs.txt`
- 日志文件能保留 `10` 天
- 最多保留 `2` 个旧审计日志文件
/etc/kubernetes/logpolicy/sample-policy.yaml 提供了基本策略。它仅指定不记录的内容。
注意：基本策略位于 cluster 的 master 节点上。

编辑和扩展基本策略以记录：

- RequestResponse 级别的 cronjobs 更改
- namespace front-apps 中 deployment 更改的请求体
- Metadata 级别的所有 namespace 中的 ConfigMap 和 Secret 的更改
- 此外，添加一个全方位的规则以在 Metadata 级别记录所有其他请求。
注意：不要忘记应用修改后的策略

#### Solution

搜索 audit（审计）
<https://kubernetes.io/zh-cn/docs/tasks/debug/debug-cluster/audit/>

```bash
### 如果没有 /var/log/kubernetes/，则创建目录
mkdir /var/log/kubernetes/

### 修改 audit 模板文件
vim /etc/kubernetes/logpolicy/sample-policy.yaml

apiVersion: audit.k8s.io/v1
kind: Policy
omitStages:
  - "RequestReceived"
rules:
  - level: RequestResponse
    resources:
    - group: ""
      resources: ["cronjobs"]
  - level: Request
    resources:
    - group: ""
      resources: ["deployments"]
    namespaces: ["front-apps"]
  - level: Metadata
    resources:
    - group: ""
      resources: ["secrets", "configmaps"]
  - level: Metadata
    omitStages:
      - "RequestReceived"

### 修改 apiserver 配置文件，启用审计日志
vim /etc/kubernetes/manifests/kube-apiserver.yaml
--audit-policy-file=/etc/kubernetes/logpolicy/sample-policy.yaml
--audit-log-path=/var/log/kubernetes/audit-logs.txt
--audit-log-maxage=10
--audit-log-maxbackup=2

### 在 apiserver 的 Pod 上挂载策略文件和日志文件所在的目录（考试时可能已经挂载好）
vim /etc/kubernetes/manifests/kube-apiserver.yaml
volumeMounts:
  - mountPath: /var/log/kubernetes
    name: kubernetes-logs
  - mountPath: /etc/kubernetes/logpolicy
    name: kubernetes-policy
volumes:
- name: kubernetes-logs
  hostPath:
    path: /var/log/kubernetes
- name: kubernetes-policy
  hostPath:
    path: /etc/kubernetes/logpolicy

### 重载生效配置
systemctl daemon-reload
systemctl restart kubelet

```

### 考题11 - Secret

#### Task

Retrieve the content of the existing secret named `db1-test` in the `istio-system` namespace.
store the username field in a file named `/home/candidate/user.txt`, and the password field in a file named `/home/candidate/pass`.txt.

You must create both files; they don't exist yet.
Do not use/modify the created files in the following steps, create new temporary files if needed.

Create a new secret named `db2-test` in the `istio-system` namespace, with the following

```yaml
username : production-instance
password : KvLftKgs4aVH
```

Finally, create a new Pod that has access to the secret db2-test via a volume:

- Pod name `secret-pod`
- Namespace `istio-system`
- container name `dev-container`
- image `nginx`
- volume name `secret-volume`
- mount path `/etc/secret`

在 namespace `istio-system` 中获取名为 `db1-test` 的现有 secret 的内容.
将 username 字段存储在名为 `/cks/sec/user.txt` 的文件中，并将 password 字段存储在名为 `/cks/sec/pass.txt` 的文件中。

注意：你必须创建以上两个文件，他们还不存在。
注意：不要在以下步骤中使用/修改先前创建的文件，如果需要，可以创建新的临时文件。

在 `istio-system` namespace 中创建一个名为 `db2-test` 的新 secret，内容如下：

```yaml
username : production-instance
password : KvLftKgs4aVH
```

最后，创建一个新的 Pod，它可以通过卷访问 secret `db2-test` ：

- Pod 名称 `secret-pod`
- Namespace `istio-system`
- 容器名 `dev-container`
- 镜像 `nginx`
- 卷名 `secret-volume`
- 挂载路径 `/etc/secret`

#### Solution

搜索 secret（使用 kubectl 管理 Secret）
<https://kubernetes.io/zh-cn/docs/tasks/configmap-secret/managing-secret-using-kubectl/>
搜索 secret（Secret）
<https://kubernetes.io/zh-cn/docs/concepts/configuration/secret/>

```bash
### 检索已存在的 secret，将获取到的用户名和密码字段存储到指定文件
kubectl get secrets db2-test -o jsonpath='{.data.username}' | base64 -d > /home/candidate/user.txt
kubectl get secrets db2-test -o jsonpath='{.data.password}' | base64 -d > /home/candidate/pass.txt

### 创建 secret
kubectl create secret generic db2-test -n istio-system --from-literal=username=production-instance --from-literal=password=KvLftKgs4aVH 

### 在 Pod 中以文件形式使用 Secret
vim k8s-secret.yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-pod
  namespace: istio-system
spec:
  containers:
  - name: dev-container
    image: nginx
    volumeMounts:
    - name: secret-volume
      mountPath: "/etc/secret"
      readOnly: true
  volumes:
  - name: secret-volume
    secret:
      secretName: db2-test
      optional: false

### 应用清单文件
kubectl apply -f k8s-secret.yaml

### 验证 pod
kubectl get pods -n istio-system dev-pod
```

### 考题12 - dockerfile 和 deployment 安全优化

open policyagent/conftest test deploy.yaml
open policyagent/conftest test myapp.dockerfile

#### Task

- 分析和编辑给定的 Dockerfile `/cks/docker/Dockerfile`（基于 ubuntu:16.04 镜像），并修复在文件中拥有的突出的安全/最佳实践问题的两个指令。
- 分析和编辑给定的清单文件 `/cks/docker/deployment.yaml`，并修复在文件中拥有突出的安全/最佳实践问题的两个字段。

注意：请勿添加或删除配置设置；只需修改现有的配置设置让以上两个配置设置都不再有安全/最佳实践问题。
注意：如果您需要非特权用户来执行任何项目，请使用用户 ID 65535 的用户 nobody 。
答题： 注意，本次的 Dockerfile 和 deployment.yaml 仅修改即可，无需部署。

- Analyze and edit the given Dockerfile (based on the ubuntu:16.04 image) `/cks/7/Dockerfile` fixing two instructions present in the file being prominent security/best-practice issues.
- Analyze and edit the given manifest file `/cks/7/deployment.yaml` fixing two fields present in the file being prominent security/best-practice issues.

Don't add or remove configuration settings; only modify the existing configuration settings, so that two configuration settings each are no longer security/best-practice concerns.

Should you need an unprivileged user for any of the tasks, use user `nobody` with user id `65536`.

#### Solution 12

```bash
### 修复 dockerfile 文件中存在的两个安全/最佳实践指令
### (1)把ubuntu:latest改为ubuntu:16.04 (2)将 root 注释掉；增加 nobody
vim /cks/docker/Dockerfile
# FROM ubuntu:latest  1 修改
FROM ubuntu:16.04
#USER root 
USER nobody # 2

### 修复 deployment 文件中存在的两个安全/最佳实践问题字段
### (1)将 privileged 变为 False；(2)将 readOnlyRootFilesystem 变为 True
vim /cks/docker/deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: dev
  name: dev
spec:
  replicas: 1
  selector:
    matchLabels:
      app: dev
  template:
    metadata:
      labels:
        app: dev
    spec:
      containers:
      - image: mysql
        name: mysql
        securityContext: {'capabilities':{'add':['NET_ADMIN'],'drop':['all']},'privileged': False,'readOnlyRootFilesystem': True, 'runAsUser': 65535}
```

### 考题13 - admission-controllers - ImagePolicyWebhook

#### Context

A container image scanner is set up on the cluster, but it's not yet fully integrated into the cluster's configuration. When complete, the container image scanner shall scan for and reject the use of vulnerable images.

cluster 上设置了容器镜像扫描器，但尚未完全集成到 cluster 的配置中。完成后，容器镜像扫描器应扫描并拒绝易受攻击的镜像的使用。

#### Task

You have to complete the entire task on the cluster's `master` node, where all services and files have been prepared and placed.
Given an incomplete configuration in directory `/etc/kubernetes/epconfig` and a functional container image scanner with HTTPS endpoint `https://acme.local:8082/image_policy`:

1. Enable the necessary plugins to create an image policy
2. validate the control configuration and change it to an implicit deny
3. Edit the configuration to point to the provided HTTPS endpoint correctly.
4. Finally , test if the configuration is working by trying to deploy the vulnerable resource  `/cks/1/web1.yaml`

You can find the container image scanner's log file at `/var/loglimagepolicyiacme.log`

注意：你必须在 cluster 的 master 节点上完成整个考题，所有服务和文件都已被准备好并放置在该节点上。 给定一个目录 `/etc/kubernetes/epconfig` 中不完整的配置以及具有 HTTPS 端点 `https://acme.local:8082/image_policy` 的功能性容器镜像扫描器：

1. 启用必要的插件来创建镜像策略
2. 校验控制配置并将其更改为隐式拒绝（implicit deny）
3. 编辑配置以正确指向提供的 HTTPS 端点
4. 最后，通过尝试部署易受攻击的资源 `/cks/img/web1.yaml` 来测试配置是否有效。

你可以在 `/var/log/imagepolicy/roadrunner.log` 找到容器镜像扫描仪的日志文件。

#### Solution

搜索 imagepolicywebhook（使用准入控制器），接着再搜索字符串"imagepolicywebhook"
<https://kubernetes.io/zh-cn/docs/reference/access-authn-authz/admission-controllers/>

```bash
### (1)修改不完整的配置
cd /etc/kubernetes/epconfig
ls

### (2)验证控制平面的配置并将其更改为拒绝
vim admission_configuration.json
```

```json
{
   "apiVersion": "apiserver.config.k8s.io/v1",
   "kind": "AdmissionConfiguration",
   "plugins": [
      {
         "name": "ImagePolicyWebhook",
         "configuration": {
            "imagePolicy": {
               "kubeConfigFile": "/etc/kubernetes/epconfig/kubeconfig.yaml", // kubeconfig
               "allowTTL": 100,
               "denyTTL": 50,
               "retryBackoff": 500,
               "defaultAllow": false   // 2.modify from true to false
            }
         }
      }
   ]
}
```

```bash
### (3)编辑配置以正确指向提供的 HTTPS 端点
vim kubeconfig.yaml
    apiVersion: v1
    kind: Config
    clusters:
    - cluster:
        certificate-authority: /etc/kubernetes/epconfig/webhook.pem
        server: https://acme.local:8082/image_policy   # 配置此步
    name: bouncer_webhook

### (4)启用必要的插件以创建镜像策略
vim /etc/kubernetes/manifests/kube-apiserver.yaml

    - --enable-admission-plugins=NodeRestriction,ImagePolicyWebhook
    - --admission-control-config-file=/etc/kubernetes/epconfig/admission_configuration.json
    ......
    volumeMounts:
    - mountPath: /etc/kubernetes/epconfig
      name: config
      readyOnly: true
  volumes:
  - hostPath:
      path: /etc/kubernetes/epconfig
      type: DirectoryOrCreate
    name: config

### (5)加载生效配置
systemctl daemon-reload
systemctl restart kubelet

### (6)通过部署易受攻击的资源来测试配置是否有效
kubectl apply -f /cks/img/web1.yaml
```

### 考题14 - 删除非无状态或非不可变的 pod

Context: it is best-practice to design containers to be stateless and immutable

#### Task

Inspect Pods runnings in namespace `production` and delete any Pod that is either not stateless or not immutable.

Use the following strict interpretation of stateless and immutable:

- Pod being able to store data inside containers must be treated as not stateless. You don't have to worry whether data is actually stored inside containers or not already.
- Pod being configured to be `privileged` in any way must be treated as potentially not stateless and not immutable.

检查在 namespace production 中运行的 Pod，并删除任何非无状态或非不可变的 Pod。
使用以下对无状态和不可变的严格解释：

- 能够在容器内存储数据的 Pod 的容器必须被视为非无状态的。
- 被配置为任何形式的特权 Pod 必须被视为可能是非无状态和非不可变的。
注意：你不必担心数据是否实际上已经存储在容器中。

```bash
### 在命名空间 dev 中检查 running 状态的 pod
kubectl get pods -n production | grep running

### 查看具有特权的 pod
kubectl get pods -n production -oyaml | grep -i "privileged: true"

### 查看具有 volume 的 pod
# jq 用于处理JSON输入，将给定过滤器应用于其JSON文本输入并在标准输出上将过滤器的结果生成为JSON。
kubectl get pods -n production -o jsonpath={.spec.volumes} | jq

### 将查询到的具有特权和 volume 的 pod 都删除
kubectl delete pods -n production pod名称

```

### 考题15 - gVisor/runtimeclass

#### Context

该 cluster 使用 containerd 作为 CRI 运行时。
containerd 的默认运行时处理程序是 `runc`。 containerd 已准备好支持额外的运行时处理程序 `runsc` (gVisor)。

This cluster uses containerd as CRI runtime.
Containerd's default runtime handler is `runc` . Containerd has been prepared to support an additional runtime handler , `runsc` (gVisor).

#### Task

使用名为 `runsc` 的现有运行时处理程序，创建一个名为 `untrusted` 的 RuntimeClass。
更新 namespace `server` 中的所有 Pod 以在 gVisor 上运行。
您可以在 `/cks/gVisor/rc.yaml` 中找到一个模版清单

Create a RuntimeClass named `untrusted` using the prepared runtime handler named `runsc`.
Update all Pods in the namespace `client` to run on gvisor, unless they are already running on `anon-default` runtime handler.
You can find a skeleton manifest file at `/cks/13/rc.yaml`

#### Solution

搜索 runtimeclass（容器运行时类）
<https://kubernetes.io/zh-cn/docs/concepts/containers/runtime-class/>

```bash
### 修改模板清单文件
vim /cks/gVisor/rc.yaml
    apiVersion: node.k8s.io/v1
    kind: RuntimeClass
    metadata:
      name: untrusted
    handler: runsc

### 应用清单文件
kubectl apply -f /cks/gVisor/rc.yaml

### 修改 server 命名空间下的所有 pod（还需要修改deployment）
kubectl get pods -n server -oyaml > myrc.yaml
vim myrc.yaml
spec:
  ......
  runtimeClassName: untrusted

### 更新清单文件
kubectl delete -f myrc.yaml
kubectl apply -f myrc.yaml
```

### 考题16 - 启用 API Server 认证

#### Context

由 kubeadm 创建的 cluster 的 Kubernetes API 服务器，出于测试目的，临时配置允许未经身份验证和未经授权的访问，授予匿名用户 `cluster-admin` 的访问权限。

#### Task

重新配置 cluster 的 Kubernetes API 服务器，以确保**只允许经过身份验证和授权**的 REST 请求。
使用授权模式 `Node`,`RBAC` 和准入控制器 `NodeRestriction。`
删除用户 `system:anonymous` 的 ClusterRoleBinding 来进行清理。
注意：所有 kubectl 配置环境/文件也被配置使用未经身份验证和未经授权的访问。 你不必更改它，但请注意，一旦完成 cluster 的安全加固， kubectl 的配置将无法工作。 您可以使用位于 cluster 的 master 节点上，cluster 原本的 kubectl 配置文件 /etc/kubernetes/admin.conf ，以确保经过身份验证的授权的请求仍然被允许。

```bash
k get nodes

### 注意：修改 master 节点！
ssh masterNode

### (1)使用授权模式 Node,RBAC 和准入控制器 NodeRestriction
vim /etc/kubernetes/manifests/kube-apiserver.yaml
    - --authorization-mode=Node,RBAC
    - --enable-admission-plugins=NodeRestriction
    - --client-ca-file=/etc/kubernetes/pki/ca.crt
    - --enable-bootstrap-token-auth=true

### (2)删除 system:anonymous 的 ClusterRolebinding 角色绑定（取消匿名用户的集群管理员权限）
k get clusterrolebinding | grep system:anonymous
kubectl delete clusterrolebinding system:anonymous
```

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
