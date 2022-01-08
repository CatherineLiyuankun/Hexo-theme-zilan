---
title: Mac上python2和python3的版本切换设置
catalog: true
date: 2020-06-10 20:50:27
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

# 安装Python

如果你正在使用Mac，系统是OS X>=10.9，那么系统自带的Python版本是2.7。要安装最新的Python 3.9，有两个方法：

## 方法一：从Python官网下载安装程序

[从Python官网下载Python 3.9的安装程序](https://www.python.org/downloads/)下载后双击运行并安装:

安装目录：

```python
which python3
/Library/Frameworks/Python.framework/Versions/3.9/bin/python3
```

## 方法二：Homebrew

如果安装了Homebrew，直接通过命令`brew install python3`安装即可。

安装目录：`/usr/local/Cellar/python@3.9`
可执行文件目录：`/usr/local/bin/python3.9`

# 查找Python路径

根据你实际的python安装路径，进行下一步的Environment path的设置。
## Mac 自带python 路径

```python
which python
/usr/bin/python
```

## 从Python官网下载Python 3.9的安装程序安装路径

```python
which python3
/Library/Frameworks/Python.framework/Versions/3.8/bin/python3
```

## 查看python版本

```python
python -V
```

# 设置Python路径

按这篇[Python笔记：Mac上python2和python3的版本切换的简单处理方式](https://blog.csdn.net/Tyro_java/article/details/78510301)的方法设置：

## 修改bash_profile

```bash
vi ~/.bash_profile
```

如果使用zsh则相应修改`~/.zprofile`

```bash
vi ~/.zprofile
```

```vim
# Setting PATH for Python 2.7
# The original version is saved in .bash_profile.pysave
export PATH="/usr/bin:${PATH}"

# Setting PATH for Python 3.8
# The original version is saved in .bash_profile.pysave
export PATH="/Library/Frameworks/Python.framework/Versions/3.8/bin:${PATH}"

# If you using Homebrew to install Python 3
# export PATH="/usr/local/bin:${PATH}"
```

## 修改bashrc

```bash
vi ~/.bashrc
```

如果使用zsh则相应修改`~/.zshrc`

```bash
vi ~/.zshrc
```

```vim
# python
alias python2='/usr/bin/python2.7'
alias python3='/Library/Frameworks/Python.framework/Versions/3.8/bin/python3.8'
# If you using Homebrew to install Python 3
# alias python3='/usr/local/bin/python3.8'
alias python=python3
```

使设置生效：

```bash
source ~/.bashrc
```

# 设置完后

设置完后：

```python
$ python -V
Python 3.8.0
$ which python2
python2: aliased to /usr/bin/python2.7
$ which python3
python3: aliased to /Library/Frameworks/Python.framework/Versions/3.8/bin/python3.8
$ which python
python: aliased to python3
```

# 切换Python版本

修改.bashrc文件中的刚添加的最后一行
修改 `alias python=python3` 或者改为`alias python=python2`

使设置生效：

```bash
source ~/.bashrc
```

# 命令行报错 command cannot found pip

```bash
$ pip install wakatime
command cannot found pip
```

Maybe you have installed both python2 and python3. python3 may have been installed later.

You may try to use `pip3` instead of `pip`.

First, input the command:

`pip3 -V`
If you see the version, the pip3 can be used.

In case you do

`which pip`
and it doesn't show the path, just do

`which pip3`
This will print the path which is `/usr/local/bin/pip3`

Then do open `~/.zshrc` or `nano ~/.bash_profile`.

Make alias for pip like:

```vim
alias pip=/usr/local/bin/pip3
```

N.B: You copy that line above and paste in your `.zshrc` file.

After do `source ~/.zshrc` and close `.zshrc`