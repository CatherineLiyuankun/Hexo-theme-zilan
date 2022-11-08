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

上一篇：[CKA考试真题](./Kubernates-Certified-Kubernetes-Administrator-CKA.html)

## 考试内容

- 考试包括 15-20 项performance-based tasks。
  - 实测是19道题
- 考生有 2 小时的时间完成 CKA 和 CKAD 考试。
  - 因为从06/2022开始环境升级（贬义），考试环境更难用了，变的很卡，所以时间变得比较紧张。容易做不完题，建议先把有把握的，花费时间不多的题先做掉
    - [CKS CKA CKAD changed Terminal to Remote Desktop ](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e)
- CKAD考试66分以上即可通过，考试不通过有一次补考机会。

![CKA](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKA/CKA_exam_syllabus.png)
![CKAD](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/CKA/CKAD_exam_syllabus.png)

### More items for CKAD than CKA

- Define, build and modify container images, `Dockerfile`
- Understand multi-container Pod design patterns (init containers)
- Understand `Jobs` and `CronJobs`
- Implement `probes` and health checks
- Understand `SecurityContexts`

## 如何备考

可以本地安装`Minikube`练习， 参考另一篇博客[Minikube安装-MacOS M1](./Minikube%E5%AE%89%E8%A3%85-MacOS-M1.html)。有几个练习库，建议将每个题目都自己亲自操作一遍，一定要操作。

- https://github.com/StenlyTU/K8s-training-official
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
  - k8s中创建sa时会默认创建对应的secret，secret中存有token信息，查看yaml文件和使用describe命令得到的token信息不一致，因为yaml中的token是使用base64加密后的，可使用`echo yaml token | base64 -d`解密，对比可以发现两者一致。


## Pre Setup

Once you've gained access to your terminal it might be wise to spend ~1 minute to setup your environment. You could set these:

```bash
alias k=kubectl                         # will already be pre-configured

export do="--dry-run=client -o yaml"    # k create deploy nginx --image=nginx $do

export now="--force --grace-period 0"   # k delete pod x $now 复制粘贴 format

# 使用例子
k run pod1 --image=httpd:2.4.41-alpine $do > 2.yaml
```

### [Vim 设置](https://www.ruanyifeng.com/blog/2018/09/vimrc.html)

1. `:set nopaste` Turning off auto indent when pasting text into vim
   `:set paste` Turning on auto indent when pasting text into vim
   [Paste toggle](https://vim.fandom.com/wiki/Toggle_auto-indenting_for_code_paste)
  
2. 开启TAB补全 (2022最新考试环境已开启，不用再配置了)
   - `kubectl --help | grep bash`,此步是为了找关键词completion
   - `sudo vim /etc/profile`
   - 添加`source <(kubectl completion bash)`
   - 保存退出，`source /etc/profile`

3. toggle vim line numbers

When in `vim` you can press <kbd>Esc</kbd> and type `:set number` (turn on number) or `:set nonumber` (turn off number) followed by Enter to toggle line numbers. This can be useful when finding syntax errors based on line - but can be bad when wanting to mark&copy by mouse. You can also just jump to a line number with <kbd>Esc</kbd> `:22` + Enter.

4. copy & paste

复制粘贴 - 从网页上copy yaml内容，使用vim 来粘贴时，yaml内容格式会乱。现在已经被修复，环境里面默认加了一些vim粘贴的设置。
Make sure to set these in your `.vimrc` or otherwise indents will be very messy during pasting (the exams have these config settings now also by default, but can’t hurt to be able to type them down):

下面代码中，双引号开始的行表示注释。

```vim
”由于 Tab 键在不同的编辑器缩进不一致，该设置自动将 Tab 转为空格。
:set expandtab

”按下 Tab 键时，Vim 显示的空格数。
:set tabstop=2

”在文本上按下>>（增加一级缩进）、<<（取消一级缩进）或者==（取消全部缩进）时，每一级的字符数。
:set shiftwidth=2
```

Get used to copy/paste/cut with vim:

```md
Mark lines: Esc+v (then arrow keys)
Copy marked lines: y
Cut marked lines: d
Past lines: p or P
```

5. Indent multiple lines

To indent multiple lines press <kbd>Esc</kbd> and type `:set shiftwidth=2`. First mark multiple lines using <kbd>Ctrl</kbd> <kbd>v</kbd>  and the up/down keys. Then to indent the marked lines press <kbd>></kbd> or <kbd><</kbd>. You can then press <kbd>.</kbd> to repeat the action.


### [使用nano编辑器](./Kubernates-Certified-Kubernetes-Administrator-CKA.html#%E4%BD%BF%E7%94%A8nano%E7%BC%96%E8%BE%91%E5%99%A8)

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
  - [Kubernetes CKAD 1.20 - 真题 3道题](https://blog.csdn.net/itsaka/article/details/117590286)
    - [Kubernetes CKAD 1.20 - 真题 （第4题）](https://www.cxymm.net/article/itsaka/117590558)
  - [2022 K8S CKAD 1.23 考试 实验 模拟环境（一键导入）](https://blog.csdn.net/vic_qxz/article/details/123361130?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166039499316782248581366%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166039499316782248581366&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~pc_rank_34-16-123361130-null-null.142^v40^pc_search_integral,185^v2^control&utm_term=CKAD%E8%80%83%E8%AF%95%E9%A2%98&spm=1018.2226.3001.4187)


- CKAD 练习题
  - [CKAD考试真题-练习题150道](https://www.cnblogs.com/peteremperor/p/12785335.html)
  - [2020 CKAD 考试习题练习104道](https://blog.csdn.net/tanjunchen/article/details/104865939?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166039499316782248541148%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166039499316782248541148&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-104865939-null-null.142^v40^pc_search_integral,185^v2^control&utm_term=CKAD%E8%80%83%E8%AF%95%E9%A2%98&spm=1018.2226.3001.4187)
  - [2019 Practice Enough With These 150 Questions for the CKAD Exam](https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552)