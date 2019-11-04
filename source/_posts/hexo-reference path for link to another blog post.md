---
title: "hexo-reference path for link to another blog post"
catalog: true
date: 2019-07-10 16:55:24
subtitle: "reference path for markdown"
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/hexotheme/header-hexo-themes.png"
tags:
- Hexo
- Blog
categories:
- TECH
- Hexo
---

## 需求

Hexo blog里面，需要一篇文章里link到另一篇文章。最好是相对路径，绝对路径容易出错，而且不灵活，一换域名所有的link都不能用了。

## Hexo的路径生成
我们可以看到Hexo的路径生成：

例子1：
http://localhost:4000/2019/06/11/BlogName1/

例子2：
http://liyuankun.top/2019/06/11/Changing-SSL-port-from-8443-to-443/

> 域名：端口/YYYY/MM/DD/BlogName

> 域名/YYYY/MM/DD/BlogName

YYYY/MM/DD 是BlogName的创建时间，date: 2019-06-11 16:55:24

## 解决方法

例子1：

在BlogName1里面link到BlogName2 的链接就为：
```markdown
当_config.yml  permalink: :year/:month/:day/:title/
[BlogName2](../../../../2019/06/11/BlogName2)
或
当_config.yml permalink: :title.html
[BlogName2](../BlogName2.html)
```
2019/06/11 必须是BlogName2的date


例子2：

本篇文章link到文章“Changing SSL port from 8443 to 443”

markdown写为：
```markdown
当_config.yml  permalink: :year/:month/:day/:title/

[Changing-SSL-port-from-8443-to-443](../../../../2019/06/11/Changing-SSL-port-from-8443-to-443/)
或
当_config.yml permalink: :title.html
[Changing-SSL-port-from-8443-to-443](../Changing-SSL-port-from-8443-to-443.html)
```
效果为：
当_config.yml  permalink: :year/:month/:day/:title/
[Changing-SSL-port-from-8443-to-443](../../../../2019/06/11/Changing-SSL-port-from-8443-to-443/)
或
当_config.yml permalink: :title.html
[Changing-SSL-port-from-8443-to-443](../Changing-SSL-port-from-8443-to-443.html)



## 参考
[Markdown 中文文档 内联元素](https://markdown-zh.readthedocs.io/en/latest/spanelements/)
