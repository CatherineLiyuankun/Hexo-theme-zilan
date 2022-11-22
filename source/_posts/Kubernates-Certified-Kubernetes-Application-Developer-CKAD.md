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

### k8s练习环境

可以本地安装`Minikube`练习， 参考另一篇博客[Minikube安装-MacOS M1](./Minikube%E5%AE%89%E8%A3%85-MacOS-M1.html)。


### CKAD练习题

有几个练习库，建议将每个题目都自己亲自操作一遍，一定要操作。

- [Git - StenlyTU - K8s Practice Training for CKA, CKAD and CKS](https://github.com/StenlyTU/K8s-training-official)
- [bbachi/CKAD-Practice-Questions](https://github.com/bbachi/CKAD-Practice-Questions)
  - 对应博客[2019.11 Practice Enough With These 150 Questions for the CKAD Exam](https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552)
    <!-- - [CKAD考试真题-练习题150道](https://www.cnblogs.com/peteremperor/p/12785335.html) 同第一个链接一样 -->
    - 同第一个链接一样，中文版 [2020 CKAD 考试习题练习104道](https://blog.csdn.net/tanjunchen/article/details/104865939?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166039499316782248541148%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166039499316782248541148&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-104865939-null-null.142^v40^pc_search_integral,185^v2^control&utm_term=CKAD%E8%80%83%E8%AF%95%E9%A2%98&spm=1018.2226.3001.4187)
- [dgkanatsios/CKAD-exercises](https://github.com/dgkanatsios/CKAD-exercises)
- Oreilly视频课程-附带练习环境（链接已失效）： https://www.katacoda.com/liptanbiswas/courses/ckad-practice-challenges


题库里面题目是更简单一些，真的考题会是这些练习题的组合，把里面的题目都能熟练操作，就差不多了。

### 课程

1. CKAD考试-对应官方课程[Kubernetes for Developers (LFD259)](https://training.linuxfoundation.org/training/kubernetes-for-developers/)
2. Oreilly视频课程-附带练习环境: (For beginner or Advanced) [Certified Kubernetes Application Developer (CKAD) Sander van Vugt](https://learning.oreilly.com/videos/certified-kubernetes-application/9780136677628/9780136677628-CKAD_00_00_00)
https://www.katacoda.com/ .

## [经验总结](http://liyuankun.top/Kubernates-Certified-Kubernetes-Administrator-CKA.html#%E7%BB%8F%E9%AA%8C%E6%80%BB%E7%BB%93)

## [Pre Setup](http://liyuankun.top/Kubernates-Certified-Kubernetes-Administrator-CKA.html#pre-setup)

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
    - [Kubernetes CKAD 1.20 - 真题 （第4题）Defining a Pod’s Readiness and Liveness Probe](https://www.cxymm.net/article/itsaka/117590558)
  - [2022 K8S CKAD 1.23 考试 实验 模拟环境（一键导入）](https://blog.csdn.net/vic_qxz/article/details/123361130?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166039499316782248581366%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166039499316782248581366&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~pc_rank_34-16-123361130-null-null.142^v40^pc_search_integral,185^v2^control&utm_term=CKAD%E8%80%83%E8%AF%95%E9%A2%98&spm=1018.2226.3001.4187)
- [Practical tips for passing CKAD certification exam](https://itnext.io/practical-tips-for-passing-ckad-exam-6cbdf2d35cb1)
