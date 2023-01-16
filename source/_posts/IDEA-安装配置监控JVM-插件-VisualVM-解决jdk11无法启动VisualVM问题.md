---
title: IDEA 安装配置监控JVM 插件-VisualVM-解决jdk11无法启动VisualVM问题
catalog: true
date: 2023-01-16 18:43:33
subtitle:
header-img:
tags:
- Java
- IntelliJ
categories:
- TECH
- BackEnd
- Java
- JVM
---

## IDEA 安装配置监控JVM 插件

打开Preference --> Plugins --> 搜索VisualVM  --> install --> Apply

[VisualVM IDEA 插件链接](https://plugins.jetbrains.com/plugin/7115-visualvm-launcher/)

![VisualVM-install.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Java/VisualVM/VisualVM-install.png)

## IDEA配置VisualVM

重新打开Preference --> Other Settings --> VisualVM Launcher --> VisualVM executable

Other Settings --> VisualVM Launcher 这部分设置第一步"plugins中安装VisualVM Launcher插件"之后才会显示。

### jdk 8

VisualVM executable 填 `你的jdk8路径/bin/jvisualvm.exe`, 例如`C:/Program Files/Java/jdk1.8.0_131/bin/jvisualvm.exe`

### jdk 11

发现JDK11的目录里，bin目录下并没有jvisualvm的可执行文件`jvisualvm.exe`.
原来从jdk 9开始, visualVM不再集成在Oracle JDK中, 需要单独下载安装。

- IDEA 的VisualVM executable里也有提示链接： [VisualVM executable](https://visualvm.github.io/)
- 下载地址: https://visualvm.github.io/download.html
- 与IDE集成方式： https://visualvm.github.io/idesupport.html

- Windows 下载visualvm_215.zip
  <!-- - 解压到JDK目录下，层级对应覆盖即可。bin目录下的内容copy到`你的jdk11路径/bin` (例如`C:/Program Files/Eclipse Adoptium/jdk-11.0.13.8-hotspot/bin/visualvm.exe`)下面，其他类似。 -->
  - 解压visualvm_215.zip为visualvm_215，我是放在`Z:\Program Files\visualvm_215`
  - VisualVM executable 填写`visualvm_215路径/bin/visualvm.exe`
  - `visualvm_215路径/etc/visualvm.conf` 里面配置JDK路径，例如 `visualvm_jdkhome="C:/Program Files/Eclipse Adoptium/jdk-11.0.13.8-hotspot"`
  - 如果显示检测不到本地运行Java程序, 就到刚刚`visualvm_215路径/bin/jvisualvm.exe`的文件处，右击选择`以管理员身份运行`
    - 监控的本地jdk路径（不修改也是能用，只是不能显示详细的包名和类名，只显示进程号难以区分）
- MacOS 下载VisualVM_215.dmg 安装
  - VisualVM executable 填写`/Applications/VisualVM.app/Contents/MacOS/visualvm`

![VisualVM-config-mac](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Java/VisualVM/VisualVM-config-mac.png)

![VisualVM-config-windows](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Java/VisualVM/VisualVM-config-windows.png)

Preference --> Other Settings --> VisualVM Launcher --> Custom JDK home path 默认使用project配置的JDK，如果找不到，就会使用填写的指定的jdk。



## IDEA启动VisualVM

然后重启IDEA，点击`Run`就发现多了两个选择。点击这两个选项，就可以启动VisualVM。

- `Run with VisualVM`
- `DeBug with VisualVM`

![启动VisualVM](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Java/VisualVM/VisualVM-start.png)

![VisualVM-run](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Java/VisualVM/VisualVM-run.png)

### 启动按钮diabled状态无法启动VisualVM

可以参考这篇文章：[IDEA安装了VisualVM Launcher插件无法调试使用](https://segmentfault.com/a/1190000040495117)
但是仍然没有解决我的问题，仍然是disabled状态。后来在左下方“Console” tab下看到了VisualVM一个图标，实测可用。

![“Console” tab下看到了VisualVM一个图标](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Java/VisualVM/VisualVM-IDEAstart.pic.jpg)

### 命令行启动VisualVM

1. 本地启动Java服务后，保持运行；打开终端，输入jps命令回车，查看进程ID，例如进程ID为44620；
`jps`

2. 打开终端，输入jvisualvm命令、参数和进程ID后回车，会自动打开此软件，命令如下：

`jvisualvm --openpid 44620`
之后，稍等片刻，会自动弹出Java VisualVM软件界面。

## 查看VisualVM

![VisualVM-heap](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Java/VisualVM/VisualVM-heap.png)

可以改变在VisualVM --> Tool --> Plugins --> Settings --> Edit
Java VisualVM 插件各个版本： https://visualvm.github.io/pluginscenters.html

![VisualVM-plugin.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Java/VisualVM/VisualVM-plugin.png)

## Java VisualVM软件操作

1、点击次级导航Tab中Threads项，之后点击Heap Dump按钮，会打印输出线程详细状态；

2、点击次级导航Tab中Monitor项，之后点击Heap Dump按钮，会输出内存镜像文件(.hprof文件，此文件可使用Eclipse平台的Memory Analyzer Tool，即MAT，进行详细分析)，此文件的完整路径，在界面中有显示；

[Jvisualvm简单使用教程](https://blog.csdn.net/u014427391/article/details/95347716?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-95347716-blog-124230445.pc_relevant_3mothn_strategy_recovery&spm=1001.2101.3001.4242.1&utm_relevant_index=3)

## [jdk 11使用jvisualVM visualGC](https://blog.csdn.net/muxiaoshan/article/details/124230445)


## 监控JVM

- [VisualVM远程连接配置](https://blog.csdn.net/wngpenghao/article/details/82884874)
- [环境篇：idea 安装VisualVM，Jprofiler，jclasslib](https://juejin.cn/post/6997281868362350599#heading-2)

- [idea安装Jprofiler](https://juejin.cn/post/6997281868362350599#heading-2)
- [JAVA内存分析：idea集成jprofiler查看JVM内存使用情况](https://blog.csdn.net/liaoyue11/article/details/110853303?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-110853303-blog-123939267.pc_relevant_recovery_v2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-110853303-blog-123939267.pc_relevant_recovery_v2&utm_relevant_index=5)
- [JVM系列（二十）JVM监控及诊断工具-命令行篇](https://juejin.cn/post/7081830261846982693)
