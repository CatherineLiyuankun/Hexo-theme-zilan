---
title: 奥利给你的iTerm2-快速用IDE打开文件
catalog: true
date: 2020-05-25 23:26:24
subtitle: Mac 配置Finder当前目录打开iTerm2 Go2Shell or OpenInTerminal
header-img:
tags:
- Command line
categories:
- TECH
- Tools
- Environment setup
---

# [MAC终端命令行下用sublime、vscode、atom打开文件或目录](https://www.cnblogs.com/hongrunhui/p/5928833.html)

打开~/.zshrc

```bash
vim ~/.zshrc
```

添加内容:

```bash
# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"
alias atom='/Applications/Atom.app/Contents/MacOS/Atom'
alias subl='/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl'
alias vsc='/Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin/code'
```

# [Mac 配置Finder当前目录打开iTerm2](https://www.jianshu.com/p/445d3f754c4d)

MAC版本升级到Monterey后，Go2Shell不能使用，转用OpenInTerminal。

- MAC OS 版本 <= Big Sur, 使用Go2Shell
- MAC OS 版本 >= Monterey, 使用OpenInTerminal

## 除Go2Shell的其他方法（MAC OS 版本 >= Monterey）

- 参考文章： [Mac 系統升級， go2shell 不能用了，求大佬們推薦類似功能的軟體](https://xa8.net/post/34806729)整理的几种方法：
  - 直接拖文件夾 /文件到 Dock 上的 iTerm2 的圖標上。。。哈哈，这是一直都有的原生功能，虽然可以。。。但是不好用
  - [OpenInTerminal](https://github.com/Ji4n1ng/OpenInTerminal/blob/master/Resources/README-zh.md)  【推荐】个人目前选择使用这个开源软件了。
  - [cdto](https://github.com/jbtule/cdto)
  - [Alfred 有TerminalFinder workflow](https://github.com/LeEnno/alfred-terminalfinder)
  - [XtraFinder](https://www.macwk.com/soft/xtrafinder)，附贈这个功能： XtraFinder 设置 -> Menus -> 从这里启动，设置个快捷键，选择 iTerm，完事。
  - MAC Automator，找到個更原生的辦法 <http://azaleasays.com/2017/09/21/mac-os-x-open-iterm-here/>

## Go2Shell（MAC OS 版本 <= Big Sur）

### 安装Go2Shell

- [Go2Shell官方安装](http://zipzapmac.com/Go2Shell) 【我的百度网盘】`!!!!!亲测版本V2.5, Mac OS Big Sur可以使用`。

- 苹果应用商店安装[Go2Shell](https://apps.apple.com/cn/app/go2shell/id445770608?mt=12)，只支持Mac OS 到Yosemite。新版Mac OS Big Sur 不能使用。

### 设置Go2Shell

#### 1 进入 Preferences 的方式

1. v2.3 和 v2.5 直接在应用文件中打开 Go2Shell 就行。

2. 新老版本都可以通过命令行打开:

```bash
# 新老版本都可以通过命令行打开
open -a Go2Shell --args configGo
```

#### 2 设置选择

- `iTerm2`
- `New Tab`
  - 优点：Find直接点Go2Shell按钮就可以在当前目录打开终端了
  - 缺点：iTerm2 APPStore 版本每次都是在新的终端窗口中打开，而不是在新的终端标签中打开
- Command to execute in terminal:

```bash
  cd %PATH%; clear; echo -e "Last login: `date`"; pwd
```

![Go2Shell设置](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E5%A5%A5%E5%88%A9%E7%BB%99%E4%BD%A0%E7%9A%84iTerm2-%E5%BF%AB%E9%80%9F%E7%94%A8IDE%E6%89%93%E5%BC%80%E6%96%87%E4%BB%B6/Go2Shell.png)

#### 3 添加Go2Shell 图标到finder

上一步点击： “Install Go2Shell to Finder”后, Finder出现图标：

![Go2Shell图标](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E5%A5%A5%E5%88%A9%E7%BB%99%E4%BD%A0%E7%9A%84iTerm2-%E5%BF%AB%E9%80%9F%E7%94%A8IDE%E6%89%93%E5%BC%80%E6%96%87%E4%BB%B6/Go2Shell2.png)

点击右边这个`>_<`图标，就可以在 iterm2 中以新窗口的模式打开一个 terminal。

> 删除这个功能，或者图标显示错误很好处理，按住 cmd 键，鼠标拖拽这个图标到外面释放图标，就可以删除这个功能了。
> 或者重新打开Go2Shell设置， 点击“Uninstall Go2Shell from Finder”

# Links

- [MAC终端命令行下用sublime、vscode、atom打开文件或目录](https://www.cnblogs.com/hongrunhui/p/5928833.html)
- [Mac 配置Finder当前目录打开iTerm2](https://www.jianshu.com/p/445d3f754c4d)
- [iTerm2 官方文档](https://link.jianshu.com/?t=http://www.iterm2.com/documentation.html)
- [终端环境之iTerm2](https://link.jianshu.com/?t=http://foocoder.com/blog/wo-zai-yong-de-macruan-jian.html/)
- [mac下超好用的终端--iterm2用法与技巧](https://link.jianshu.com/?t=http://blog.csdn.net/thinkdiff/article/details/25075047)
- [使用profiles功能快速ssh机器-Fast SSH Windows With iTerm 2](https://link.jianshu.com/?t=http://hiltmon.com/blog/2013/07/18/fast-ssh-windows-with-iterm-2/) 或者看这篇中文文章 <http://fuweiyi.com/mac/2015/03/06/a-mac-iterm2-ssh-profile.html>
  - - [Mac 系統升級， go2shell 不能用了，求大佬們推薦類似功能的軟體](https://xa8.net/post/34806729)
