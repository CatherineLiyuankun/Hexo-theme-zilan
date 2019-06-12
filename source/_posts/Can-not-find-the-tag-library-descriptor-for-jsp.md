---
title: Can not find the tag library descriptor for .tld
catalog: true
date: 2019-05-14 11:28:45
subtitle: 
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Can-not-find-the-tag-library-descriptor-for-jsp/header-JSP-Tag.png"
tags:
- eclipse
categories:
- TECH
- Tools
---

# Problem
Eclipse Photon
eclipse web project一直在正常使用，不知哪天。。。突然 Promblems tab 里就冒出了好多error:
                                                                      
                                                                               
![error](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Can-not-find-the-tag-library-descriptor-for-jsp/error.png)

# Solution

基本上把[Eclipse “cannot find the tag library descriptor” for custom tags (not JSTL!)](https://stackoverflow.com/questions/1265309/eclipse-cannot-find-the-tag-library-descriptor-for-custom-tags-not-jstl?rq=1)里的方法都试了一遍，貌似都不管用。。。

最后打开project的properties：
![before](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Can-not-find-the-tag-library-descriptor-for-jsp/before.png)

修改后：
![after](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Can-not-find-the-tag-library-descriptor-for-jsp/after.png)

那些error没了，而且再改回去，貌似也没了。。。
有空再详细研究下原因。。。

# Reference Links

[Eclipse “cannot find the tag library descriptor” for custom tags (not JSTL!)](https://stackoverflow.com/questions/1265309/eclipse-cannot-find-the-tag-library-descriptor-for-custom-tags-not-jstl?rq=1)

[Can not find teh tag library descriptor for “http://java.sun.com/jsp/jstl/core”](https://stackoverflow.com/questions/13285826/can-not-find-the-tag-library-descriptor-for-http-java-sun-com-jsp-jstl-core)
