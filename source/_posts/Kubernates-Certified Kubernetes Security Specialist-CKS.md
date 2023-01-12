---
title: 2023 CKS v1.25 考试真题整理
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
    - [CKS CKA CKAD changed Terminal to Remote Desktop ](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e)
- CKS考试66分以上即可通过，考试不通过有一次补考机会。

### More items for CKS than CKA and CKAD

- Pod Security Policies(PSP) - removed from Kubernetes in `v1.25`
- [AppArmor](https://kubernetes.io/docs/tutorials/security/apparmor/)
- Apiserver
  - Apiserver Crash
  - Apiserver NodeRestriction
- ImagePolicyWebhook
- [kube-bench](https://github.com/aquasecurity/kube-bench)
- [Trivy](https://github.com/aquasecurity/trivy)

### Pod Security Policies(PSP)

Reference:
- [k8s Pod Security Policy官方文档](https://kubernetes.io/docs/concepts/security/pod-security-policy/)
  - [PodSecurityPolicy Deprecation: Past, Present, and Future](https://kubernetes.io/zh-cn/blog/2021/04/06/podsecuritypolicy-deprecation-past-present-and-future/)
- [aws eks 官方文档](https://docs.aws.amazon.com/eks/latest/userguide/pod-security-policy.html)
- [PodSecurityPolicy is Dead, Long Live…?](https://www.appvia.io/blog/podsecuritypolicy-is-dead-long-live/)
- https://docs.bitnami.com/kubernetes/faq/configuration/understand-pod-security-policies/


> Removed feature
> PodSecurityPolicy was deprecated in Kubernetes `v1.21`, and removed from Kubernetes in `v1.25`.
> Use [`Pod Security Admission`](https://kubernetes.io/docs/concepts/security/pod-security-admission/)instead.

A Pod Security Policy is a **cluster-level** resource that controls security sensitive aspects of the **pod** specification.

### [AppArmor](https://kubernetes.io/docs/tutorials/security/apparmor/)

[Manage AppArmor profiles and Pods using these](https://killercoda.com/killer-shell-cks/scenario/apparmor)

![apparmor1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor1-Check%20existing%20AppArmor%20profiles.png)

![apparmor1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor2-deployment.png)

![AppArmor2-deployment2.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor2-deployment2.png)

![AppArmor2-deployment3beforeChange.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor2-deployment3beforeChange.png)

![AppArmor2-deployment4.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor2-deployment4.png)

![AppArmor2-deployment5.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor2-deployment5.png)

![AppArmor3-install profile.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor3-install%20profile.png)

### Apiserver Crash

[Crash that Apiserver and check them logs](https://killercoda.com/killer-shell-cks/scenario/apiserver-crash)

kube-apiserver.yaml Location: `/etc/kubernetes/manifests/kube-apiserver.yaml`

Log locations to check:

- `/var/log/pods`
- `/var/log/containers`
- `crictl ps` + `crictl logs`
- `docker ps` + `docker logs` (in case when Docker is used)
- kubelet logs: `/var/log/syslog` or `journalctl`

```bash
# smart people use a backup
cp ~/kube-apiserver.yaml.ori /etc/kubernetes/manifests/kube-apiserver.yaml

# wait till container restarts
watch crictl ps

# check for apiserver pod
k -n kube-system get pod
```

Give the Apiserver some time to restart itself, like 1-2 minutes. If it doesn't restart by itself you can also force it with:
- 1: `mv /etc/kubernetes/manifests/kube-apiserver.yaml /tmp/kube-apiserver.yaml`
- 2: wait till container is removed with `watch crictl ps`
- 3: `mv /tmp/kube-apiserver.yaml /etc/kubernetes/manifests/kube-apiserver.yaml`

#### Configure a wrong argument

The idea here is to misconfigure the Apiserver in different ways, then check possible log locations for errors.

You should be very comfortable with situations where the Apiserver is not coming back up.

Configure the Apiserver manifest with a new argument `--this-is-very-wrong` .

Check if the Pod comes back up and what logs this causes.

Fix the Apiserver again.

```bash
# always make a backup !
cp /etc/kubernetes/manifests/kube-apiserver.yaml ~/kube-apiserver.yaml.ori

# make the change
vim /etc/kubernetes/manifests/kube-apiserver.yaml

# wait till container restarts
watch crictl ps

# check for apiserver pod
k -n kube-system get pod
```

Apiserver is not coming back, we messed up!

```bash
# check pod logs
cat /var/log/pods/kube-system_kube-apiserver-controlplane_a3a455d471f833137588e71658e739da/kube-apiserver/X.log
> 2022-01-26T10:41:12.401641185Z stderr F Error: unknown flag: --this-is-very-wrong
```

Now undo the change and continue

```bash
# smart people use a backup
cp ~/kube-apiserver.yaml.ori /etc/kubernetes/manifests/kube-apiserver.yaml

# wait till container restarts
watch crictl ps

# check for apiserver pod
k -n kube-system get pod
```

#### Misconfigure ETCD connection

Change the existing Apiserver manifest argument to: `--etcd-servers=this-is-very-wrong` .

Check what the logs say, without using anything in `/var` .

Fix the Apiserver again.

```bash
# always make a backup !
cp /etc/kubernetes/manifests/kube-apiserver.yaml ~/kube-apiserver.yaml.ori

# make the change
vim /etc/kubernetes/manifests/kube-apiserver.yaml

# wait till container restarts
watch crictl ps

# check for apiserver pod
k -n kube-system get pod
```

Apiserver is not coming back, we messed up!

```bash
# 1) if we would check the /var directory
cat /var/log/pods/kube-system_kube-apiserver-controlplane_e24b3821e9bdc47a91209bfb04056993/kube-apiserver/X.log
> Err: connection error: desc = "transport: Error while dialing dial tcp: address this-is-very-wrong: missing port in address". Reconnecting...

# 2) but here we want to find other ways, so we check the container logs
crictl ps # maybe run a few times, because the apiserver container get's restarted
crictl logs f669a6f3afda2 # pod ID
> Error while dialing dial tcp: address this-is-very-wrong: missing port in address. Reconnecting...

# 3) what about syslogs
journalctl | grep apiserver # nothing specific
cat /var/log/syslog | grep apiserver # nothing specific
```

Now undo the change and continue

```bash
# smart people use a backup
cp ~/kube-apiserver.yaml.ori /etc/kubernetes/manifests/kube-apiserver.yaml

# wait till container restarts
watch crictl ps

# check for apiserver pod
k -n kube-system get pod
```

#### Invalid Apiserver Manifest YAML

Change the Apiserver manifest and add invalid YAML, something like this:

```yaml
apiVersionTHIS IS VERY ::::: WRONG v1
kind: Pod
metadata:
```

Check what the logs say, and fix again.

Fix the Apiserver again.

Apiserver is not coming back, we messed up!

```bash
# seems like the kubelet can't even create the apiserver pod/container
/var/log/pods # nothing
crictl logs # nothing

# syslogs:
tail -f /var/log/syslog | grep apiserver
> Could not process manifest file err="/etc/kubernetes/manifests/kube-apiserver.yaml: couldn't parse as pod(yaml: mapping values are not allowed in this context), please check config file"

# or:
journalctl | grep apiserver
> Could not process manifest file" err="/etc/kubernetes/manifests/kube-apiserver.yaml: couldn't parse as pod(yaml: mapping values are not allowed in this context), please check config file
```

### [Apiserver NodeRestriction](https://killercoda.com/killer-shell-cks/scenario/apiserver-node-restriction)

[admission controller - Use the NodeRestriction Admission Controller to restrict Kubelet's permissions](https://killercoda.com/killer-shell-cks/scenario/apiserver-node-restriction)

#### Verify the issue

The Kubelet on `node01` shouldn't be able to set Node labels

- starting with `node-restriction.kubernetes.io/*`
- on other Nodes than itself （不能label其他node，只能label本node：`node01`）

Verify this is not restricted atm by performing the following actions as the Kubelet from node01 :

- add label `killercoda/one=123` to Node `controlplane`
- add label `node-restriction.kubernetes.io/one=123` to Node `node01`

Tip

We can contact the Apiserver as the Kubelet by using the Kubelet kubeconfig

```bash
export KUBECONFIG=/etc/kubernetes/kubelet.conf
k get node
```


Solution

```bash
ssh node01
    export KUBECONFIG=/etc/kubernetes/kubelet.conf
    k label node controlplane killercoda/one=123 # works but should be restricted 现在可以成功加label，但是我们应该更改配置使得它满足题目要求：be restricted
    node/controlplane labeled
    k label node node01 node-restriction.kubernetes.io/one=123 # works but should be restricted
    node/node01 labeled

    k get node --show-labels 
NAME           STATUS   ROLES           AGE   VERSION   LABELS
controlplane   Ready    control-plane   20d   v1.25.3   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,killercoda/one=123,kubernetes.io/arch=amd64,kubernetes.io/hostname=controlplane,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
node01         Ready    <none>          20d   v1.25.3   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=node01,kubernetes.io/os=linux,node-restriction.kubernetes.io/one=123

# 可以看到两个label都成功加上了
```

#### Enable the NodeRestriction Admission Controller

```bash
node01 $ exit
logout
Connection to node01 closed.
controlplane $ vim /etc/kubernetes/manifests/kube-apiserver.yaml
```

```bash
spec:
  containers:
  - command:
    - kube-apiserver
    - --advertise-address=172.30.1.2
    - --allow-privileged=true
    - --authorization-mode=Node,RBAC
    - --client-ca-file=/etc/kubernetes/pki/ca.crt
    - --enable-admission-plugins=NodeRestriction    # Add this line
    - --enable-bootstrap-token-auth=true
```

```bash
ssh node01
    export KUBECONFIG=/etc/kubernetes/kubelet.conf
    k label node controlplane killercoda/two=123 # restricted
      Error from server (Forbidden): nodes "controlplane" is forbidden: node "node01" is not allowed to modify node "controlplane"

    k label node node01 node-restriction.kubernetes.io/two=123 # restricted
      Error from server (Forbidden): nodes "node01" is forbidden: is not allowed to modify labels: node-restriction.kubernetes.io/two

    k label node node01 test/two=123 # works

    # other test
    k label node controlplane test/two=123
      Error from server (Forbidden): nodes "controlplane" is forbidden: node "node01" is not allowed to modify node "controlplane"
```

Notice that existing restricted labels won't be removed once the NodeRestriction is enabled.

### [ImagePolicyWebhook](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#imagepolicywebhook)

[Complete the ImagePolicyWebhook setup](https://killercoda.com/killer-shell-cks/scenario/image-policy-webhook-setup)

#### Complete the ImagePolicyWebhook setup

An ImagePolicyWebhook setup has been half finished, complete it:

1. Make sure `admission_config.json` points to correct kubeconfig
2. Set the `allowTTL` to `100`
3. All Pod creation should be prevented if the external service is not reachable
4. The external service will be reachable under `https://localhost:1234` in the future. It doesn't exist yet so it - shouldn't be able to create any Pods till then
5. Register the correct admission plugin in the apiserver

<details>
  <summary>Solution</summary>
  <p>

```bash
  # find admission_config.json path
  vim /etc/kubernetes/manifests/kube-apiserver.yaml
```

```bash
  # find admission_config.json path in kube-apiserver.yaml
  vim /etc/kubernetes/manifests/kube-apiserver.yaml # Find value of --admission-control-config-file
  # or
  cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep admission-control-config-file
      - --admission-control-config-file=/etc/kubernetes/policywebhook/admission_config.json

  vim /etc/kubernetes/policywebhook/admission_config.json
```

The `/etc/kubernetes/policywebhook/admission_config.json` should look like this:

```json
{
   "apiVersion": "apiserver.config.k8s.io/v1",
   "kind": "AdmissionConfiguration",
   "plugins": [
      {
         "name": "ImagePolicyWebhook",
         "configuration": {
            "imagePolicy": {
               "kubeConfigFile": "/etc/kubernetes/policywebhook/kubeconf", // 1.modify "kubeConfigFile": "/todo/kubeconf" to current
               "allowTTL": 100,  // 2.modify to 100
               "denyTTL": 50,
               "retryBackoff": 500,
               "defaultAllow": false   // 3.modify from true to false
            }
         }
      }
   ]
}
```

```bash
  vim /etc/kubernetes/policywebhook/admission_config.json
```

The `/etc/kubernetes/policywebhook/kubeconf` should contain the correct server:

```yaml
apiVersion: v1
kind: Config
clusters:
- cluster:
    certificate-authority: /etc/kubernetes/policywebhook/external-cert.pem
    server: https://localhost:1234 # 4.
  name: image-checker
...
```

5 The apiserver needs to be configured with the ImagePolicyWebhook admission plugin:

```yaml
spec:
  containers:
  - command:
    - kube-apiserver
    - --enable-admission-plugins=NodeRestriction,ImagePolicyWebhook # 5. Add ImagePolicyWebhook
    - --admission-control-config-file=/etc/kubernetes/policywebhook/admission_config.json
```

Luckily the `--admission-control-config-file` argument seems already to be configured.
  </p>
</details>

<details>
  <summary>Test your Solution</summary>
  <p>
Wait till apiserver container restarted: 

`watch crictl ps`

To test your solution you can simply try to create a Pod:

`k run pod --image=nginx`

It should throw you an error like:

```bash
Error from server (Forbidden): pods "pod" is forbidden: Post "https://localhost:1234/?timeout=30s": dial tcp 127.0.0.1:1234: connect: connection refused
```

Once that service would be implemented and if it would allow the Pod, the Pod could be created.
  </p>
</details>

### [kube-bench](https://github.com/aquasecurity/kube-bench)

[cis-benchmarks-kube-bench-fix-controlplane](https://killercoda.com/killer-shell-cks/scenario/cis-benchmarks-kube-bench-fix-controlplane)

#### Apiserver should be more conform to CIS

Use `kube-bench` to ensure `1.2.20` has status `PASS`.

Solution

Check for results

```bash
# see all
kube-bench run --targets master

# or just see the one 推荐这种方法，输出比较少，好看关键信息
kube-bench run --targets master --check 1.2.20

[INFO] 1 Master Node Security Configuration
[INFO] 1.2 API Server
[FAIL] 1.2.20 Ensure that the --profiling argument is set to false (Automated)

== Remediations master ==
1.2.20 Edit the API server pod specification file /etc/kubernetes/manifests/kube-apiserver.yaml
on the master node and set the below parameter.
--profiling=false
```

Fix the `/etc/kubernetes/manifests/kube-apiserver.yaml`

```yaml
...
containers:
  - command:
    - kube-apiserver
    - --profiling=false
...
    image: k8s.gcr.io/kube-apiserver:v1.22.2
...

```

Now wait for container to be restarted: `watch crictl ps`

#### ControllerManager should be more conform to CIS

Use `kube-bench` to ensure `1.3.2` has status `PASS`.

```bash
# 推荐这种方法，输出比较少，好看关键信息
kube-bench run --targets=master --check=1.3.2

[INFO] 1 Master Node Security Configuration
[INFO] 1.3 Controller Manager
[FAIL] 1.3.2 Ensure that the --profiling argument is set to false (Automated)

== Remediations master ==
1.3.2 Edit the Controller Manager pod specification file /etc/kubernetes/manifests/kube-controller-manager.yaml
on the master node and set the below parameter.
--profiling=false
```

Fix the /etc/kubernetes/manifests/kube-controller-manager.yaml


```yaml
...
  containers:
  - command:
    - kube-controller-manager
    - --profiling=false
...
    image: k8s.gcr.io/kube-controller-manager:v1.22.2
...
```

Now wait for container to be restarted: `watch crictl ps`

#### PKI directory should be more conform to CIS

```bash
# 推荐这种方法，输出比较少，好看关键信息
kube-bench run --check 1.1.19 --targets=master
[INFO] 1 Master Node Security Configuration
[INFO] 1.1 Master Node Configuration Files
[FAIL] 1.1.19 Ensure that the Kubernetes PKI directory and file ownership is set to root:root (Automated)

== Remediations master ==
1.1.19 Run the below command (based on the file location on your system) on the master node.
For example,
chown -R root:root /etc/kubernetes/pki/
```

Fix the /etc/kubernetes/pki/

```bash
chgrp root /etc/kubernetes/pki/

# or
chown -R root:root /etc/kubernetes/pki/
```

### [Trivy](https://github.com/aquasecurity/trivy)

[Image Vulnerability Scanning Trivy](https://killercoda.com/killer-shell-cks/scenario/image-vulnerability-scanning-trivy)
#### Use trivy to scan images for known vulnerabilities

Using `trivy` :
Scan images in Namespaces `applications` and `infra` for the vulnerabilities `CVE-2021-28831` and `CVE-2016-9841` .

Scale those Deployments containing any of these down to `0` .


Solution:

First we check the applications Namespace.

```bash
# find images
k -n applications get pod -oyaml | grep image:

# scan first deployment
trivy image nginx:1.19.1-alpine-perl | grep CVE-2021-28831
31.00 MiB / 31.00 MiB [---------------------------------------------------------------------------------------------------] 100.00% 8.41 MiB p/s 4s
| busybox      | CVE-2021-28831   |          | 1.31.1-r9         | 1.31.1-r10    | busybox: invalid free or segmentation |
| ssl_client   | CVE-2021-28831   | HIGH     | 1.31.1-r9         | 1.31.1-r10    | busybox: invalid free or segmentation |

trivy image nginx:1.19.1-alpine-perl | grep CVE-2016-9841

# scan second deployment
trivy image nginx:1.20.2-alpine | grep CVE-2021-28831
trivy image nginx:1.20.2-alpine | grep CVE-2016-9841

# hit on the first one, so we scale down
$ k -n applications get deploy
NAME   READY   UP-TO-DATE   AVAILABLE   AGE
web1   2/2     2            2           6m53s
web2   1/1     1            1           6m53s

$ k -n applications get deploy web1 -oyaml | grep nginx:1.19.1-alpine-perl
      - image: nginx:1.19.1-alpine-perl
$ k -n applications get deploy web2 -oyaml | grep nginx:1.19.1-alpine-perl

k -n applications get deploy web1 
NAME   READY   UP-TO-DATE   AVAILABLE   AGE
web1   2/2     2            2           13m

k -n applications scale deploy web1 --replicas 0

$ k -n applications get deploy web1
NAME   READY   UP-TO-DATE   AVAILABLE   AGE
web1   0/0     0            0           13m
```

Next we check the infra Namespace.

```bash
# find images
k -n infra get pod -oyaml | grep image:

# scan deployment
trivy image httpd:2.4.39-alpine | grep CVE-2021-28831
trivy image httpd:2.4.39-alpine | grep CVE-2016-9841

# hit, so we scale down
$ k -n infra get deployments.apps 
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
inf-hjk   3/3     3            3           16m

k -n infra scale deploy inf-hjk --replicas 0

$ k -n infra get deployments.apps 
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
inf-hjk   0/0     0            0           18m
```

### TODO



## 如何备考

### [k8s练习环境](./Kubernates-Certified-Kubernetes-Administrator-CKA.html#k8s%E7%BB%83%E4%B9%A0%E7%8E%AF%E5%A2%83)(同CKA)

### CKS练习题

有几个练习库，建议将每个题目都自己亲自操作一遍，一定要操作。

- CKS在线练习环境：https://killercoda.com/killer-shell-cks
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
