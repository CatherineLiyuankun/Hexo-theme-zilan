---
title: 2022 CKAD 考试真题整理
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

## 考试内容

- 考试包括 15-20 项performance-based tasks。
  - 实测是19道题
- 考生有 2 小时的时间完成 CKA 和 CKAD 考试。
  - 因为从06/2022开始环境升级（贬义），考试环境更难用了，变的很卡，所以时间变得比较紧张。容易做不完题，建议先把有把握的，花费时间不多的题先做掉
    - [CKS CKA CKAD changed Terminal to Remote Desktop ](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e)
- CKAD考试66分以上即可通过，考试不通过有一次补考机会。

<!-- > 本文记录的题目大概按照难易程度，先易后难。 -->
## 如何备考

可以本地安装minikube练习。有几个练习库，建议将每个题目都自己亲自操作一遍，一定要操作。

- https://www.katacoda.com/liptanbiswas/courses/ckad-practice-challenges
- https://github.com/dgkanatsios/CKAD-exercises
- https://github.com/bbachi/CKAD-Practice-Questions
- https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552

题库里面题目是更简单一些，真的考题会是这些练习题的组合，把里面的题目都能熟练操作，就差不多了。

## 经验总结

- **经验1**： Kubernates cluster upgrade 或者 etcd backup 放最后做，否则环境搞坏，其他的题不能做.
- **经验2**：  需要在ssh到新的node的时候，在新的tab做题，避免忘记exit出来。
- 考试环境点击`-`来zoom out, 这样可以显示更多内容。（尤其是使用平板电脑，屏幕太小，显示有效内容很少）。
- 复制粘贴
  - What always works: copy+paste using right mouse context menu
  - What works in Terminal: <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>c</kbd> and <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>v</kbd>
  - What works in other apps like Firefox: <kbd>Ctrl</kbd>+<kbd>c</kbd> and <kbd>Ctrl</kbd>+<kbd>v</kbd>
- 可以用<kbd>Tab</kbd>键，自动补全kubectl命令，大大提升效率，以及避免键盘输入拼写错误
- 考试时间快结束的时候，弹出对话框，问你是否结束考试，一定要点击“Continue”继续考试
  - 否则直接结束考试，会引发考试系统的bug： session未能正常close，造成一直无法出成绩。只能通过提ticket来人工解决，才能拿到成绩。
- 关于sa token
  - k8s中创建sa时会默认创建对应的secret，secret中存有token信息，查看yaml文件和使用describe命令得到的token信息不一致，因为yaml中的token是使用base64加密后的，可使用`echo yaml。token | base64 -d`解密，对比可以发现两者一致。


## Pre Setup

Once you've gained access to your terminal it might be wise to spend ~1 minute to setup your environment. You could set these:

```bash
alias k=kubectl                         # will already be pre-configured

export do="--dry-run=client -o yaml"    # k create deploy nginx --image=nginx $do

export now="--force --grace-period 0"   # k delete pod x $now 复制粘贴 format

# 使用例子
k run pod1 --image=httpd:2.4.41-alpine $do > 2.yaml
```

### vim设置

1. `:set paste`
    Turning off auto indent when pasting text into vim
2. 开启TAB补全
   - `kubectl --help | grep bash`,此步是为了找关键词completion
   - `sudo vim /etc/profile`
   - 添加`source <(kubectl completion bash)`
   - 保存退出，`source /etc/profile`

3. toggle vim line numbers

When in `vim` you can press <kbd>Esc</kbd> and type `:set number` or `:set nonumber` followed by Enter to toggle line numbers. This can be useful when finding syntax errors based on line - but can be bad when wanting to mark&copy by mouse. You can also just jump to a line number with <kbd>Esc</kbd> `:22` + Enter.

4. copy&paste

复制粘贴 - 从网页上copy yaml内容，使用vim 来粘贴时，yaml内容格式会乱。现在已经被修复，环境里面默认加了一些vim粘贴的设置。
Get used to copy/paste/cut with vim:

```md
Mark lines: Esc+v (then arrow keys)
Copy marked lines: y
Cut marked lines: d
Past lines: p or P
```

5. Indent multiple lines

To indent multiple lines press <kbd>Esc</kbd> and type `:set shiftwidth=2`. First mark multiple lines using <kbd>Ctrl</kbd> <kbd>v</kbd>  and the up/down keys. Then to indent the marked lines press <kbd>></kbd> or <kbd><</kbd>. You can then press <kbd>.</kbd> to repeat the action.


### 使用nano编辑器

```bash
# 编辑1.yaml文件，如果1.yaml文件不存在则新建
nano 1.yaml
# 粘贴+编辑

# 保存 control + o
# 退出 control + x
```

##### nano快捷键

nano中被称为“快捷方式”，例如保存，退出，对齐等。最常见的功能在屏幕底部列出，但还有许多其他功能。

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



---

## 参考文章

- [linux nano命令_Nano入门指南，Linux命令行文本编辑器](https://blog.csdn.net/cum88284/article/details/109042737)
- [CKS CKA CKAD changed Terminal to Remote Desktop since 06/2022](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e)
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
  - [Kubernetes CKAD 1.20 - 真题 3道题](https://blog.csdn.net/itsaka/article/details/117590286)
    - [Kubernetes CKAD 1.20 - 真题 （第4题）](https://www.cxymm.net/article/itsaka/117590558)
  - [2022 K8S CKAD 1.23 考试 实验 模拟环境（一键导入）](https://blog.csdn.net/vic_qxz/article/details/123361130?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166039499316782248581366%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166039499316782248581366&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~pc_rank_34-16-123361130-null-null.142^v40^pc_search_integral,185^v2^control&utm_term=CKAD%E8%80%83%E8%AF%95%E9%A2%98&spm=1018.2226.3001.4187)


- CKAD 练习题
  - [CKAD考试真题-练习题150道](https://www.cnblogs.com/peteremperor/p/12785335.html)
  - [2020 CKAD 考试习题练习104道](https://blog.csdn.net/tanjunchen/article/details/104865939?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166039499316782248541148%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166039499316782248541148&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-104865939-null-null.142^v40^pc_search_integral,185^v2^control&utm_term=CKAD%E8%80%83%E8%AF%95%E9%A2%98&spm=1018.2226.3001.4187)
  - [2019 Practice Enough With These 150 Questions for the CKAD Exam](https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552)