---
title: 程序员-MAC 重新装机必备2命令行+环境配置
catalog: true
date: 2021-05-31 15:25:13
subtitle:
header-img:
tags:
- MAC
categories:
- TECH
- Tools
- Environment setup
---

# Terminal 设置

- [x] [Warp](https://www.warp.dev/) [Git开源](https://github.com/warpdotdev/Warp) The terminal for the 21st century。
  - Warp解决第一个痛点，是通过减少配置、方便输入，优化输出，增加常用命令行自动提示(通过fig)，方便查看历史记录，可定义流程，等等。
  - 解决第二个痛点，则是增加协作功能。例如可以共享自己的命令行、设置项、历史记录。
  - [Warp AI](https://www.warp.dev/blog/introducing-warp-ai)： 可以直接问Warp AI怎样write script 来实现特定功能。
- [x] Terminal 用 [**iTerm2**](https://www.iterm2.com/) + [**zsh**](https://en.wikipedia.org/wiki/Z_shell) + [**oh-my-zsh**](https://github.com/robbyrussell/oh-my-zsh) 的组合，主题是 [robbyrussell](https://github.com/robbyrussell/oh-my-zsh/blob/master/themes/robbyrussell.zsh-theme).
  配置方法参考文章： [iterm2+oh-my-zsh组合你的terminal](../oh-my-zsh%E7%BB%84%E5%90%88%E4%BD%A0%E7%9A%84terminal.html).

- [x] zsh 的插件开了 git、autojump、brew、git、git-extra、git-flow、git-prompt、git-remote-branch、github、gitignore、history、history-substring-search、iterm2、node、npm、npx、nvm、tig、vscode、yarn、[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)、[命令行安装WakaTime](https://wakatime.com/terminal)
- [Mac 配置在Finder里用iTerm2打开当前目录](http://liyuankun.top/%E5%A5%A5%E5%88%A9%E7%BB%99%E4%BD%A0%E7%9A%84iTerm2-%E5%BF%AB%E9%80%9F%E7%94%A8IDE%E6%89%93%E5%BC%80%E6%96%87%E4%BB%B6.html#mac-%E9%85%8D%E7%BD%AEfinder%E5%BD%93%E5%89%8D%E7%9B%AE%E5%BD%95%E6%89%93%E5%BC%80iterm2)
  - [**Qmenu**](https://apps.apple.com/cn/app/qmenu/id1567442612?l=en&mt=12) 【免费, App strore】访达扩展，拥有QSpace【付费, App strore】的部分功能。 【推荐】现在用Qmenu，功能比OpenInTerminal 更多。
- [x] 配置[MAC终端命令行下用sublime、vscode、atom打开文件或目录](https://liyuankun.top/%E5%A5%A5%E5%88%A9%E7%BB%99%E4%BD%A0%E7%9A%84iTerm2-%E5%BF%AB%E9%80%9F%E7%94%A8IDE%E6%89%93%E5%BC%80%E6%96%87%E4%BB%B6.html#mac%E7%BB%88%E7%AB%AF%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%B8%8B%E7%94%A8sublime-vscode-atom%E6%89%93%E5%BC%80%E6%96%87%E4%BB%B6%E6%88%96%E7%9B%AE%E5%BD%95)
  - [x] open .  用finder打开当前文件
  - [x] vsc .  用vscode打开当前文件
  - [x] subl .  用Sublime打开当前文件
  - [x] atom .  用Atom打开当前文件
  - [x] command + <-  / ->     切换tab
  - [x] control + w 回退一部分命令
- [tldr](https://tldr.sh/) Simplified and community-driven `man` pages. Quick install: `npm install -g tldr`.
  - Take `git` for example, while `man` `git` outputs more than 100 lines. `> tldr git`

- [Git 多用户配置](http://liyuankun.top/Git-Push-%E9%81%BF%E5%85%8D%E9%87%8D%E5%A4%8D%E8%BE%93%E5%85%A5%E7%94%A8%E6%88%B7%E5%90%8D%E5%92%8C%E5%AF%86%E7%A0%81%E6%96%B9%E6%B3%95-%E5%A4%9A%E8%B4%A6%E6%88%B7%E9%85%8D%E7%BD%AE.html)

- [Tomcat 10.x](https://tomcat.apache.org/download-10.cgi)

# 命令行开发环境设置

## 安装Command line tools

苹果的 Command line tools 是专为开发者使用的，包括 gcc 等常用的基本工具。
推荐登陆 [<http://connect.apple.com>](http://connect.apple.com) ，然后搜索 `command line tools` 选择对应版本进行安装。
也可以通过Xcode进行安装，如果已经安装Xcode则已经包含了`command line tools`。

Mac 自带ruby，可以检查版本：

```bash
ruby -v
```

## 检查shell版本 bash or zsh or?

MAC 自带并默认使用zsh。

参考： [How to check what shell I am using in a terminal?](https://unix.stackexchange.com/questions/9501/how-to-test-what-shell-i-am-using-in-a-terminal)

### 1 常用且好记

The following works on zsh, bash, and dash, but not on csh:

```bash
$ echo $0
# or
$ echo $SHELL
```

```bash
$ echo $BASH_VERSION
# or
$ echo $ZSH_VERSION
```

### 2 作用范围广

Works in the four shells (bash, dash, zsh, csh):

```bash
ps -p $$
```

```bash
ps -p$$ -ocmd= 

# On Solaris, this may need to be
ps -p$$ -ofname=

# On macOS and on BSD should be
ps -p$$ -ocommand=
```

## 设置Zsh 作为默认shell

打开一个新的terminal来确认，设置Zsh 作为默认shell：

```bash
echo $SHELL
# 期望结果: /usr/bin/zsh or similar

# 如果shell列表中没有zsh或者你没有使用chsh权限的时候，不起作用
# 使用下面命令设置Zsh 作为默认shell
[sudo] chsh -s $(which zsh)  #或 chsh -s /bin/zsh
```

## 安装homebrew

[Homebrew 官网](https://brew.sh/)。
homebrew是Mac下目前最常用的包管理工具，相当于debain下的 apt , Red hat系列的 yum ，帮你安装、升级、移除软件工具包。
软件安装完成后homebrew有时会给出进一步设置的提示，强烈建议仔细阅读。

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 报错解决方法

[Mac 怎么安装Homebrew (2021)](https://zhuanlan.zhihu.com/p/346726110)

### 安装路径

The `/usr/local/Cellar` directory is the default location on OS X. You'll see sub-directories in there for all your installed formulae.
MAC 系统上默认路径为`/usr/local/Cellar`, 下面的子目录就是用brew安装的其他包。
homebrew默认会把可执行文件装在目录 /usr/local/bin 下面，建议修改 path 路径，让你通过 homebrew安装的工具可以覆盖掉Mac默认的（例如git, Big sur Mac自带2.30.1版本的git）。使用管理员权限修改文件/etc/paths 将 /usr/local/bin 移动到第一行。

MAC Monterey 系统上新版本Homebrew， 例如 3.3.12，默认路径变为`/opt/homebrew/Cellar`, 下面的子目录就是用brew安装的其他包。

### 通过 [homebrew](https://brew.sh/) 安装

- [x] [**autojump**](https://github.com/wting/autojump)，目录跳转。 `brew install autojump`。

<!-- - [ ] [**the\_silver\_searcher**](https://github.com/ggreer/the_silver_searcher)，文件搜索，命令行是 ag
- [ ] [**hub**](https://hub.github.com/) - git 扩展
- [ ] [**tig**](https://github.com/jonas/tig) - git 扩展
- [ ] [**bat**](https://github.com/sharkdp/bat)，带行号的 cat，可以配 `alias cat="bat"`
- [ ] [**fd**](https://github.com/sharkdp/fd)，比系统自带的 find 友好 -->

## 多个Java版本切换和安装

[Install Multiple Java Versions on Mac by Homebrew Cask](../Install-Multiple-Java-Versions-on-Mac-by-Homebrew-Cask.html)

## [Install node.js and nvm](../Install-node-js-and-nvm.html)

### Install Grunt globally

```bash
npm install -g grunt-cli
```

```bash
grunt -v
```

### Install yarn globally

```bash
npm install -g yarn
```

#### 通过 `yarn global add` 安装

- [ ] [**projj**](https://github.com/popomore/projj)，github/gitlab 项目管理
- [ ] [**serve**](https://github.com/zeit/serve)，本地静态服务器
- [ ] [**fkill**](https://github.com/sindresorhus/fkill)，比 kill 好用的进程 killer
- [ ] [**qrcode-terminal**](https://github.com/gtanner/qrcode-terminal)，二维码生成

## 安装bash-complete

bash 自动完成功能在 linux 发行版里一般都会自带，不过通过 homebrew 安装也很简单

brew install bash-completion
安装完成后需要根据提示在你的 `.profile` 文件中添加几行：

```bash
if [ -f $(brew --prefix)/etc/bash_completion ]; then
  . $(brew --prefix)/etc/bash_completion
fi
```

## Install `Maven`

### Install `Maven` - MacOS

```bash
brew install maven
```

```bash
mvn -v
Apache Maven 3.9.11 (3e54c93a704957b63ee3494413a2b544fd3d825b)
Maven home: /opt/homebrew/Cellar/maven/3.9.11/libexec
Java version: 24.0.2, vendor: Homebrew, runtime: /opt/homebrew/Cellar/openjdk/24.0.2/libexec/openjdk.jdk/Contents/Home

# vi ~/.bash_profile or
vim ~/.zshrc
```

add its bin folder to the PATH environment variable

```bash
# Maven
export M2_HOME="/opt/homebrew/Cellar/maven/3.9.11/libexec"
export PATH="${M2_HOME}/bin:${PATH}"
```

`echo $M2_HOME` 或者 `mvn --version`验证

### Install `Maven` - Windows

- Maven 3.3 要求 JDK 1.7 或以上
- Maven 3.2 要求 JDK 1.6 或以上
- Maven 3.0/3.1 要求 JDK 1.5 或以上

#### 下载 Maven 文件

- [下载 Maven](http://maven.apache.org/download.html)
- 解压 Maven 文件
  - 解压文件到你想要的位置来安装 Maven 3.2.5，你会得到 apache-maven-3.2.5 子目录。`C:\Tools\apache-maven-3.3.9`
- 设置 Maven 环境变量
  - 添加 `M2_HOME`、`MAVEN_OPTS` 环境变量。
    - 右键单击“我的电脑”，然后单击“属性” --> 单击“高级”选项卡 --> 单击“环境变量” --> 单击“新建”添加一个新变量名和值。
      - `M2_HOME= C:\Tools\apache-maven-3.3.9` 或者通过`where maven`查找已经安装的路径
      - `MAVEN_OPTS=-Xms256m -Xmx512m`
  - 编辑环境变量`path`
    - 尾部添加`%M2_HOME%\bin`
- 验证 Maven 安装
  - 现在打开控制台，执行以下命令。
  - `c:\> mvn --version`
  - 或者`echo $M2_HOME`

## Install the `Ant` build tool

### Install the `Ant` - MacOS

```bash
brew install ant
```

Add the environment variable `ANT_HOME` in your system.  
Add its bin folder to the `PATH` environment variable.

```bash
where ant
/opt/homebrew/bin/ant

# vi ~/.bash_profile or
vim ~/.zshrc
```

添加：

```bash
# ant
# BIN folder should include both ant and antRun
# If installed with brew, it should be "/usr/local/Cellar/ant@1.9/1.9.x/libexec/bin"
# export ANT_HOME=/usr/local/Cellar/1.10.10/libexec
export ANT_HOME=/opt/homebrew/Cellar/ant/1.10.15_1/libexec
export PATH=$PATH:$ANT_HOME/bin
```

`echo $ANT_HOME` 或者 `ant -version` 验证

### Install the `Ant` - Windows

- 设置 Ant 环境变量
  - 添加 `ANT_HOME`环境变量。
    - 右键单击“我的电脑”，然后单击“属性” --> 单击“高级”选项卡 --> 单击“环境变量” --> 单击“新建”添加一个新变量名和值。
      - `ANT_HOME= C:\Tools\ant` 或者通过`where ant`查找已经安装的路径
  - 编辑环境变量`path`
    - 尾部添加`%ANT_HOME%\bin`
- 验证 Maven 安装
  - 现在打开控制台，执行以下命令。
  - `c:\> ant --version`
  - 或者`echo $ANT_HOME`

## Install gradle

### 方法1：通过Homebrew安装

```bash
brew install gradle
# brew install gradle@6
brew upgrade gradle
```

### 方法2：通过SDKman安装，gradle多版本管理【推荐】

[不同版本 Gradle ，怎么和平共处](https://juejin.cn/post/6844903481942212621)

[安装SDKman](https://github.com/sdkman/sdkman-cli)

```bash
curl -s https://get.sdkman.io | bash
```

查看安装版本：

```bash
sdk version
```

安装指定版本的 Gradle

```bash
sdk install gradle 6.7
```

卸载指定版本的 Gradle

```bash
sdk uninstall gradle 6.7
```

查看当前安装的 Gradle 版本

```bash
sdk current gradle
```

查看安装的 Gradle 版本和所有版本

```bash
sdk list gradle
```

设置默认的 Gradle 版本

```bash
sdk default gradle 6.7
```

使用临时的 Gradle 版本

```bash
sdk use gradle 6.7
```

## 安装Python

### 安装Python

如果你正在使用Mac，系统是OS X>=10.9，那么系统自带的Python版本是2.7。要安装最新的Python 3.9，有两个方法：

方法一：[从Python官网下载Python 3.9的安装程序](https://www.python.org/downloads/)，下载后双击运行并安装；

安装目录：

```python
which python3
/Library/Frameworks/Python.framework/Versions/3.9/bin/python3
```

方法二：如果安装了Homebrew，直接通过命令`brew install python3`安装即可。

安装目录：`/usr/local/Cellar/python@3.9`
可执行文件目录：`/usr/local/bin/python3.9`

MAC Monterey 系统上新版本Homebrew， 例如 3.3.12，默认路径变为`/opt/homebrew/Cellar/python@3.10`, 下面的子目录就是用brew安装的其他包。

### [Mac上python2和python3的版本切换设置](../Mac上python2和python3的版本切换设置.html)

### APKTOOL

```bash
brew install apktool
```

### JADX

```bash
brew install jadx
```

<!-- ## 安装Bash

Mac 虽然默认也是使用 GNU Bash，不过使用命令 `/bin/bash --version` 可看到版本只有 3.2，该版本不支持 4.0 版本后添加的关联数组等功能，为了脚本的通用，建议升级到最新版本。

```bash
brew install bash
```

安装完要设置新安装的 bash 为默认 bash ，用超级用户编辑文件：`/etc/shells`，加入
`/usr/local/bin/bash`到第一行 -->

<!-- ## 安装coreutils

Mac底层是基于freeBSD的，所以常用工具例如 `ls` 、`grep` 也都是freeBSD版本的，为了让我们的脚本可以更容易的跨平台，我们可以安装coreutils

```bash
brew install coreutils
```

装完需要根据提示进行设置，在`.profile`文件中加入

```bash
export PATH="/usr/local/opt/coreutils/libexec/gnubin:$PATH"
export MANPATH="/usr/local/opt/coreutils/libexec/gnuman:$MANPATH"
```

让GNU的工具覆盖freeBSD的，并且使用man时显示的是GNU工具的文档。 -->

<!-- ## 安装dircolors-solarized

因为默认的 ls 配色实在很土，所以我用solarized配色方案：

mkdir ~/lib
cd ~/lib
git clone git@github.com:seebi/dircolors-solarized.git
echo 'eval `dircolors ~/lib/dircolors-solarized/dircolors.256dark`' >> ~/.profile -->

# 其他设置

## Hexo 博客

安装 Hexo（参考：[Git Pages + Jekyll/Hexo Build your own blog](../Git-Pages-Jekyll-Hexo-Build-your-own-blog.html#step1-安装-hexo)）

```bash
npm install -g hexo-cli
```

# 参考链接

- [当你拿到一台崭新的Mac电脑时，我们应该如何快速高效配置开发环境?](https://segmentfault.com/a/1190000037592655)
