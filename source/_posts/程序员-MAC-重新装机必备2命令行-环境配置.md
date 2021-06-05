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
---

- [x] Terminal 用 [**iTerm2**](https://www.iterm2.com/) + [**zsh**](https://en.wikipedia.org/wiki/Z_shell) + [**oh-my-zsh**](https://github.com/robbyrussell/oh-my-zsh) 的组合，主题是 [robbyrussell](https://github.com/robbyrussell/oh-my-zsh/blob/master/themes/robbyrussell.zsh-theme)
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
- Take `git` for example, while `man` `git` outputs more than 100 lines. `> tldr git`


## 命令行

### 通过 [homebrew](https://brew.sh/) 安装

- [x] [**autojump**](https://github.com/wting/autojump)，目录跳转
- [ ] [**the\_silver\_searcher**](https://github.com/ggreer/the_silver_searcher)，文件搜索，命令行是 ag
- [ ] [**hub**](https://hub.github.com/) - git 扩展
- [ ] [**tig**](https://github.com/jonas/tig) - git 扩展
- [ ] [**bat**](https://github.com/sharkdp/bat)，带行号的 cat，可以配 `alias cat="bat"`
- [ ] [**fd**](https://github.com/sharkdp/fd)，比系统自带的 find 友好

### 通过 `yarn global add` 安装

- [ ] [**projj**](https://github.com/popomore/projj)，github/gitlab 项目管理
- [ ] [**serve**](https://github.com/zeit/serve)，本地静态服务器
- [ ] [**fkill**](https://github.com/sindresorhus/fkill)，比 kill 好用的进程 killer
- [ ] [**qrcode-terminal**](https://github.com/gtanner/qrcode-terminal)，二维码生成

# Mac 显示隐藏文件 命令 comand finder
defaults write com.apple.finder AppleShowAllFiles Yes && killall Finder //显示隐藏文件


defaults write com.apple.finder AppleShowAllFiles No && killall Finder //不显示隐藏文件