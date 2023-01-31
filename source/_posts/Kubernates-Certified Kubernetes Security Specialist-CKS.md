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

[kubernetes CKS 3.2 AppArmor限制容器对资源访问](https://blog.csdn.net/cloud_engineer/article/details/125659959)

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

- Api Server: `/etc/kubernetes/manifests/kube-apiserver.yaml`
- Controller Manager pod specification file `/etc/kubernetes/manifests/kube-controller-manager.yaml`
- Kubelet: `/var/lib/kubelet/config.yaml`
- etcd: `/etc/kubernetes/manifests/etcd.yaml`


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
https://kubernetes.io/zh/docs/tutorials/security/apparmor/

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
Use webhook authn/authz where possible. 注意：尽可能使用 Webhook authn/authz。

Fix all of the following violations that were found against etcd:
修复针对 etcd 发现的所有以下违规行为：
Ensure that the 4.2.1 --client-cert-auth FAIL argument is set to true

#### Solution

```bash
$ ssh root@vms65.rhce.cc

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
### 确保 4.2.2 --authorization-mode 参数不能设置为 AlwaysAllow，尽可能使用 webhook authn/authz
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
https://kubernetes.io/zh-cn/docs/tasks/access-application-cluster/list-all-running-container-images/

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

the tools are pre-installed on the cluster's worker node only;the are not

avaliable on the base system or the master node.

using the tool of you choice(including any non pre-install tool) analyse the

container's behaviour for at lest 30 seconds,using filers that detect newly

spawing and executing processes

store an incident file at /opt/2/report,containing the detected incidents one per

line in the follwing format:

   [timestamp],[uid],[processName]

use runtime detection tools to detect anomalous processes spawning and executing frequently in the sigle container belonging to Pod redis. Two tools are avaliable to use:
使用运行时检测工具来检测 Pod tomcat 单个容器中频发生成和执行的异常进程。有两种工具可供使用：
- sysdig
- falco
注：这些工具只预装在 cluster 的工作节点，不在 master 节点。 使用工具至少分析 30 秒，使用过滤器检查生成和执行的进程，将事件写到 /opt/KSR00101/incidents/summary 文件中，其中包含检测的事件，格式如下：[timestamp],[uid],[processName] 保持工具的原始时间戳格式不变。
注：确保事件文件存储在集群的工作节点上。

```bash
### 需登录到工作节点操作
ssh cka-node01

### 查看 sysdig 帮助
sysdig -h

### 查看 sysdig 支持的元数据
sysdig -l

### 查看指定容器ID
crictl ps | grep tomcat

### -M 分析容器30秒，-p 指定事件保存格式，--cri 指定容器运行时，并且保存到指定文件路径中
sysdig -M 30 -p "*%evt.time,%user.uid,%proc.name" --cri /run/containerd/containerd.sock container.id=xxxxx > /opt/KSR00101/incidents/summary
```


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
