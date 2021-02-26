---
title: 快速解决windows下 cd 无法切换盘符目录
catalog: true
date: 2018-02-26 16:45:01
subtitle:
header-img:
tags:
- Command line
categories:
- TECH
- Tools
---

在windows系统， 打开cmd.exe 或者 Command prompt。
默认进入到当前用户主目录下， 发现除了C:\， 可以通过cd .. , cd , dir 去到C:\下的各个目录， 可以在c盘下的各个目录自由切换。
但是不能通过 `cd e:\` 进入到e盘，仍停留在原来C:\盘的位置。

## 解决方法1

在 cd 和盘符之间加上 /e

```shell
cd /e e:
```

## 解决方法2

不用cd指令,直接用e盘符

```shell
e: 
```

![https://github.com/CatherineLiyuankun/PictureBed/blob/master/blog/post/%E5%BF%AB%E9%80%9F%E8%A7%A3%E5%86%B3windows%E4%B8%8B-cd-%E6%97%A0%E6%B3%95%E5%88%87%E6%8D%A2%E7%9B%98%E7%AC%A6%E7%9B%AE%E5%BD%95/command.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E5%BF%AB%E9%80%9F%E8%A7%A3%E5%86%B3windows%E4%B8%8B-cd-%E6%97%A0%E6%B3%95%E5%88%87%E6%8D%A2%E7%9B%98%E7%AC%A6%E7%9B%AE%E5%BD%95/command.png)

我使用方法1，不管用，方法2成功。
