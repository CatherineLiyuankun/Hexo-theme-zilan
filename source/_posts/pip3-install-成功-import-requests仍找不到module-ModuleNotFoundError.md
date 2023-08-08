---
title: 'pip3 install 成功- import requests仍找不到module:ModuleNotFoundError'
catalog: true
date: 2023-08-08 22:56:42
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

## ModuleNotFoundError 报错

```bash
# 安装requests成功 -------------
pip3 install requests
Requirement already satisfied: requests in /Users/yuanli/anaconda3/lib/python3.10/site-packages (2.28.1)
Requirement already satisfied: certifi>=2017.4.17 in /Users/yuanli/anaconda3/lib/python3.10/site-packages (from requests) (2022.12.7)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /Users/yuanli/anaconda3/lib/python3.10/site-packages (from requests) (1.26.14)
Requirement already satisfied: charset-normalizer<3,>=2 in /Users/yuanli/anaconda3/lib/python3.10/site-packages (from requests) (2.0.4)
Requirement already satisfied: idna<4,>=2.5 in /Users/yuanli/anaconda3/lib/python3.10/site-packages (from requests) (3.4)
# 安装requests成功 -------------

# 使用import requests来验证，结果报错：仍然找不到requests module
python3
Python 3.10.8 (main, Oct 13 2022, 09:48:40) [Clang 14.0.0 (clang-1400.0.29.102)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'requests
```

## 解决方法

错误消息"ModuleNotFoundError: 找不到名为 'requests' 的模块"发生的原因是Python解释器无法找到 'requests' 模块，尽管已经使用pip3进行了安装。
这个问题通常出现在系统上有多个Python安装，并且pip3安装与当前使用的Python版本不一致。

当运行Python解释器时，它显示正在使用Python 3.10.8。虽然补丁版本的差异（3.10.8与3.10）可能不是问题的原因，但是仍然值得检查pip3和python3是否引用相同的Python版本。

要解决这个问题，可以尝试以下步骤：

1. 验证与pip3关联的Python版本：`pip3 --version`
2. 检查Python路径：
运行以下命令以检查Python解释器和pip3的路径：

```bash
which python3
which pip3
```

尝试之后发现果然pip3 和 python3 对应的不是用一个python

```bash
# pip3 使用的是anaconda3里面带的pip3
/Users/yuanli/anaconda3/bin/pip3
# python3 用的是hombrew里面安装的python
python3: aliased to /opt/homebrew/Cellar/python@3.10/3.10.8/bin/python3.10
```

3. 修改`~/.bash_profile`里面python3的路径

```bash
# 根据anaconda版本可能是/anaconda 或者/anaconda2 或者/anaconda3 目录名
alias python3=/Users/yuanli/anaconda3/bin/python # yuanli修改为你的机器名
```
