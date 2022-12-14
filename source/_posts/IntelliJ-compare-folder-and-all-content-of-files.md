---
title: Compare folder and all content of files
catalog: true
date: 2022-12-14 20:37:40
subtitle: IntelliJ, Meld, BeyondCompare
header-img:
tags:
- IntelliJ
categories:
- TECH
- Tools
- IDE
---

## 需求

- 文件夹比较：自动递归把所有子文件夹里的文件夹和文件内容都比较
- .class 文件会自动decomple成.java文件查看和比较

## 工具

研究了下，有几个工具可以实现，不过很多都收费：

> Any tools for comparing decompiled classes to source code?
> I'd compile the .java files you have. Then decompile those .class files and the original .class files you have. A script should be able to get you this far. Then you can compare the resultant .java files with a tool like Meld, BeyondCompare or simply `diff -ur` on the command line. Running them through the same decompiler should at least give you better commonality so there's less noise in your diffs. Good luck with that though, that doesn't sound like fun any way you slice it.

### [Meld](https://meldmerge.org/)

> Meld 帮助您比较文件、目录和版本控制的项目。 它提供文件和目录的双向和三向比较，并支持许多流行的版本控制系统。
> Meld 可帮助您查看代码更改并了解补丁。 它甚至可以帮助您弄清楚在您一直避免的合并中发生了什么。

Folder comparison

- Identify and manage missing or modified files across folders
- Drill down into a file comparison for a detailed view of differences
- Ignore certain files or folders for more useful comparisons

### [Beyond Compare 4](https://www.scootersoftware.com/)

> Intelligent Comparison
> Compare files and folders using simple, powerful commands that focus on the differences you're interested in and ignore those you're not.  Merge changes, synchronize files, and generate reports.

To decompile Java class files to source code in Beyond Compare, install the Java Class to Source file format. With the file format installed, when you double click on a .class file inside a .war archive, it will display the decompiled source code in Beyond Compare's Text Compare.
Download page for file formats: http://www.scootersoftware.com/download.php?zz=kb_moreformatsv4

缺点： 免费试用30天

### `diff -ur` on the command line

功能少，查看不方便

## IntelliJ 自带 `Compare Directories`

> IntelliJ IDEA lets you compare files in two folders against their file size, content, or timestamp. 
> The differences are displayed in the [Differences Viewer for Folders](https://www.jetbrains.com/help/idea/comparing-files-and-folders.html#comparing_folders)

优点： 免费， 使用方便，功能全！！！

1. 选中要比较的两个文件夹
2. 右键 --> `Compare Directories`
3. 可以加filter，过滤，例如*.class

![Compare Directories](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/compareFolder.png)
![Compare Directories](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/compareFolder-filter.png)