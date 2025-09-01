---
title: Python安装+python2和python3的版本切换设置
catalog: true
date: 2020-06-10 20:50:27
subtitle: MacOS Python 集合
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

[廖雪峰安装Python](https://liaoxuefeng.com/books/python/install/)

如果你正在使用Mac，系统是OS X>=10.9，那么系统自带的Python版本是2.7。要安装最新的Python，有两个方法：

## 方法一：从Python官网下载安装程序

[从Python官网下载Python 最新的安装程序](https://www.python.org/downloads/)
[从Python官网下载Python 3.11.9 安装程序](https://www.python.org/downloads/release/python-3119/)
[从Python官网下载Python 2.7.18 (python2最后一个版本)](https://www.python.org/downloads/release/python-2718/)

下载后双击运行并安装:

安装目录：

```bash
which python3
/Library/Frameworks/Python.framework/Versions/3.11/bin/python3
# python2
which python
/Library/Frameworks/Python.framework/Versions/2.7/bin/python
```

## 方法二：[Homebrew and Python](https://docs.brew.sh/Homebrew-and-Python)

如果安装了Homebrew，直接通过命令`brew install python3`安装即可。
MAC Monterey 系统上新版本Homebrew， 例如 3.3.12，默认路径变为`/opt/homebrew/Cellar/python@3.10`, 下面的子目录就是用brew安装的其他包。

安装目录：`/usr/local/Cellar/python@3.11`
可执行文件目录：`/usr/local/bin/python3.11`

### `/usr/local/bin`和`/opt/homebrew/bin`都是用于存放可执行文件的目录。它们的区别在于

- `/usr/local/bin`：这是Mac OS系统中的一个标准目录，用于存放用户自己安装的软件或第三方软件的可执行文件。当你使用Homebrew或其他包管理器安装软件时，它们通常会将可执行文件安装到`/usr/local/bin`目录下。这样做的好处是，你可以通过在终端中直接输入命令来运行这些软件。

- `/opt/homebrew/bin`：这是Homebrew软件包管理器的默认安装目录。当你使用Homebrew安装软件时，它会将软件的可执行文件安装到/opt/homebrew/bin目录下。这样做的好处是，Homebrew可以管理软件的版本和依赖关系，并确保这些软件在系统中正确地运行。

总的来说，`/usr/local/bin`是一个通用的可执行文件目录，而`/opt/homebrew/bin`是Homebrew软件包管理器的特定安装目录。

## 查找Python路径

根据你实际的python安装路径，进行下一步的Environment path的设置。

### Mac 自带python 路径

```bash
which python
/usr/bin/python
```

### 从Python官网下载Python 的安装程序安装路径

```bash
which python3
/Library/Frameworks/Python.framework/Versions/3.11/bin/python3
which python
/Library/Frameworks/Python.framework/Versions/2.7/bin/python
```

### Homebrew python 路径

```bash
which python3
/opt/homebrew/bin/python3

where python
/usr/local/bin/python
```

## 查看python版本

```bash
python -V

python --version
Python 2.7.18

python3 --version
Python 3.12.5
```

# python2和python3的版本切换设置

按这篇[Python笔记：Mac上python2和python3的版本切换的简单处理方式](https://blog.csdn.net/Tyro_java/article/details/78510301)的方法设置：

## 修改bash_profile

```bash
# 我的.bash_profile没有python配置，都配在了~/.zprofile
vi ~/.bash_profile
```

如果使用zsh则相应修改`~/.zprofile`

```bash
vi ~/.zprofile
```

```vim
# -------------------- Python --------------------
# Setting PATH for Python 2.7 MAC Default
# The original version is saved in .bash_profile.pysave
# export PATH="/usr/bin:${PATH}"

# Setting PATH for Python 2.7
# The original version is saved in .zprofile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/2.7/bin:${PATH}"
export PATH

# Setting PATH for Python 3.11
# The original version is saved in .zprofile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.11/bin:${PATH}"
export PATH

# Setting PATH for Python 3.12 Homebrew
# The original version is saved in .bash_profile.pysave
# export PATH="/opt/homebrew/bin:${PATH}"
# If you using Homebrew to install Python 3
# export PATH="/usr/local/bin:${PATH}"
```

## 修改bashrc

```bash
vi ~/.bashrc
```

如果使用zsh则相应修改`~/.zshrc`

```bash
# 我的~/.zshrc没有python配置，都配在了 ~/.bashrc
vi ~/.zshrc
```

```vim
# python
alias python2='/usr/bin/python2.7'
# alias python2='/Library/Frameworks/Python.framework/Versions/2.7/bin/python2' # 2.7.18  in work machine
alias python3='/Library/Frameworks/Python.framework/Versions/3.11/bin/python3.11' # 3.11 in work machine

# If you using Homebrew to install Python 3
# alias python3='/usr/local/bin/python3.9'

alias python=python3
```

使设置生效：

```bash
source ~/.bashrc
```

设置完后：

```shell
$ python -V
Python 3.8.0
$ which python2
python2: aliased to /usr/bin/python2.7
$ which python3
python3: aliased to /Library/Frameworks/Python.framework/Versions/3.11/bin/python3.9
$ which python
python: aliased to python3
```

### 切换Python版本

修改.bashrc文件中的刚添加的最后一行
修改 `alias python=python3` 或者改为`alias python=python2`

使设置生效：

```bash
source ~/.bashrc
```

# python包管理工具

## pip

`pip` 是 Python 的官方包管理工具，用于安装和管理 Python 包。它允许用户从 `Python Package Index (PyPI)` 上安装第三方库，并可以通过简单的命令来更新和卸载已安装的包。

## pipenv

`pipenv` 是一个基于 `pip` 的虚拟环境管理工具，它可以帮助开发者更方便地管理项目的依赖关系。`pipenv` 可以自动为每个项目创建一个独立的虚拟环境，并且可以自动跟踪项目所需的包及其版本。它还提供了一些方便的命令，如安装、卸载、更新依赖等。
因此，`pipenv` 可以看作是 `pip` 的一个扩展，它在 `pip` 的基础上提供了更强大的功能和更方便的使用方式，用于更好地管理 Python 项目的依赖关系。

- [Pipenv Crash Course - Youtube](https://www.youtube.com/watch?v=6Qmnh5C4Pmo&t=1s)
  - [Pipenv官方文档](https://pipenv.pypa.io/en/latest/)
  - [Python—pipenv精心整理教程](https://juejin.cn/post/6844904202737713160)
    - 安装pipenv `pip install pipenv`注：无法用pip管理的包，pipenv同样无法使用。pipenv依赖：psutil, virtualenv-clone, pew, certifi, urllib3, chardet, requests, mccabe, pyflakes, pycodestyle, flake8等第三方模块。
    - `pipenv shell`  生成`Pipfile`文件
    - `pipenv install langchain` 即可生成`Pipfile.lock`文件

# 报错解决

## pip not found 和 Pychram配置

```bash
where python3
python3: aliased to /opt/homebrew/Cellar/python@3.13/3.13.5/bin/python3.13 /opt/homebrew/bin/python3 /usr/bin/python3

pip install --user pipenv 
zsh: command not found: pip

# 1. Check which Python you’re actually using
which python3
python3: aliased to /opt/homebrew/Cellar/python@3.13/3.13.5/bin/python3.13 

python3 --version
Python 3.13.5 

# 2. Check if pip is installed for that Python
python3 -m pip --version
pip 25.1.1 from /opt/homebrew/lib/python3.13/site-packages/pip (python 3.13)


python3 -m pip install --user pipenv
error: externally-managed-environment × This environment is externally managed ╰─> To install Python packages system-wide, try brew install xyz, where xyz is the package you are trying to install. If you wish to install a Python library that isn't in Homebrew, use a virtual environment: python3 -m venv path/to/venv source path/to/venv/bin/activate python3 -m pip install xyz If you wish to install a Python application that isn't in Homebrew, it may be easiest to use 'pipx install xyz', which will manage a virtual environment for you. You can install pipx with brew install pipx You may restore the old behavior of pip by passing the '--break-system-packages' flag to pip, or by adding 'break-system-packages = true' to your pip.conf file. The latter will permanently disable this error. If you disable this error, we STRONGLY recommend that you additionally pass the '--user' flag to pip, or set 'user = true' in your pip.conf file. Failure to do this can result in a broken Homebrew installation. Read more about this behavior here: <https://peps.python.org/pep-0668/> note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages. hint: See PEP 668 for the detailed specification.
```

that error comes from PEP 668. Homebrew marks its Python as an "externally managed environment", so pip install --user pipenv is blocked to prevent breaking your system Python. (Recommended): Use pipx

do it step by step with pipx so you’ll end up with a clean, working pipenv command.

   
```bash
# 1. Install pipx via Homebrew
brew install pipx

# 2. Make sure pipx’s path is added
pipx ensurepath

#This may tell you to add something like this to your ~/.zshrc:
# export PATH="$HOME/.local/bin:$PATH"
# Then reload your shell:
source ~/.zshrc

# 3. Install pipenv with pipx
pipx install pipenv

# 4. Verify it’s working
which pipenv
/Users/yuanli/.local/bin/pipenv

pipenv --version
pipenv, version 2025.0.4
# After this, pipenv will always be available globally, isolated from Homebrew’s Python environment, 
# and you won’t run into the PEP 668 restrictions anymore. 
```

Once pipenv is installed with pipx, you can hook it into PyCharm so your projects automatically use the right environment. Here’s how:

🔹 Step 1: Make sure pipenv is in PATH

Check in your terminal:
`which pipenv`

It should point to something like:
`/Users/<you>/.local/bin/pipenv`

If PyCharm can’t find it later, you may need to add that path to PyCharm’s environment PATH (I’ll show how in Step 4).

🔹 Step 2: Open PyCharm Preferences

macOS: PyCharm > Preferences…

Windows/Linux: File > Settings…

Go to:
Project: <your project> > Python Interpreter

🔹 Step 3: Add a new interpreter from Pipenv

Click the ⚙️ gear icon > Add Interpreter.

Choose Pipenv Environment.

In the dialog:

Select Pipenv executable → click ... and point to the result of which pipenv.

Choose `Pipenv` environment:

Existing environment → if you already ran pipenv install in your project.

New environment → PyCharm will run pipenv install for you.

PyCharm will detect the Python version from Pipenv and set up the interpreter.

Look at **Python Interpreter**

If it’s not the Pipenv venv from Step 1, click the ⚙️ → Add Interpreter → Existing environment

Navigate to:

`/Users/yuanli/.local/share/virtualenvs/python-NwH-YMu4/bin/python`

Click OK and apply.

🔹 Step 4: (If PyCharm can’t find pipenv)

If PyCharm complains it can’t find pipenv, add its location to the IDE’s PATH:

Go to PyCharm > Preferences > Tools > Terminal.

Add this to the “Shell Path” or “Environment variables” section:

`PATH=$HOME/.local/bin:$PATH`

Restart PyCharm.


🔹 Step 5: Verify

Once set, open a PyCharm terminal and run:

`pipenv --version`
`python --version`


Both should match what you expect from your Pipenv environment.

## [pip3 install 成功- import requests仍找不到module:ModuleNotFoundError](https://liyuankun.top/pip3-install-%E6%88%90%E5%8A%9F-import-requests%E4%BB%8D%E6%89%BE%E4%B8%8D%E5%88%B0module-ModuleNotFoundError.html)

## 命令行报错 command cannot found pip 2

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
