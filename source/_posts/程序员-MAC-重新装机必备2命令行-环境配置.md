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

- [x] Terminal 用 [**iTerm2**](https://www.iterm2.com/) + [**zsh**](https://en.wikipedia.org/wiki/Z_shell) + [**oh-my-zsh**](https://github.com/robbyrussell/oh-my-zsh) 的组合，主题是 [robbyrussell](https://github.com/robbyrussell/oh-my-zsh/blob/master/themes/robbyrussell.zsh-theme). 
  配置方法参考文章： [iterm2+oh-my-zsh组合你的terminal](../oh-my-zsh%E7%BB%84%E5%90%88%E4%BD%A0%E7%9A%84terminal.html).

- [x] zsh 的插件开了 git、autojump、brew、git、git-extra、git-flow、git-prompt、git-remote-branch、github、gitignore、history、history-substring-search、iterm2、node、npm、npx、nvm、tig、vscode、yarn、[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
- [] iTerm2 里配 `Run command...` 为 `/usr/local/bin/idea --path \2 \1` ([图](https://zos.alipayobjects.com/rmsportal/RmWdxKRQUWFMoVDjerNQ.png))，这样 Command + 点击文件路径，就会在 Intellij Idea 里打开
  - [x] 安装Go2Shell，在finder可以用iTerm2打开当前目录
  - [x] 配置[MAC终端命令行下用sublime、vscode、atom打开文件或目录](https://www.cnblogs.com/hongrunhui/p/5928833.html)
    - [x] open .  用finder打开当前文件
    - [x] vsc .  用vscode打开当前文件
    - [x] subl .  用Sublime打开当前文件
    - [x] atom .  用Atom打开当前文件
    - [x] command + <-  / ->     切换tab
    - [x] control + w 回退一部分命令
- [tldr](https://tldr.sh/) Simplified and community-driven `man` pages. Quick install: `npm install -g tldr`.
  Take `git` for example, while `man` `git` outputs more than 100 lines. `> tldr git`


# 命令行开发环境设置

## 安装Command line tools

苹果的 Command line tools 是专为开发者使用的，包括 gcc 等常用的基本工具。
推荐登陆 [<http://connect.apple.com>](http://connect.apple.com) ，然后搜索 `command line tools` 选择对应版本进行安装。
也可以通过Xcode进行安装，如果已经安装Xcode则已经包含了`command line tools`。

Mac 自带ruby，可以检查版本：

```bash
ruby -v
```

## 安装homebrew

[Homebrew 官网](https://brew.sh/)。
homebrew是Mac下目前最常用的包管理工具，相当于debain下的 apt , Red hat系列的 yum ，帮你安装、升级、移除软件工具包。
软件安装完成后homebrew有时会给出进一步设置的提示，强烈建议仔细阅读。

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

报错解决方法： [Mac 怎么安装Homebrew (2021)](https://zhuanlan.zhihu.com/p/346726110)。

<!-- > homebrew默认会把可执行文件装在目录 /usr/local/bin 下面，建议修改 path 路径，让你通过 homebrew
安装的工具可以覆盖掉Mac默认的（例如git，Big sur Mac自带2.30.1版本的git）。使用管理员权限修改文件
/etc/paths 将 /usr/local/bin 移动到第一行。 -->

### 通过 [homebrew](https://brew.sh/) 安装

- [x] [**autojump**](https://github.com/wting/autojump)，目录跳转。 `brew install autojump`。

<!-- - [ ] [**the\_silver\_searcher**](https://github.com/ggreer/the_silver_searcher)，文件搜索，命令行是 ag
- [ ] [**hub**](https://hub.github.com/) - git 扩展
- [ ] [**tig**](https://github.com/jonas/tig) - git 扩展
- [ ] [**bat**](https://github.com/sharkdp/bat)，带行号的 cat，可以配 `alias cat="bat"`
- [ ] [**fd**](https://github.com/sharkdp/fd)，比系统自带的 find 友好 -->

## 多个Java版本切换和安装

[Install Multiple Java Versions on Mac by Homebrew Cask](../Install-Multiple-Java-Versions-on-Mac-by-Homebrew-Cask.html)

## Node Version Manager: nvm

```bash
brew install nvm
```

```bash
nvm
zsh: command not found: nvm
```

### 解决方法1：

There might be some problems installing nvm in new mac, caused by the shell is not bash by default, check if it is bash with command

```bash
$ echo $0
```

§ if it is not run command

```bash
$ chsh -s /bin/bash
```

And then reopen the terminal

### 解决方法2：

如果用的是`zsh`, 而不是`bash`. 将`.bashrc`中关于`nvm`的配置copy到`.zshrc`里边。
将`.bashrc`中的copy到`~.zshrc`下就可以啦。

```bash
export NVM_DIR="/usr/local/Cellar/nvm/0.38.0"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" #This loads nvm bash_completion
```

然后再

```bash
$ source ~/.zshrc
```

## 安装bash-complete

bash 自动完成功能在 linux 发行版里一般都会自带，不过通过 homebrew 安装也很简单

brew install bash-completion
安装完成后需要根据提示在你的 `.profile` 文件中添加几行：

```bash
if [ -f $(brew --prefix)/etc/bash_completion ]; then
  . $(brew --prefix)/etc/bash_completion
fi
```


## Install Node.js

1. Install Node.js

```bash
$ nvm install v10.15.0
```

2. Upgrade(https://codeforgeek.com/update-node-using-npm/)

```bash
$ sudo npm install -g n
$ npm -v
$ sudo n 10.15.0
```

## Install Maven and add its bin folder to the PATH environment variable.

```bash
brew install maven
```

```bash
mvn -v
vi ~/.bash_profile
```

```bash
# Maven
export M2_HOME="/usr/local/Cellar/maven/3.8.1/libexec"
export PATH="${M2_HOME}/bin:${PATH}"
```

## Install Grunt globally

```bash
npm install -g grunt-cli
```

## Install the Ant build tool

```bash
brew install ant
```

Add the environment variable `ANT_HOME` in your system.  
Add its bin folder to the `PATH` environment variable.

```bash
vi ~/.bash_profile
```

添加：

```bash
# ant
# BIN folder should include both ant and antRun
# If installed with brew, it should be "/usr/local/Cellar/ant@1.9/1.9.x/libexec/bin"
export ANT_HOME=/usr/local/Cellar/1.10.10/libexec
export PATH=$PATH:$ANT_HOME/bin
```

## Install gradle

```bash
brew install gradle
# brew install gradle@6
brew upgrade gradle
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

## 通过 `yarn global add` 安装

- [ ] [**projj**](https://github.com/popomore/projj)，github/gitlab 项目管理
- [ ] [**serve**](https://github.com/zeit/serve)，本地静态服务器
- [ ] [**fkill**](https://github.com/sindresorhus/fkill)，比 kill 好用的进程 killer
- [ ] [**qrcode-terminal**](https://github.com/gtanner/qrcode-terminal)，二维码生成

# 其他设置

## Hexo 博客

安装 Hexo（参考：[Git Pages + Jekyll/Hexo Build your own blog](../Git-Pages-Jekyll-Hexo-Build-your-own-blog.html#step1-安装-hexo)）

```bash
$ npm install -g hexo-cli
```

## Mac 显示隐藏文件 命令 comand finder

```bash
defaults write com.apple.finder AppleShowAllFiles Yes && killall Finder //显示隐藏文件

defaults write com.apple.finder AppleShowAllFiles No && killall Finder //不显示隐藏文件
```
