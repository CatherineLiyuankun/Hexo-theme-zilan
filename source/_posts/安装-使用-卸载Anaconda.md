---
title: 安装/使用/卸载Anaconda
catalog: true
date: 2023-08-08 21:53:39
subtitle:
header-img:
tags:
- Python
- Command line
categories:
- TECH
- Language
- Python
---

## 安装Anaconda

[Anaconda官网下载](https://www.anaconda.com/download)

如果下载网速过慢，可以使用清华大学镜像：

- 下载列表：[https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)
- 使用说明：[https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)

## 卸载Anaconda

- [Anaconda官方卸载方法-英文版](https://docs.anaconda.com/free/anaconda/install/uninstall/)
- [Anaconda官方卸载方法-中文版](https://anaconda.org.cn/anaconda/install/uninstall/)

### Step1 彻底卸载Anaconda

1. 安装 Anaconda-Clean package

打开 Anaconda Prompt 或者命令行， 输入如下命令：
```conda install anaconda-clean```

如果安装失败，参考[如何完全卸载Anaconda（如何下载Anaconda-Clean package）](https://developer.aliyun.com/article/936211)

- 删除`.condarc`文件里面的内容（不是删文件）
  - [MacOS] `~/.condarc`
  - [Window]C盘下`.condarc`
- 重新`conda install anaconda-clean`

2. 输入如下命令卸载

```bash
# If you want to confirm each file and directory you are deleting
anaconda-clean

# If you don't want to be asked about each file and directory
anaconda-clean --yes
```

### Step2 简单移除Anaconda文件

#### MacOS

Open your terminal application.
Remove your entire Anaconda directory with `rm -rf`. Depending on your installation, your anaconda2 or anaconda3 directory will be in your root folder or in your opt folder.

```bash
# The following are a few examples of how you may need to delete your Anaconda folder
rm -rf anaconda3
rm -rf ~/anaconda3
rm -rf ~/opt/anaconda3
```

Close and reopen your terminal to refresh it. You should no longer see (base) in your terminal prompt.

### Step3 Removing Anaconda path from `.bash_profile`

If you use Linux or macOS, you may also wish to check your `.bash_profile` or `.zprofile` file in your home directory for a line such as:
`export PATH="/Users/yourname/anaconda3/bin:$PATH"`

## 参考文章

- [Anaconda 介绍、安装及使用保姆级教程](https://mp.weixin.qq.com/s/vIZoE4BmXYlyhfFFmlhDWg)
