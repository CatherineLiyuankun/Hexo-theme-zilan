---
title: Mac上python2和python3的版本切换设置
catalog: true
date: 2020-06-10 20:50:27
subtitle:
header-img:
tags:
---

# 查找Python路径

```python
which python
/usr/bin/python
```

```python
which python3
/Library/Frameworks/Python.framework/Versions/3.8/bin/python3
```

```python
python -V
```

# 设置Python路径

按这篇[Python笔记：Mac上python2和python3的版本切换的简单处理方式](https://blog.csdn.net/Tyro_java/article/details/78510301)的方法设置：

## 修改bash_profile

```bash
vi ~/.bash_profile
```

```vim
# Setting PATH for Python 2.7
# The original version is saved in .bash_profile.pysave
export PATH="/usr/bin:${PATH}"

# Setting PATH for Python 3.6
# The original version is saved in .bash_profile.pysave
export PATH="/Library/Frameworks/Python.framework/Versions/3.8/bin:${PATH}"
```

## 修改bashrc

```bash
vi ~/.bashrc
```

```vim
# python
alias python2='/usr/bin/python2.7'
alias python3='/Library/Frameworks/Python.framework/Versions/3.8/bin/python3.8'
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
