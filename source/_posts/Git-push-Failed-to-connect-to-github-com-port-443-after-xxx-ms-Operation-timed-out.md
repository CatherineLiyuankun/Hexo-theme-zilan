---
title: >-
  Git push - Failed to connect to github.com port 443 after xxx ms: Operation
  timed out
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
  - 修改hosts文件，添加github.com IP
- [github push ssh方式 出现 port 443 22 的报错排查及踩坑](https://juejin.cn/post/7101271526061637668)
  - 修改DNS

- 去掉http和https代理：
`git config --global --unset http.proxy`
`git config --global --unset https.proxy`


## Error 2 HTTP/2 stream 1 was not closed cleanly before end of the underlying stream

是 git 默认使用的通信协议出现了问题，可以通过将默认通信协议修改为 http/1.1 来解决该问题。
`$ git config --global http.version HTTP/1.1`
`git config --global http.postBuffer 157286400`