---
title: 'IntelliJ IDEA:Unregistered VCS root detected'
catalog: true
date: 2019-07-10 11:26:20
subtitle:
header-img:
tags:
- IntelliJ
categories:
- TECH
- Tools
- IDE

---

如果还没有配置git，参考[IntelliJ-IDEA-Set-git](../IntelliJ-IDEA-Set-git.html)。

在IntelliJ IDEA导入已有的git项目时，出现warning：


![warning](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/IntelliJ-IDEA-Unregistered-VCS-root-detected/1.png)

打开Preference->Version Control，看到Unregistered的project目录：
![warning](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/IntelliJ-IDEA-Unregistered-VCS-root-detected/2.png)

选中要配置的Unregistered的project，点击“+”，然后Apply，解决
![warning](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/IntelliJ-IDEA-Unregistered-VCS-root-detected/3.png)


参考链接：
[Unregistered VCS root detected ](https://intellij-support.jetbrains.com/hc/en-us/community/posts/360000013600--Unregistered-VCS-root-detected-)

