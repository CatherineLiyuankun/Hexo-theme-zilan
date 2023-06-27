---
title: Git error 常见报错总结
catalog: true
date: 2022-12-07 00:30:04
subtitle:
header-img:
tags:
- git
categories:
- TECH
- Tools
---

## Error 1 Failed to connect to github.com port 443 after xxx ms: Operation timed out

- [GitHub无法访问、443 Operation timed out的解决办法](https://juejin.cn/post/6844904193170341896)
  - Solution 1：修改hosts文件，添加github.com IP
- [github push ssh方式 出现 port 443 22 的报错排查及踩坑](https://juejin.cn/post/7101271526061637668)
  - Solution 2：修改DNS

- Solution 3： 设置http和https代理 set proxy to git command by executing
  - `git config --global http.proxy http://10.xx.x.xxx:8080`
  <!-- - `git config --global http.proxy http://10.27.7.110:8080` -->
  - unset the proxy, 去除http和https代理：
    `git config --global --unset http.proxy`
    `git config --global --unset https.proxy`

## Error 2 HTTP/2 stream 1 was not closed cleanly before end of the underlying stream

是 git 默认使用的通信协议出现了问题，可以通过将默认通信协议修改为 http/1.1 来解决该问题。
`$ git config --global http.version HTTP/1.1`
`git config --global http.postBuffer 157286400`

## Error git cherry-pick xxx  fatal: bad object xxx

```bash
git checkout ABranch
# cherry-pick BBranch的一个commit
git cherry-pick 121c5f6402501dc05a9c8021ec39a52ce843d76d
fatal: bad object 121c5f6402501dc05a9c8021ec39a52ce843d76d
```

出现这个错误通常意味着你试图合并一个不存在的提交。git cherry-pick是本地特性，本地要有这个commit才可以被git cherry-pick。

- 检查提交的哈希值是否正确；
- 确保该提交存在于你的本地代码库中；
- 如果提交是在远程代码库中，请确保已将其克隆到本地并且与远程代码库保持同步；
- 如果仍然无法解决问题，可以尝试重新克隆代码库。

```bash
# 本地获取BBranch的commit
git checkout BBranch
git pull

git checkout ABranch
# cherry-pick BBranch的一个commit
git cherry-pick 121c5f6402501dc05a9c8021ec39a52ce843d76d
```
