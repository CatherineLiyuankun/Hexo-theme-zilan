---
title: Kubernetes CKS 知识点&练习题
catalog: true
date: 2023-02-04 18:34:49
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


## Pod Security Policies(PSP)

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

## [AppArmor](https://kubernetes.io/docs/tutorials/security/apparmor/)

[kubernetes CKS 3.2 AppArmor限制容器对资源访问](https://blog.csdn.net/cloud_engineer/article/details/125659959)

[Manage AppArmor profiles and Pods using these](https://killercoda.com/killer-shell-cks/scenario/apparmor)

![apparmor1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor1-Check%20existing%20AppArmor%20profiles.png)

![apparmor1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor2-deployment.png)

![AppArmor2-deployment2.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor2-deployment2.png)

![AppArmor2-deployment3beforeChange.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor2-deployment3beforeChange.png)

![AppArmor2-deployment4.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor2-deployment4.png)

![AppArmor2-deployment5.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor2-deployment5.png)

![AppArmor3-install profile.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKS/AppArmor3-install%20profile.png)

## Apiserver Crash

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

### Configure a wrong argument

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

### Misconfigure ETCD connection

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
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
062e4db76ac48       a31e1d84401e6       10 minutes ago      Running             kube-apiserver            0                   2641ca9ecc8ee       kube-apiserver-controlplane

crictl logs 2641ca9ecc8ee # pod ID
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

### Invalid Apiserver Manifest YAML

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

## Apiserver Misconfigured

https://killercoda.com/killer-shell-cks/scenario/apiserver-misconfigured

Make sure to have solved the previous Scenario Apiserver Crash.
The Apiserver is not coming up, the manifest is misconfigured in `3` places. Fix it.

### Issues

For your changes to apply you might have to:

move the kube-apiserver.yaml out of the manifests directory
wait for apiserver container to be gone (watch crictl ps )
move the manifest back in and wait for apiserver coming back up
Some users report that they need to restart the kubelet (service kubelet restart ) but in theory this shouldn't be necessary.

### Solution 1

The kubelet cannot even create the Pod/Container. Check the kubelet logs in syslog for issues.

```bash
cat /var/log/syslog | grep kube-apiserver
```

There is wrong YAML in the manifest at `metadata;`

```bash
vim /etc/kubernetes/manifests/kube-apiserver.yaml

apiVersion: v1
kind: Pod
metadata:  # `metadata;` 改为 "metadata:"
```

### Solution 2

After fixing the wrong YAML there still seems to be an issue with a wrong parameter.

```bash
# Check logs in `/var/log/pods`.
cd /var/log/pods
cd /kube-system_kube-apiserver-controlplane_24f6c7045a5830f4ff3dd5c63e8bd9cb/kube-apiserver/
ls
    5.log
cat 5.log
    Error: Error: unknown flag: --authorization-modus.
# The correct parameter is --authorization-mode.
vim /etc/kubernetes/manifests/kube-apiserver.yaml
    - --authorization-mode=Node,RBAC # 修改--authorization-modus
```

### Solution 3

After fixing the wrong parameter, the pod/container might be up, but gets restarted.

Check container logs or /var/log/pods, where we should find:

Error while dialing dial tcp 127.0.0.1:23000: connect:connection refused

Check the container logs: the ETCD connection seems to be wrong. Set the correct port on which ETCD is running (check the ETCD manifest)

```bash
vim /etc/kubernetes/manifests/kube-apiserver.yaml
  - --etcd-servers=https://127.0.0.1:2379 # 修改--etcd-servers=https://127.0.0.1:23000 为--etcd-servers=https://127.0.0.1:2379
```

## [Apiserver NodeRestriction](https://killercoda.com/killer-shell-cks/scenario/apiserver-node-restriction)

[admission controller - Use the NodeRestriction Admission Controller to restrict Kubelet's permissions](https://killercoda.com/killer-shell-cks/scenario/apiserver-node-restriction)

### Verify the issue

The Kubelet on `node01` shouldn't be able to set Node labels

- starting with `node-restriction.kubernetes.io/*`
- on other Nodes than itself （不能label其他node，只能label本node：`node01`）

Verify this is not restricted atm by performing the following actions as the Kubelet from node01 :

- add label `killercoda/one=123` to Node `controlplane`
- add label `node-restriction.kubernetes.io/one=123` to Node `node01`

#### Tip

We can contact the Apiserver as the Kubelet by using the Kubelet kubeconfig

```bash
export KUBECONFIG=/etc/kubernetes/kubelet.conf
k get node
```

#### Solution

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

### Enable the NodeRestriction Admission Controller

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

## [ImagePolicyWebhook](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#imagepolicywebhook)

[Complete the ImagePolicyWebhook setup](https://killercoda.com/killer-shell-cks/scenario/image-policy-webhook-setup)

### Complete the ImagePolicyWebhook setup

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
               "allowTTL": 100,  // 2.modify 50 to 100
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
  vim /etc/kubernetes/policywebhook/kubeconf
```

The `/etc/kubernetes/policywebhook/kubeconf` should contain the correct server:

```yaml
apiVersion: v1
kind: Config
# clusters refers to the remote service.
clusters:
- cluster:
    certificate-authority: /etc/kubernetes/policywebhook/external-cert.pem # CA for verifying the remote service.
    server: https://localhost:1234 # 4.external service  # URL of remote service to query. Must use 'https'.
  name: image-checker

contexts:
- context:
    cluster: image-checker
    user: api-server
  name: image-checker
current-context: image-checker
preferences: {}

# users refers to the API server's webhook configuration.
users:
- name: api-server
  user:
    client-certificate: /etc/kubernetes/policywebhook/apiserver-client-cert.pem     # cert for the webhook admission controller to use
    client-key:  /etc/kubernetes/policywebhook/apiserver-client-key.pem             # key matching the cert
...
```

5 The apiserver needs to be configured with the ImagePolicyWebhook admission plugin:

```bash
  vim /etc/kubernetes/manifests/kube-apiserver.yaml
```

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

## [kube-bench](https://github.com/aquasecurity/kube-bench)

[cis-benchmarks-kube-bench-fix-controlplane](https://killercoda.com/killer-shell-cks/scenario/cis-benchmarks-kube-bench-fix-controlplane)

- Api Server: `/etc/kubernetes/manifests/kube-apiserver.yaml`
- Controller Manager pod specification file `/etc/kubernetes/manifests/kube-controller-manager.yaml`
- Kubelet: `/var/lib/kubelet/config.yaml`
- etcd: `/etc/kubernetes/manifests/etcd.yaml`

### Apiserver should be more conform to CIS

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

### ControllerManager should be more conform to CIS

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

### PKI directory should be more conform to CIS

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

## [Trivy](https://github.com/aquasecurity/trivy)

[Image Vulnerability Scanning Trivy](https://killercoda.com/killer-shell-cks/scenario/image-vulnerability-scanning-trivy)

### Use trivy to scan images for known vulnerabilities

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

## Falco

https://killercoda.com/killer-shell-cks/scenario/falco-change-rule

### Investigate a Falco Rule

Falco has been installed on Node `controlplane` and it runs as a service.

It's configured to log to `syslog`, and this is where the verification for this scenario also looks.

Cause the rule "shell in a container" to log by:

1. creating a new Pod image `nginx:alpine`
2. `kubectl exec pod -- sh` into it
3. check the Falco logs contain a related output

#### Tip

`service falco status`

`cat /var/log/syslog | grep falco`

#### Solution

`k run pod --image=nginx:alpine`

`k exec -it pod -- sh`

`exit`

`cat /var/log/syslog | grep falco | grep shell`

### Change a Falco Rule

Change the Falco `output` of rule "Terminal shell in container" to:

- include `NEW SHELL!!!` at the very beginning
- include `user_id=%user.uid` at any position
- include `repo=%container.image.repository` at any position

Cause syslog output again by creating a shell in that Pod.
Verify the syslogs contain the new data.

##### Tip

https://falco.org/docs/rules/supported-fields

```bash
cd /etc/falco/
grep -ri "shell in"
```
#### Solution

```bash
cd /etc/falco/
cp falco_rules.yaml falco_rules.local.yaml
vim falco_rules.local.yaml
```

```yaml
- rule: Terminal shell in container
  desc: A shell was used as the entrypoint/exec point into a container with an attached terminal.
  condition: >
    spawned_process and container
    and shell_procs and proc.tty != 0
    and container_entrypoint
    and not user_expected_terminal_shell_in_container_conditions
  output: >
    NEW SHELL!!! (user_id=%user.uid repo=%container.image.repository %user.uiduser=%user.name user_loginuid=%user.loginuid %container.info
    shell=%proc.name parent=%proc.pname cmdline=%proc.cmdline terminal=%proc.tty container_id=%container.id image=%container.image.repository)
  priority: NOTICE
  tags: [container, shell, mitre_execution]
```

```bash
service falco restart
k exec -it pod -- sh
cat /var/log/syslog | grep falco | grep shell
```

## NetworkPolicy - namespace selector

There are existing Pods in Namespace `space1` and `space2` .

We need a new NetworkPolicy named `np` that restricts all Pods in Namespace `space1` to only have outgoing traffic to Pods in Namespace `space2` . Incoming traffic not affected.

We also need a new NetworkPolicy named `np` that restricts all Pods in Namespace `space2` to only have incoming traffic from Pods in Namespace `space1` . Outgoing traffic not affected.

The NetworkPolicies should still allow outgoing DNS traffic on port `53` TCP and UDP.

### Tip

For learning you can check the NetworkPolicy Editor
The namespaceSelector from NPs works with Namespace labels, so first we check existing labels for Namespaces

### Solution

```bash
# 获取 namespace的label
k get ns --show-labels
  NAME              STATUS   AGE     LABELS
  space1            Active   3m9s    kubernetes.io/metadata.name=space1
  space2            Active   3m9s    kubernetes.io/metadata.name=space2

vim 1.yaml
```

```yaml
# 1.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: np
  namespace: space1  # namespace 已经来表示应用到all Pods in Namespace `space1`
spec:
  podSelector: {} # 所有pod
  policyTypes:
  - Egress
  egress:
    - to:
      - namespaceSelector:
          matchLabels:
            kubernetes.io/metadata.name: space2  # space2的namespace
    - ports: # 注意加 - 表示或的关系
      - protocol: TCP
        port: 53
      - protocol: UDP
        port: 53
```

```yaml
# 2.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: np
  namespace: space2
spec:
  podSelector: {}
  policyTypes:
    - Ingress
  ingress:
    - from:
      - namespaceSelector:
          matchLabels:
            kubernetes.io/metadata.name: space1
    - ports:
      - protocol: TCP
        port: 53
      - protocol: UDP
        port: 53
```

```bash
k apply -f 1.yaml
k apply -f 2.yaml
```

## NetworkPolicy - Metadata Protection

https://killercoda.com/killer-shell-cks/scenario/networkpolicy-metadata-protection

Cloud providers can have Metadata Servers which expose critical information, for example GCP or AWS.

For this task we assume that there is a Metadata Server at `1.1.1.1` .

You can test connection to that IP using `nc -v 1.1.1.1 53` .

Create a NetworkPolicy named `metadata-server `In Namespace `default` which restricts all egress traffic to that IP.

The NetworkPolicy should only affect Pods with label `trust=nope` .

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: metadata-server
  namespace: default
spec:
  podSelector:
    matchLabels:
      trust: nope
  policyTypes:
    - Egress
  egress:
    - to:
      - ipBlock:
          cidr: 0.0.0.0/0  # all addresses 掩码为0，且0.0.0.0，代表所有地址
          except:
            - 1.1.1.1/32 # 
```


## RBAC - user

https://killercoda.com/killer-shell-cks/scenario/rbac-user-permissions

There is existing Namespace applications.

- User `smoke` should be allowed to `create` and `delete` Pods, Deployments and StatefulSets in Namespace `applications`.
- User `smoke` should have `view` permissions (like the permissions of the default ClusterRole named `view` ) in all Namespaces but not in `kube-system` .
- User `smoke` should be allowed to retrieve available Secret names in Namespace `applications`. Just the Secret names, no data.
- Verify everything using `kubectl auth can-i` .

### Solution

⁣1) RBAC for Namespace applications

```bash
k -n applications create role smoke --verb create,delete --resource pods,deployments,sts
k -n applications create rolebinding smoke --role smoke --user smoke
```

⁣2) view permission in all Namespaces but not kube-system

As of now it’s not possible to create deny-RBAC in K8s

So we allow for all other Namespaces

```bash
k get ns # get all namespaces
k -n applications create rolebinding smoke-view --clusterrole view --user smoke
k -n default create rolebinding smoke-view --clusterrole view --user smoke
k -n kube-node-lease create rolebinding smoke-view --clusterrole view --user smoke
k -n kube-public create rolebinding smoke-view --clusterrole view --user smoke
```

⁣3) just list Secret names, no content

This is NOT POSSIBLE using plain K8s RBAC. You might think of doing this:

```bash
# NOT POSSIBLE: assigning "list" also allows user to read secret values
k -n applications create role list-secrets --verb list --resource secrets

k -n applications create rolebinding ...
```

Having the list verb you can simply run kubectl get secrets -oyaml and see all content. Dangerous misconfiguration!

### Verify

```bash
# applications
k auth can-i create deployments --as smoke -n applications # YES
k auth can-i delete deployments --as smoke -n applications # YES
k auth can-i delete pods --as smoke -n applications # YES
k auth can-i delete sts --as smoke -n applications # YES
k auth can-i delete secrets --as smoke -n applications # NO
k auth can-i list deployments --as smoke -n applications # YES
k auth can-i list secrets --as smoke -n applications # NO
k auth can-i get secrets --as smoke -n applications # NO

# view in all namespaces but not kube-system
k auth can-i list pods --as smoke -n default # YES
k auth can-i list pods --as smoke -n applications # YES
k auth can-i list pods --as smoke -n kube-public # YES
k auth can-i list pods --as smoke -n kube-node-lease # YES
k auth can-i list pods --as smoke -n kube-system # NO
```

## RBAC - ServiceAccount

There are existing Namespaces `ns1` and `ns2`
Create ServiceAccount `pipeline` in both Namespaces.

- These SAs should be allowed to `view` almost everything in the whole cluster. You can use the default ClusterRole `view` for this
- These SAs should be allowed to `create` and `delete` `Deployments` in their Namespace.

Verify everything using `kubectl auth can-i` 

### Solution

```bash
# create Namespaces
k -n ns1 create sa pipeline
k -n ns2 create sa pipeline

# use ClusterRole view
k get clusterrole view # there is default one
k create clusterrolebinding pipeline-view --clusterrole view --serviceaccount ns1:pipeline --serviceaccount ns2:pipeline

# manage Deployments in both Namespaces
k create clusterrole -h # examples
k create clusterrole pipeline-deployment-manager --verb create,delete --resource deployments
# instead of one ClusterRole we could also create the same Role in both Namespaces

k -n ns1 create rolebinding pipeline-deployment-manager --clusterrole pipeline-deployment-manager --serviceaccount ns1:pipeline
k -n ns2 create rolebinding pipeline-deployment-manager --clusterrole pipeline-deployment-manager --serviceaccount ns2:pipeline
```



## Secret - ETCD Encryption

https://kubernetes.io/zh-cn/docs/tasks/administer-cluster/encrypt-data/
https://killercoda.com/killer-shell-cks/scenario/secret-etcd-encryption

### Enable ETCD Encryption

Create an `EncryptionConfiguration` file at `/etc/kubernetes/etcd/ec.yaml` and make ETCD use it.
- One provider should be of type `aesgcm` with password `this-is-very-sec` . All new secrets should be encrypted using this one.
- One provider should be the `identity` one to still be able to read existing unencrypted secrets.

#### Solution

Generate EncryptionConfiguration:

```bash
mkdir -p /etc/kubernetes/etcd
echo -n this-is-very-sec | base64
```

```yaml
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources:
    - secrets
    providers:
    - aesgcm:
        keys:
        - name: key1
          secret: dGhpcy1pcy12ZXJ5LXNlYw==
    - identity: {}
```

1. Add a new volume and volumeMount in `/etc/kubernetes/manifests/kube-apiserver.yaml`, so that the container can access the file.

2. Pass the new file as argument: `--encryption-provider-config=/etc/kubernetes/etcd/ec.yaml`

```yaml
spec:
  containers:
  - command:
    - kube-apiserver
...
    - --encryption-provider-config=/etc/kubernetes/etcd/ec.yaml
...
    volumeMounts:
    - mountPath: /etc/kubernetes/etcd
      name: etcd
      readOnly: true
...
  hostNetwork: true
  priorityClassName: system-cluster-critical
  volumes:
  - hostPath:
      path: /etc/kubernetes/etcd
      type: DirectoryOrCreate
    name: etcd
...
```

Wait till apiserver was restarted: `watch crictl ps`

### Encrypt existing Secrets

Encrypt all existing Secrets in Namespace `one` using the new provider
Encrypt all existing Secrets in Namespace `two` using the new provider
Encrypt all existing Secrets in Namespace `three` using the new provider

#### Tip

Recreate Secrets so they are encrypted through the new encryption settings.

#### Solution

```bash
kubectl -n one get secrets -o json | kubectl replace -f -
kubectl -n two get secrets -o json | kubectl replace -f -
kubectl -n three get secrets -o json | kubectl replace -f -
```

To check you can do for example:

```bash
ETCDCTL_API=3 etcdctl --cert /etc/kubernetes/pki/apiserver-etcd-client.crt --key /etc/kubernetes/pki/apiserver-etcd-client.key --cacert /etc/kubernetes/pki/etcd/ca.crt get /registry/secrets/one/s1
```

The output should be encrypted and prefixed with `k8s:enc:aesgcm:v1:key1`.

## Secret - Read and Decode

### Read and decode the Secrets in Namespace one

1. Get the Secrets of type Opaque that have been created in Namespace one .
2. Create a new file called /opt/ks/one and store the base64-decoded values in that file. Each value needs to be stored on a new line.

#### Solution

```bash
k get secrets -n one
NAME   TYPE     DATA   AGE
s1     Opaque   1      39s
s2     Opaque   1      39s

k get secrets s1 -n one -o yaml | grep data: -A 3
data:
  data: c2VjcmV0
kind: Secret

k get secrets s2 -n one -o yaml | grep data: -A 3
data:
  data: YWRtaW4=
kind: Secret

kubectl -n one get secret s1 -ojsonpath="{.data.data}" | base64 -d

kubectl -n one get secret s2 -ojsonpath="{.data.data}" | base64 -d

vim /opt/ks/one
```

Your file `/opt/ks/one` should look like this:

```yaml
secret
admin
```


## Privilege Escalation Containers

Set Privilege Escalation for Deployment

There is a Deployment named `logger` which constantly outputs the `NoNewPrivs` flag.

Let the Pods of that Deployment run with `Privilege Escalation` disabled.

The logs should show the field change.

### Solution

Check them logs `k logs -f deploy/logger`

Edit the Deployment and set the `allowPrivilegeEscalation` field:

`k edit deployments.apps logger`

```yaml
...
spec:
  replicas: 3
  selector:
    matchLabels:
      app: logger
  strategy: {}
  template:
    metadata:
      labels:
        app: logger
    spec:
      containers:
      - image: httpd:2.4.52-alpine
        name: httpd
        securityContext:
            allowPrivilegeEscalation: false  # 注意加在containers下面，而非spec下
...
```

## Privileged Containers

https://killercoda.com/killer-shell-cks/scenario/privileged-containers

### Create a privileged Pod

- Create a Pod named `prime` image `nginx:alpine` .
- The container should run as `privileged` .

Install iptables (`apk add iptables` ) inside the Pod.

Test the capabilities using `iptables -L` .

#### Solution

Generate Pod yaml
`k run prime --image=nginx:alpine -oyaml --dry-run=client --command -- sh -c 'sleep 1d' > pod.yaml`

Set the privileged :

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: prime
  name: prime
spec:
  containers:
  - command:
    - sh
    - -c
    - sleep 1d
    image: nginx:alpine
    name: prime
    securityContext:
      privileged: true      # Add, 注意加在containers下面，而非spec下
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```

Now exec into the Pod and run apk add iptables .

`k exec prime -- apk add iptables`

You'll see that iptables -L needs capabilities to run which it here gets through privileged.

`k exec prime -- iptables -L`

### Create a privileged StatefulSet

There is an existing StatefulSet yaml at `/application/sts.yaml` .

It should run as `privileged` but it seems like it cannot be applied.

Fix it and create the StatefulSet.

#### Solution

Edit the yaml to set privileged in the container section:

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: habanero
spec:
  selector:
    matchLabels:
      app: habanero
  serviceName: habanero
  replicas: 1
  template:
    metadata:
      labels:
        app: habanero
    spec:
      #securityContext:                   # remove
        #privileged: true                 # remove
      containers:
        - name: habanero
          image: nginx:alpine
          command:
            - sh
            - -c
            - apk add iptables && sleep 1d
          securityContext:                # add
            privileged: true              # add
```

## Container Hardening

Harden a given Docker Container
There is a Dockerfile at `/root/image/Dockerfile` .

It’s a simple container which tries to make a curl call to an imaginary api with a secret token, the call will 404 , but that's okay.

1. Use specific version `20.04` for the base image
2. Remove layer caching issues with `apt-get`
3. Remove the hardcoded secret value `2e064aad-3a90–4cde-ad86–16fad1f8943e`. The secret value should be passed into the container during runtime as env variable `TOKEN`
4. Make it impossible to `docker exec` , `podman exec` or `kubectl exec` into the container using `bash`
You can build the image using

```bash
cd /root/image
docker build .
```

### Solution

```bash
# vim /root/image/Dockerfile
FROM ubuntu
RUN apt-get update 
RUN apt-get -y install curl
ENV URL https://google.com/this-will-fail?secret-token=
CMD ["sh", "-c", "curl --head $URL=2e064aad-3a90-4cde-ad86-16fad1f8943e"]
```

```bash
# 修改为
FROM ubuntu:20.04  # 1 Specific version
RUN apt-get update && apt-get -y install curl # 2 Remove Layer Caching
ENV URL https://google.com/this-will-fail?secret-token=
RUN rm /usr/bin/bash # 4 remove bash
CMD ["sh", "-c", "curl --head $URL$TOKEN"] # 3 Secret as runtime Env variable
```

```bash
cd /root/image
docker build .
docker image ls

# 或者
podman build -t app .
podman image ls
    REPOSITORY                TAG         IMAGE ID      CREATED         SIZE
    localhost/app             latest      2bb9ee2ae5bc  57 seconds ago  132 MB

podman run -d -e TOKEN=2e064aad-3a90-4cde-ad86-16fad1f8943e app sleep 1d # run in background
podman ps | grep app
    CONTAINER ID  IMAGE                 COMMAND     CREATED        STATUS            PORTS       NAMES
    4a848daec2e2  localhost/app:latest  sleep 1d    9 seconds ago  Up 9 seconds ago              heuristic_golick

podman exec -it 4a848daec2e2 bash # fails
podman exec -it 4a848daec2e2 sh # works
```

## Container Image Footprint User

### Run the default Dockerfile

There is a given Dockerfile under /opt/ks/Dockerfile .

Using Docker:

- Build an image named `base-image` from the Dockerfile.
- Run a container named `c1` from that image.
- Check under which user the sleep process is running inside the container

#### Solution

```bash
# Build and run
cd /opt/ks/
docker build -t base-image .
docker run --name c1 -d base-image

# Show the user of processes
docker exec c1 ps
    PID   USER     TIME  COMMAND
        1 root      0:00 sleep 1d
        2 root      0:00 ps
# (to start again) Delete container
docker rm c1 --force
```

### Run container as user

Modify the Dockerfile `/opt/ks/Dockerfile` to run processes as user `appuser`
Update the image `base-image` with your change
Build a new container `c2` from that image

#### Solution

Add the USER docker command:

```bash
FROM alpine:3.12.3
RUN adduser -D -g '' appuser
USER appuser # Add this line
CMD sh -c 'sleep 1d'
```

```bash
# Build and run:
cd /opt/ks/
docker build -t base-image .
docker run --name c2 -d base-image

# Show the user of processes
docker exec c2 ps

# (to start again) Delete container
docker rm c2 --force
```

## RuntimeClass - gVisor

https://killercoda.com/killer-shell-cks/scenario/sandbox-gvisor
### Install and configure gVisor

You should install gVisor on the node `node01` and make containerd use it.
There is install script `/root/gvisor-install.sh` which should setup everything, execute it on node `node01` .

#### **Solution**

```bash
scp gvisor-install.sh node01:/root
ssh node01
    sh gvisor-install.sh
    service kubelet status
```

### Create RuntimeClass and Pod to use gVisor

Now that gVisor should be configured, create a new `RuntimeClass` for it.
Then create a new Pod named `sec` using image `nginx:1.21.5-alpine` .
Verify your setup by running `dmesg` in the Pod.

#### Tip

The handler for the gVisor RuntimeClass is `runsc`.

#### Solution

```bash
# Back to cantroplane
node01 $ exit
    logout
    Connection to node01 closed.
controlplane $ 
```

First we create the RuntimeClass

```yaml
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
  name: gvisor
handler: runsc
```

And the Pod that uses it

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sec
spec:
  runtimeClassName: gvisor
  containers:
    - image: nginx:1.21.5-alpine
      name: sec
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```

```bash
k apply -f rc.yaml
k apply -f pod.yaml
```

#### Verify

```bash
k exec sec -- dmesg | grep -i gvisor
```

## 