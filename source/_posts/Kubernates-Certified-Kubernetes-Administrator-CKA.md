---
title: 2022年8月 CKA 考试真题整理
catalog: true
date: 2022-08-02 22:52:43
subtitle: Kubernates-Certified Kubernetes Administrator
header-img:
tags: 
- Cloud
- container
categories:
- TECH
- container
- Kubernetes
---

## 考试内容

- 考试包括 15-20 项performance-based tasks。
  - 实测是17道题
- 考生有 2 小时的时间完成 CKA 和 CKAD 考试。
  - 因为从[06/2022开始环境升级](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad)（贬义），考试环境更难用了，变的很卡，所以时间变得比较紧张。容易做不完题，建议先把有把握的，花费时间不多的题先做掉
    - [CKS CKA CKAD changed Terminal to Remote Desktop ](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e)
    - 2022.9更新，据说很多卡顿的bug已经修复。
- 2020年9月更新的CKA新版考试66分以上即可通过（原定72分），考试不通过有一次补考机会。

![CKA](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKA/CKA_exam_syllabus.png)

### CKA Preparation

- Read the Curriculum
https://github.com/cncf/curriculum
- Read the Handbook
https://docs.linuxfoundation.org/tc-docs/certification/If-candidate-handbook
- Read the important tips
https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad
- Read the FAQ
https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad

<!-- > 本文记录的题目大概按照难易程度，先易后难。 -->

## 如何备考

### k8s练习环境

#### 本地环境-Minikube

可以本地安装`Minikube`练习， 参考另一篇博客[Minikube安装-MacOS M1](./Minikube%E5%AE%89%E8%A3%85-MacOS-M1.html)。

#### 在线环境-killercoda

- https://killercoda.com/killer-shell-cka
- https://killercoda.com/killer-shell-ckad

### CKA课程

- CKA考试-对应官方课程[Kubernetes Fundamentals (LFS258)](https://training.linuxfoundation.org/training/kubernetes-fundamentals/)
- Oreilly视频课程: (For beginner or Advanced) [Certified Kubernetes Administrator (CKA), 2nd Ed](https://learning.oreilly.com/videos/certified-kubernetes-administrator/9780137438419/).
  - [Certified Kubernetes Administrator (CKA) Crash Course](https://learning.oreilly.com/live-events/certified-kubernetes-administrator-cka-crash-course/0636920315766/)
    - 附带练习环境Practice: [Certified Kubernetes - CKA Labs](https://learning.oreilly.com/playlists/d6e3fe86-067c-4dc7-a36d-698802d0bdee/)

## 经验总结

- **经验1**： 不要完全按照顺序做题！！！Kubernates cluster upgrade 或者 etcd backup 放最后做，否则环境搞坏，其他的题不能做. 隔过去的题可以用flag标记，省的忘记哪些还没有做。
- **经验2**：  需要在ssh到新的node的时候，在新的tab做题，避免忘记exit出来。
- 使用`kubectl explain` 来查看命令内容， 例如`kubectl explain pods.spec.tolerations --recursive`
- 使用`kubectl --help` 查看命令参数, 例如`kubectl create clusterrole --help`
- 使用`kubectl api-resources`, 查看所有资源缩写
- 考试环境点击`-`来zoom out, 这样可以显示更多内容。（尤其是使用平板电脑，屏幕太小，显示有效内容很少）。
- 善用考试记事本（exam notepad）。
- 复制粘贴
  - What always works: copy+paste using right mouse context menu
  - What works in Terminal: <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>c</kbd> and <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>v</kbd>
  - What works in other apps like Firefox: <kbd>Ctrl</kbd>+<kbd>c</kbd> and <kbd>Ctrl</kbd>+<kbd>v</kbd>
- 可以用<kbd>Tab</kbd>键，自动补全kubectl命令，大大提升效率，以及避免键盘输入拼写错误
- 考试时间快结束的时候，弹出对话框，问你是否结束考试，一定要点击"Continue"继续考试
  - 否则直接结束考试，会引发考试系统的bug： session未能正常close，造成一直无法出成绩。只能通过提ticket来人工解决，才能拿到成绩。

### 常用官方文档链接

- https://kubernetes.io/docs/reference/kubectl/cheatsheet/
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands
- https://github.com/kubernetes/kubernetes
- 考试中多使用命令式命令CLI ( imperative commands)，少使用声明式（Declarative）
  - https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands
  - https://medium.com/better-programming/kubernetes-tips-create-pods-with-imperative-commands-in-1-18-62ea6e1ceb32
  - Promote the use of generators for Job, CronJob, Network Policies etc: this link is very useful:
    - https://www.linkedin.com/pulse/kubernetes-deep-dive-part-3-generators-quick-poc-atharva-chauthaiwale/
  - Use maximum conventions and best practices to avoid unexpected pod errors:
    - https://unofficial-kubernetes.readthedocs.io/en/latest/user-guide/kubectl-conventions/

## Pre Setup

Once you've gained access to your terminal it might be wise to spend ~1 minute to setup your environment. You could set these:

### kubectl 设置

**1. 设置kubectl命令别名**

```bash
alias k=kubectl                         # will already be pre-configured 
                                        # (2022最新考试环境默认已开启，不用再配置了)
export do="--dry-run=client -o yaml"    # k create deploy nginx --image=nginx $do

export now="--force --grace-period 0"   # k delete pod x $now
                                        # Don't need to wait ~30 seconds
```

```bash
# 使用例子
k run pod1 --image=httpd:2.4.41-alpine $do > 2.yaml
```

**Alias Namespace**
In addition you could define an alias like:

```bash
alias kn='kubectl config set-context --current --namespace
```

Which allows you to define the default namespace of the current context. Then once you switch a context or namespace you can just run:

```bash
k default      # set default to default
k my-namespace # set default to my-namespace
```

But only do this if you used it before and are comfortable doing so. Else you need to specify the namespace for every call, which is also fine:

```bash
k -n my-namespace get all
k -n my-namespace get pod
...
```

**2. [开启自动补全autocomplete](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-autocomplete)**
(2022最新考试环境默认已开启，不用再配置了)

- `kubectl --help | grep bash`,此步是为了找关键词completion
- `sudo vim /etc/profile`
- 添加`source <(kubectl completion bash)`
- 保存退出，`source /etc/profile`

### [Vim 设置](https://www.ruanyifeng.com/blog/2018/09/vimrc.html)

复制粘贴 - 从网页上copy yaml内容，使用vim 来粘贴时，yaml内容格式会乱。现在考试环境已经被修复，`.vimrc` 里面默认加了一些vim粘贴的设置。
> Make sure to set these in your `.vimrc` or otherwise indents will be very messy during pasting (the exams have these config settings now also by default, but can’t hurt to be able to type them down):

下面代码中，双引号开始的行表示注释。

```vim
"1.1 由于 Tab 键在不同的编辑器缩进不一致，该设置自动将 Tab 转为空格。
:set expandtab

"1.2 按下 Tab 键时，Vim 显示的空格数。
:set tabstop=2

"1.3 在文本上按下>>（增加一级缩进）、<<（取消一级缩进）或者==（取消全部缩进）时，每一级的字符数。
:set shiftwidth=2
```

**1.3 Indent multiple lines**

To indent multiple lines press <kbd>Esc</kbd> and type `:set shiftwidth=2`.
First mark multiple lines using <kbd>Ctrl</kbd> <kbd>v</kbd>  and the up/down keys. Then to indent the marked lines press <kbd>></kbd> or <kbd><</kbd>. You can then press <kbd>.</kbd> to repeat the action.

**1.4 Get used to copy/paste/cut with vim:**

```md
Mark lines: Esc+v (then arrow keys)
Copy marked lines: y
Cut marked lines: d
Past lines: p or P
```

**1.5 `:set paste`**

- `:set nopaste` Turning off auto indent when pasting text into vim
- `:set paste` Turning on auto indent when pasting text into vim
   [Paste toggle](https://vim.fandom.com/wiki/Toggle_auto-indenting_for_code_paste)
  
**1.6 显示行号 `:set number`**

toggle vim line numbers

When in `vim` you can press <kbd>Esc</kbd> and type `:set number` (turn on number) or `:set nonumber` (turn off number) followed by Enter to toggle line numbers. This can be useful when finding syntax errors based on line - but can be bad when wanting to mark&copy by mouse.
You can also just jump to a line number with <kbd>Esc</kbd> `:22` + Enter.

### 使用nano编辑器

```bash
# 编辑1.yaml文件，如果1.yaml文件不存在则新建
nano 1.yaml
# 粘贴+编辑

# 保存 control + o
# 退出 control + x
```

#### nano快捷键

nano中被称为"快捷方式"，例如保存，退出，对齐等。最常见的功能在屏幕底部列出，但还有许多其他功能。

<!-- 请注意，nano不使用快捷键中的<kbd>Shift</kbd>键。 所有快捷方式均使用小写字母和未修改的数字键，因此<kbd>Ctrl</kbd> + <kbd>G</kbd>不是<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>G</kbd>。 -->

- 光标控制
  - 移动光标：使用用方向键移动。
  - 选择文字：按住鼠标左键拖动
  - ^A        move to the beginning of the current line.
    ^E        move to the End of the current line.

- 复制、剪贴和粘贴
  <!-- - 复制一整行：<kbd>option</kbd> + <kbd>6</kbd> -->
  - 复制和粘贴快捷键<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>c</kbd> and <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>v</kbd>
  - 剪切一整行<kbd>control</kbd>  + <kbd>K</kbd>
  - 在当前光标处插入上次剪切的内容<kbd>control</kbd>  + <kbd>U</kbd>

- 选中：<kbd>control</kbd>  + <kbd>U</kbd>
  - 如果需要复制／剪贴多行或者一行中的一部分，先将光标移动到需要复制／剪贴的文本的开头，按<kbd>control</kbd>  + <kbd>6</kbd>（或者<kbd>option</kbd> + <kbd>A</kbd>）做标记，然后移动光标到 待复制／剪贴的文本末尾。
  - 这时选定的文本会反白，用<kbd>option</kbd> + <kbd>6</kbd>来复制，<kbd>control</kbd>  + <kbd>K</kbd> 来剪贴。若在选择文本过程中要取消，只需要再按一次<kbd>control</kbd>  + <kbd>6</kbd>。

- 保存
  - 使用<kbd>control</kbd> + <kbd>O</kbd>来保存所做的修改

- 退出
  - 按<kbd>control</kbd> + <kbd>X</kbd> 
  - 如果你修改了文件，下面会询问你是否需要保存修改。
    - 输入<kbd>Y</kbd>确认保存，输入<kbd>N</kbd>不保存，按<kbd>control</kbd>  + <kbd>U</kbd>取消返回。
    - 如果输入了<kbd>Y</kbd>，下一步会让你输入想要保存的文件名。
      - 如果不需要修改文件名直接回车就行；若想要保存成别的名字（也就是另存为）则输入新名称然后回车。这个时候也可用<kbd>control</kbd>  + <kbd>U</kbd>来取消返回。
- Undo
  - <kbd>Meta</kbd> + <kbd>u</kbd>
  - 考试环境 + MAC OS 上的<kbd>Meta</kbd>实测是<kbd>Esc</kbd>
- Redo
  - <kbd>Meta</kbd> + <kbd>e</kbd>
- 搜索
  - 按<kbd>control</kbd>  + <kbd>W</kbd>，然后输入你要搜索的关键字，回车确定。这将会定位到第一个匹配的文本，接着可以用<kbd>option</kbd> + <kbd>W</kbd>来定位到下一个匹配的文本。

- 翻页
  - <kbd>control</kbd>  + <kbd>Y</kbd>到上一页 <kbd>control</kbd>  + <kbd>V</kbd>到下一页

<!-- >       ^G (F1)   Display this help text.
        ^F        move Forward a character.
        ^B        move Backward a character.
        ^P        move to the Previous line.
        ^N        move to the Next line.
        ^A        move to the beginning of the current line.
        ^E        move to the End of the current line.
        ^V (F8)   move forward a page of text.
        ^Y (F7)   move backward a page of text.

        ^W (F6)   Search for (where is) text, neglecting case.
        ^L        Refresh the display.

        ^D        Delete the character at the cursor position.
        ^^        Mark cursor position as beginning of selected text.
                  Note: Setting mark when already set unselects text.
        ^K (F9)   Cut selected text (displayed in inverse characters).
                  Note: The selected text's boundary on the cursor side
                        ends at the left edge of the cursor.  So, with
                        selected text to the left of the cursor, the
                        character under the cursor is not selected.
        ^U (F10)  Uncut (paste) last cut text inserting it at the
                  current cursor position.
        ^I        Insert a tab at the current cursor position.

        ^J (F4)   Format (justify) the current paragraph.
                  Note: paragraphs delimited by blank lines or indentation.
        ^T (F12)  To invoke the spelling checker
        ^C (F11)  Report current cursor position

        ^R (F5)   Insert an external file at the current cursor position.
        ^O (F3)   Output the current buffer to a file, saving it.
        ^X (F2)   Exit pico, saving buffer. -->

---

## 考题1-RBAC

### RBAC题目

Task weight: 4%

Set configuration context:

```bash
[student@node-1] $ kubectl config use-context k8s
```

#### Context

You have been asked to create a new `ClusterRole` for a deployment pipeline and bind it to a specific `ServiceAccount` scoped to a specific namespace.

#### Task

Create a new `ClusterRole` named `deployment-clusterrole` which only allows to create the following resource types:

- Deployment
- StatefulSet
- DaemonSet

Create a new `ServiceAccount` named `cicd-token` in the existing namespace `app-team1`.

Bind the new ClusterRole `deployment-clusterrole` to the new ServiceAccount `cicd-token` , limited to the namespace `app-team1`.

### RBAC解答

```bash
kubectl config use-contex t k8s
$ kubectl create clusterrole deployment-clusterrole --resource=deployments,statefulsets,daemonsets --verb=create
# $ kubectl create namespace app-team1 # in the existing namespace `app-team1` 所以不需要新建namespace
$ kubectl create serviceaccount cicd-token -n app-team1
$ kubectl create rolebinding cicd-token-binding --clusterrole=deployment-clusterrole --serviceaccount=app-team1:cicd-token --namespace=app-team1
# $ kubectl -n app-team1 describe rolebindings.rbac.authorization.k8s.io cicd-token-binding
# kubectl auth can-i create deployments
```

---

## 考题2-创建 NetworkPolicy

### 题目：NetworkPolicy

Task weight: 7%

Set configuration context:

```bash
[student@node-1] $ kubectl config use-context hk85
```

#### Task

Create a new `NetworkPolicy` named `allow-port-from-namespace` that allows Pods in the existing
namespace `internal` to connect to port `5768` of other Pods in the namespace `my-app`.

Ensure that the new NetworkPolicy:

- does not allow access to Pods not listening on port 5768
- does not allow access from Pods not in namespace `my-app`

### 解答：NetworkPolicy

参考[官网network-policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

```bash
kubectl config use-context hk8s
kubectl get ns --show-labels # 得到`internal`的label，例如project=internal
# kubectl create namespace internal
kubectl label ns internal project: my-app
vim allow-port-from-namespace.yaml
# nano allow-port-from-namespace.yaml
```

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-port-from-namespace
  namespace: internal # 目的命名空间
spec:
  podSelector: {} # 加matchLabels会报错
  policyTypes:
    - Ingress
    - Egress
  ingress:
    - from:
        - namespaceSelector:
        matchLabels:
          project: internal # 命名空间label
  egress:
    - to:
        - namespaceSelector:
            matchLabels:
              project: my-app # 命名空间label
    ports:
        - protocol: TCP
        port: 5768 # 允许访问的端口
```

```bash
kubectl apply -f allow-port-from-namespace.yaml
kubectl get networkpolicies.networking.k8s.io -n internal
```

---

## 考题3-创建 svc

### 题目：创建 svc

Task weight: 7%

Set configuration context:

```bash
[student@node-1] $ kubectl config use-context k8S
```

#### Task

Reconfigure the existing deployment `front-end` and add a port specification named `http` exposing port `80/tcp` of the existing container `nginx`.

Create a new service named `front-end-svc` exposing the container port `http`.

Configure the new service to also expose the individual Pods via a `NodePort` on the nodes on which they are scheduled.

### 解答：创建 svc

search "containerPort", 参考[Connecting Applications with Services](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/)
[configure-pod-container](https://kubernetes.io/docs/tasks/configure-pod-container/_print/)

```bash
kubectl config use-context k8S

kubectl get deployment front-end # 可选
kubectl edit deployment front-end

spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - name: http # 添加port name
      containerPort: 80 # 添加containerPort
      protocol: TCP # 添加protocol
```

```bash
kubectl expose deployment front-end --name=front-end-svc --port=80 --target-port=80 --protocol=TCP --type=NodePort
```

---

## 考题4-创建 ingress 资源

### 题目：ingress

Task weight: 7%
Set configuration context:

```bash
[student@node-1] $ kubectl config use-context k85
```

#### Task

Create a new nginx Ingress resource as follows:

- Name: `pong`
- Namespace: `ing-internal`
- Exposing service `hi` on path `/hi` using service port `5678`

> The availability of service `hi` can be checked using the following command, which should return `hi`:
`[student@node-11 $ curl -kl <INTERNAL_IP>/hi`

### 解答：ingress

参考[ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)

```bash
kubectl config use-context k85
# kubectl get svc

vi pong.yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: pong
  namespace: ing-internal
  annotations:
    kubernetes.io/ingress.class: "nginx"   # 要加这句，不然kubctl get ingress 不出来address
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx-example
  rules:
  - http:
      paths:
      - path: /hi
        pathType: Prefix
        backend:
          service:
            name: hi
            port:
              number: 5678

kubectl apply -f pong.yaml

# 获取 ingress 的 IP 地址
$ kubectl get pod -n ing-internal -o wide
kubctl get ingress -n ing-internal

# 验证
$ curl -kl <INTERNAL_IP>/hi
# 返回 hi 即为成功
```

```bash
# 方法2
kubectl config use-context k85
kubectl create ingress pong -n ing-internal --rule="/hi*=hi:5678"

annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
    kubernetes.io/ingress.class: "nginx"

kubectl get ingress -n ing-internal
# kubectl get svc
curl -kl <INTERNAL_IP>/hi

```

---

## 考题5-扩展 deployment

### 题目：扩展 deployment

Task weight: 4%
难易程度： 简单
Set configuration context:

```bash
[student@node-1] $ kubectl config use-context k8s
```

#### Task

Scale the deployment `loadbalancer` to `6` pods.

### 解答：扩展 deployment

```bash
$ kubectl scale deployment loadbalancer --replicas=6
kubectl get deployment loadbalancer
kubectl get pods
```

---

## 考题6-将 pod 部署到指定 node 节点上

### 题目：将 pod 部署到指定 node 节点上

难易程度： 简单
Task weight: 4%

Set configuration context:

```bash
[student@node-1] $ kubectl config use-context k8s
```

#### Task

Schedule a pod as follows:

- Name: `nginx-kuSc00401`
- Image: `nginx`
- Node selector: `disk=spinning`

### 解答：将 pod 部署到指定 node 节点上

参考官方文档： [Assigning Pods to Nodes](https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/#create-a-pod-that-gets-scheduled-to-your-chosen-node)

```bash
kubectl config use-context k8s
kubectl run nginx-kuSc00401 --image=nginx --dry-run=client -o yaml > nginx-kusc00401.yaml
vim nginx-kusc00401.yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx-kusc00401
spec:
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
  nodeSelector: # 添加nodeSelector
    disk: spinning # 添加node label
    
kubectl apply -f nginx-kusc00401.yaml
kubectl get pod nginx-kusc00401 -o wide
```

---

## 考题7-Kubernates-upgrade

### 题目： Kubernates-upgrade

Task weight: 7%

Set configuration context:

```bash
[student@node -1] $ kubectl config use-context mk85
```

#### Task

Given an existing Kubernetes cluster running version `1.24.1`, upgrade all of the Kubernetes control plane and node components on the master node only to version `1.24.2`.

You are also expected to upgrade kubelet and kubectl on the **master** node.

> Be sure to drain the master node before upgrading it and uncordon it after the upgrade.
Do not upgrade the worker nodes, etc, the container manager, the CNI plugin, the DNS service or any other addons.

### 解答：升级master

参考官方文档： [kubernetes-upgrade kubeadm](https://kubernetes.io/zh-cn/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

```bash
$ kubectl config use-context mk8s
$ kubectl get nodes

# 腾空节点
$ kubectl drain mk8s-master-1 --ignore-daemonsets # --delete-local-data

$ ssh mk8s-master-1
$ sudo -i

# 升级kubeadm
[root@mk8s-master-1] apt-get update && apt-get install -y kubeadm=1.24.2-00
[root@mk8s-master-1] kubeadm version
[root@mk8s-master-1] kubeadm upgrade plan
# 查看etcd参数
[root@mk8s-master-1] kubeadm upgrade apply -h | grep etcd

[root@mk8s-master-1] kubeadm upgrade apply v1.22.2 --etcd-upgrade=false # 注意Do not upgrade the worker nodes, etc, the container manager, the CNI plugin, the DNS service or any other addons.

# 升级 kubelet 和 kubectl 
[root@mk8s-master-1] kubectl version
[root@mk8s-master-1] kubelet --version

[root@mk8s-master-1] apt-get update && apt-get install -y kubelet=1.24.2-00 kubectl=1.24.2-00
## 重启
[root@mk8s-master-1] sudo systemctl daemon-reload
[root@mk8s-master-1] sudo systemctl restart kubelet
[root@mk8s-master-1] kubelet --version

# 解除节点的保护
[root@mk8s-master-1] kubectl uncordon mk8s-master-1
[root@mk8s-master-1] kubectl get node # (确认只升级了 master 节点到 1.24.2 版本)

[root@mk8s-master-1] exit
```

---

## 考题8-etcd 备份还原

### 题目：etcd 备份还原

(1.20 版本需要把端口号从 2739 改成 2830)
Task weight: 7%

No configuration context change required for this item.

#### Task

First, create a snapshot of the existing `etc` instance running at `https://127.0.0.1:2379`, saving the snapshot to `/srv/data/etcd-snapshot.db`.
> Creating a snapshot of the given instance is expected to complete in seconds.
If the operation seems to hang, something's likely wrong with your command. Use <kbd>CTRL</kbd>+ <kbd>C</kbd> to cancel the operation and try again.

Next, restore an existing, previous snapshot located at
`/var/lib/backup/etcd-snapshot-previous.db`.

> The following TLS certificates/key are supplied for
connecting to the server with `etcdctl`:
>
> - CA certificate: `/opt/KUIN00601/ca.crt`
> - Client certificate: `/opt/KUIN00601/etcd-client.crt`
> - Client key: `/opt/KUIN00601/etcd-client.key`

### 解答

Search `etcd backup`, 选择 [Operating etcd clusters for Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster)

```bash
# 1.0 如果记不清参数，可查看帮助
etcdctl snapshot save --help

# 1.1 backup
ETCDCTL_API=3 etcdctl snapshot save /srv/data/etcd-snapshot.db \
--endpoints 127.0.0.1:2379 
--cacert=/opt/KUIN00601/ca.crt \
--cert=/opt/KUIN00601/etcd-client.crt \
--key=/opt/KUIN00601/etcd-client.key 

# 1.2 接着既可以检查下你备份的文件:
ETCDCTL_API=3 etcdctl --write-out=table snapshot status /data/backup/etcd- snapshot.db
#有以下输出，就没问题
+----------+----------+------------+------------+ 
| HASH | REVISION | TOTAL KEYS | TOTAL SIZE |
+----------+----------+------------+------------+ 
| fe01cf57 | 10 | 7 | 2.1 MB 
| +----------+----------+------------+------------+

# 2 restore
ETCDCTL_API=3 etcdctl snapshot restore /var/lib/backup/etcd-snapshot-previous.db \
# --data-dir /var/lib/etcd-backup \
# --endpoints 127.0.0.1:2379 
--cacert=/opt/KUIN00601/ca.crt \
--cert=/opt/KUIN00601/etcd-client.crt \
--key=/opt/KUIN00601/etcd-client.key 
```

---



## 考题9-创建多个 container 的 Pod

### 题目：创建多个 container 的 Pod

难易程度： 简单
Task weight: 4%

Set configuration context:

```bash
[student@node-1] $ kubectl config use-context k8s
```

#### Task

Create a pod named `kucc1` with a single app container for each of the following images running inside (there may be between 1 and 4 images specified): `nginx + redis + memcached + consul`.

### 解答：创建多个 container 的 Pod

```bash
kubectl config use-context k8s
vim kucc1.yaml

apiVersion: v1
kind: Pod
metadata:
  name: kucc1
spec:
  containers:
  - name: nginx
    image: nginx
  - name: redis # Add 1 
    image: redis
  - name: memcached # Add 2
    image: memcached
  - name: consul # Add 3
    image: consul

kubectl apply -f kucc1.yaml
# kubectl describe pods kucc1
```

---

## 考题10-创建 Persistent Volume

### 题目：创建 Persistent Volume

Task weight: 4%

Set configuration context:
`[student@node-1] $ kubectl config use-context hk85`

#### Task

Create a persistent volume with name `app-config`, of capacity `2Gi` and access mode `ReadWriteMany`. The type of volume is
`hostPath` and its location is `/srv/app-config`.

### 解答：创建 Persistent Volume

参考官方文档： [example of hostPath typed volume](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolume)

```bash
kubectl config use-context hk85
nano app-config.yaml

apiVersion: v1
kind: PersistentVolume
metadata:
  name: app-config # name
spec:
  capacity:
    storage: 2Gi # capacity 2Gi
  accessModes:
    - ReadWriteMany # ReadWriteMany
  hostPath: # hostPath
    path: "/srv/app-config"

kubectl apply -f app-config.yaml
kubectl get pv
```

---

## 考题11-创建 PVC

### 题目：创建 PVC

Task weight: 7%

Set configuration context:
`[student@node-1] $ kubectl config use-context ok85`

#### Task

Create a new `PersistentVolumeClaim`:

- Name: pv-volume
- Class: csi-hostpath-sc
- Capacity: 10Mi

---
Create a new Pod which mounts the `PersistentVolumeClaim` as a volume:

- Name: web-server
- Image: nginx
- Mount path: /usr/share/nginx/html

Configure the new Pod to have `ReadWriteOnce` access on the volume.

---
Finally, using `kubectl edit` or `kubectl patch` expand the `PersistentVolumeClaim` to a capacity of `70Mi` and record that change.

### 解答：创建 PVC

参考官方文档：
- 搜索 `PV pod`, 选择["Configure a Pod to Use a PersistentVolume for Storage | Kubernetes"](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolumeclaim)
  - [Create a PersistentVolumeClaim](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolumeclaim)
  - [Configure a Pod ...中文文档](https://kubernetes.io/zh-cn/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)
- 搜索 `kubectl edit pvc` [Resizing Persistent Volumes using Kubernetes](https://kubernetes.io/blog/2018/07/12/resizing-persistent-volumes-using-kubernetes/)

```bash
kubectl config use-context hk85

# 1 创建PVC
nano pv-volume.yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pv-volume # 1 name
spec:
  accessModes:
    - ReadWriteOnce # 2 ReadWriteOnce
  resources:
    requests:
      storage: 10Mi # 3
  storageClassName: csi-hostpath-sc # 4

kubectl apply -f pv-volume.yaml
kubectl get pvc

# 2 创建pod
nano web-server.yaml

apiVersion: v1
kind: Pod
metadata:
  name: web-server
spec:
  volumes:
    - name: task-pv-storage
      persistentVolumeClaim:
        claimName: pv-volume # PVC name, 要与之前一致
  containers:
    - name: nginx
      image: nginx
      ports:
        - containerPort: 80
          name: "http-server"
      volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: task-pv-storage

kubectl apply -f web-server.yaml
kubectl get pods

# 3 Edit PVC
kubectl edit pvc pv-volume --record
# 修改 storage: 10Mi 为 storage: 70Mi

```



## 考题12-设置node unavailable

### 题目：设置node unavailable

Task weight: 4%
难易程度： 简单

Set configuration context：

```bash
[student@node-1] $ kubectl config use-context ek85
```

#### Task

Set the node named `ek8s-node-1` as unavailable and reschedule all the pods running on it.

### 解答：设置node unavailable

```bash
kubectl config use-context ek85
kubectl get nodes
kubectl drain ek8s-node-1 --ignore-daemonsets --delete-emptydir-data # 不加--delete-emptydir-data会报错。可选参数：--delete-local-data --force
# kubectl uncordon ek8s-node-1 # 应该不需要这行
```

---

## 考题13-监控 pod 的日志

### 题目：监控 pod 的日志

难易程度： 简单
Task weight: 5%
Set configuration context:
`[student@node-1] $ kubectl config use-context k8s`

#### Task

Monitor the logs of pod `foobar` and:

- Extract log lines corresponding to error `unable-to-access-website`
- Write them to `/opt/KUTR00101/foobar`

### 解答：监控 pod 的日志

```bash
kubectl config use-context k8s
kubectl logs foobar | grep unable-to-access-website > /opt/KUTR00101/foobar
```

---

## 考题14-查看最高 CPU 使用率的 Pod

### 题目：查看最高 CPU 使用率的 Pod

Task weight: 5%
难易程度： 简单

Set configuration context:
`[student@node-1] $ kubectl config use-context k8s`

#### Task

From the pod label `name=cpu-user`, find pods running high CPU workloads and write the name of the pod consuming most
CPU to the file `/opt/KUTR00401/KUTR00401.txt` (which already exists).

### 解答：查看最高 CPU 使用率的 Pod

```bash
kubectl top pod -l name=cpu-user -A --sort-by=cpu

    NAMAESPACE NAME CPU MEM
    cpu-user-1 45m 6Mi
    cpu-user-2 38m 6Mi 
    cpu-user-3 35m 7Mi 
    cpu-user-4 32m 10Mi

echo 'cpu-user-1' > /opt/KUTR00401/KUTR00401.txt
```

---

## 考题15-集群故障排查

### 题目：集群故障排查

Task weight: 13%

Set configuration context:
`[student@node-1] $ kubectl config use-context wk8s`

#### Task

A Kubernetes worker node, named `wk8s-node-O` is in state `NotReady`.
Investigate why this is the case, and perform any appropriate steps to bring the node to a `Ready` state, ensuring that any
changes are made permanent.

### 解答：集群故障排查

Search `systemctl restart`, 选择[Troubleshooting kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/troubleshooting-kubeadm/)

```bash
# kubectl get nodes
# 连接worker node
ssh wk8s-node-O
# 获取sudo权限
sudo -i
# 查看服务是否正常运行
systemctl status kubelet
# 服务重启
systemctl restart kubelet
# 设置开机自动启动
systemctl enable kubelet
# 查看服务是否正常运行
systemctl status kubelet
exit
```

---

## 考题16-添加 sidecar container

### 题目：添加 sidecar container

Task weight: 7%

Set configuration context:
`[student@node-1] $ kubectl config use-context k8s`

#### Context

Without changing its existing containers, an existing Pod needs to be integrated into Kubernetes's built-in logging
architecture (e.g. kubect] logs). Adding a streaming sidecar container is a good and common way to accomplish this
requirement.

#### Task

Add a `busybox` sidecar container to the existing Pod `legacy-app`. The new sidecar container has to run the
following command:
`/bin/sh -c tail -n+l -f /var/log/legacy-app.log`

Use a volume mount named `logs` to make the file `/var/log/legacy-app.log` available to the sidecar container.

> Don't modify the existing container.
Don't modify the path of the log file, both containers
must access it at `/var/log/legacy-app.log`

### 解答：添加 sidecar container

官网Search `Logging`, 选择[Logging Architecture](https://kubernetes.io/docs/concepts/cluster-administration/logging/).

```bash
kubectl config use-context k8s

kubectl get pod legacy-app -o yaml > legacy-app2.yaml
vim legacy-app2.yaml

apiVersion: v1
kind: Pod
metadata:
  name: legacy-app
spec:
  containers:
  - name: count
    image: busybox:1.28
    args:
    - /bin/sh
    - -c
    - >
      i=0;
      while true;
      do
        echo "$i: $(date)" >> /var/log/1.log;
        echo "$(date) INFO $i" >> /var/log/2.log;
        i=$((i+1));
        sleep 1;
      done      
    volumeMounts:
    - name: logs # 3.1 修改挂载名称
      mountPath: /var/log/legacy-app.log # 3.2 修改挂载目录
  - name: busybox  # 1 添加pod及vomuleMount挂载点
    image: busybox
    args: [/bin/sh, -c, 'tail -n+1 -f /var/log/legacy-app.log']
    volumeMounts:
    - name: logs
      mountPath: /var/log/legacy-app.log
  volumes:  
  - name: logs # 2 添加volumes
    emptyDir: {}

kubectl apply -f legacy-app2.yaml
kubectl delete pod legacy-app -–force
kubectl get pods | grep legacy-app
```

---





## 考题17-检查有多少 node 节点是健康状态

### 题目：检查有多少 node 节点是健康状态

Task weight: 4%
Set configuration context:

```bash
[studentfnode-1] $ kubectl config use-context k8S
```

#### Task

Check to see how many nodes are ready (not including nodes tainted `NoSchedule` ) and write the number to `/opt/KUSC00402/kusc00402.txt`

### 解答：检查有多少 node 节点是健康状态

Search `Check to see how many nodes are ready`, 选择[Troubleshooting Clusters](https://kubernetes.io/docs/tasks/debug/debug-cluster/#listing-your-cluster)

- [Linux grep 命令](https://www.runoob.com/linux/linux-comm-grep.html)

```bash
kubectl config use-context k8s
# 1 查看STATUS是Ready的node有3个
kubectl get nodes

# 2 查看Ready的那些node是否是NoSchedule
kubectl describe nodes | grep Taint

# 或者一个一个看node是否是NoSchedule
# kubectl describe nodes k8s-master-0 | grep Taint
#     Taints: node-role.kubernetes.io/master:NoSchedule

# kubectl describe nodes k8s-node-0 | grep Taint
#     Taints: <none>

# kubectl describe nodes k8s-node-1 | grep Taint
#     Taints: <none>

# 2 或者直接查看所有nodes里面不包含noschedule 并且是ready的共有几个，就是答案
# -i 或 --ignore-case : 忽略字符大小写的差别。-v 或 --invert-match : 显示不包含匹配文本的所有行。
# kubectl describe nodes | grep -i taints | grep -v -i noschedule 

# 3 输出 = node ready 个数 - NoSchedule 个数
echo 2 > /opt/KUSC00402/kusc00402.txt
```

---

---

## 参考文章

- [linux nano命令_Nano入门指南，Linux命令行文本编辑器](https://blog.csdn.net/cum88284/article/details/109042737)
- [CKS CKA CKAD changed Terminal to Remote Desktop since 06/2022](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e)
- [2022年CKA 考试题 2022年3月1日刚过](https://blog.csdn.net/april_4/article/details/123233845)
- [2022.2 k8s-cka考试题库](https://blog.csdn.net/qq_33680297/article/details/123074501)
- [CKA 百度文库](https://wenku.baidu.com/view/1d4a8bdbcbd376eeaeaad1f34693daef5ef713f4?bfetype=new)
- [CKA Kubernauts Training Plan Mind 脑图](https://www.mindmeister.com/zh/920845833/kubernauts-training-pla)
