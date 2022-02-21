---
title: 程序员-MAC 重新装机必备1软件
catalog: true
date: 2021-05-31 15:24:42
subtitle:
header-img:
tags:
- MAC
categories:
- TECH
- Tools
- Environment setup
---

# 编程必备

- [x] [**Google Chrome**](https://www.google.com/chrome/) 网址下载，或者[APP Store + 国外账号] + [**Google Chrome Canary**](https://www.google.com/chrome/canary/) + [**Firefox**](https://www.mozilla.org/en-US/firefox/new/) + **Safari**，浏览器，调试用，IE 的测试会借助内网的云测平台

## 命令行工具和配置

参考下一篇文章： [程序员-MAC-重新装机必备2命令行-环境配置](../程序员-MAC-重新装机必备2命令行-环境配置.html)

## IDE

- Xcode  [APP Store]
- [Vscode](https://code.visualstudio.com/) + 插件Settings Sync （用gitHub账号创建gist同步配置和插件）+ [Vscode 配置和插件](http://liyuankun.top/Vscode-配置和插件.html)。
- [Toolbox](https://www.jetbrains.com/toolbox-app/) + IntelliJ + PyCharm
- [Sublime](https://www.sublimetext.com/)

## 编程辅助

- [SourceTree](https://www.sourcetreeapp.com/) git 辅助，由于 git 高级操作命令记不住，就只用借助 UI 了。
- [**ColorSnapper2**](https://colorsnapper.com/)，取色工具。付费，App store 没有。
- [Docker Desktop](https://www.docker.com/products/docker-desktop)

## 文件

- [**the-unarchiver**](https://theunarchiver.com/) 【[App store](https://apps.apple.com/us/app/the-unarchiver/id425424353?mt=12), 免费】解压/压缩工具,`brew install --cask the-unarchiver`
 - [**MacZip**](https://ezip.awehunt.com/) 【免费】解压/压缩工具, 查看、编辑压缩包，无需解压！ 
- [**Meld**](http://meldmerge.org/) 文件比较， [git下载](https://github.com/yousseb/meld/releases/)

## 文档查看器

### [Dash](https://kapeli.com/dash) 快速查API文档。免费版本会在你搜索完后等10秒再显示，付费版：$29.99 无需等待
  
  ```bash
  # latest
  brew cask install dash

  # 4.6.7 with license
  brew cask install https://raw.githubusercontent.com/Homebrew/homebrew-cask/baf4f35e70c225fe1a8a60ec3b4e22604187238d/Casks/dash.rb
  ```

### DevDocs.io

[DevDocs.io Git日语](https://github.com/egoist/devdocs-desktop)
[DevDocs.io Git英语](https://github.com/ragingwind/devdogs)

### Zeal

- <https://github.com/zealdocs/zeal>
- [Build Zeal on macOS](http://xavieryao.github.io/article/zeal)
  - [Build Zeal for Mac OS X](https://mazhuang.org/2016/01/16/build-zeal-for-mac-osx/)

## 网络

- [**Paw**](https://paw.cloud/)，请求模拟，前后端联调API时用这个先走一遍。
- [**Postman**](https://www.postman.com/)，请求模拟，前后端联调API时用这个先走一遍。

- [**Charles**](https://www.charlesproxy.com/)，【不免费】抓包用，支持 https, ，公司提供的付费账号。
- [**WireShark**](https://www.wireshark.org/download.html)，抓包用。

- [**Gas Mask**](https://github.com/2ndalpha/gasmask) ，[Hosts 管理](https://zhuanlan.zhihu.com/p/20466912)

## SSH Client

- [Termius](http://www.termius.com/) 【[App store](https://apps.apple.com/us/app/termius-ssh-client/id1176074088?mt=12), 免费】
- [Cyberduck](https://cyberduck.io/download/) 【免费】

## 反编译工具

### JD-GUI

```bash
brew install --cask jd-gui
```

#### JD-GUI报错

打开jd-gui,报错：
`ERROR launching 'JD-GUI' No suitable Java version found on your system! This program requires Java 1.8+ Make sure you install the required Java version.`

- 参见 JD-GUI 的issue ：[Update universalJavaApplicationStub to be able to launch on macOS Big Sur #336](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fjava-decompiler%2Fjd-gui%2Fpull%2F336)

- 解决方法参考文章： [解决mac已经安装jdk1.8但是Java反编译工具JD-GUI还是报错找不到java 1.8+](https://www.cnblogs.com/juhy/p/14193476.html)
sh脚本文件启动执行的JD-GUI，脚本文件在`JD-GUI.app/Contents/MacOS/universalJavaApplicationStub.sh`，里面会判断你安装的jdk版本。
我安装的是openjdk 11.0.11，`where java` 查看路径：`/Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home/bin/java`。

- 修改文件：

```bash
JAVACMD="/Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home/bin/java"
```

- 解决问题，如果还没解决最后没有办法的话，直接进去 cd进入到JD-GUI.app/Contents/Resources/Java目录，然后java -jar jd-gui-1.6.6-min.jar（后面为你自己的jar包名字）来执行

# 效率

- [x] [**Alfred**](https://www.alfredapp.com/) + [**Powerpack**](https://www.alfredapp.com/powerpack/) 【我的百度网盘、硬盘】应用启动、粘贴板管理、Workflow、Snippets 管理等。 同步问题可以参考：[Alfred 中如何在不同电脑上同步自定义设置？](https://www.zhihu.com/question/39098799) 和 [在Mac之间同步您的Alfred设置](https://mac.orsoon.com/news/337637.html)。免费功能：File search, Web search，app启动, Calculator, Dictionary, System。付费功能（需购买Powerpack）：Workflow，Action, Clipboard History，Snippets, Contacts, itunes, 1Password, Terminal. 【我的百度网盘、硬盘】
  - [Alfred auto paste on return 自动粘贴失效解决方法](https://www.jianshu.com/p/594fac7950c4) 确认下 System Preferences -> Security & Privacy -> Accessibility 里有没有勾选 Alfred。如果已经勾上了 取消掉 重新选择勾上试试。
- [x] [**Thor**](https://github.com/gbammc/Thor)，【网址下载】或者[APP Store + 国外账号]一键直达应用， 免费，开源。
- [**Karabiner Element**](https://pqrs.org/osx/karabiner/)，用于[把右 Command 和 Capslock 键利用起来](http://lucifr.com/2013/02/16/caps-lock-to-hyper-key/)，避免快捷键冲突，[简单 note](https://hackmd.io/s/rk4u9i-pG)，详见[sorrycc的《我的快捷键技巧》](https://www.bilibili.com/video/av44127555)
  - “`右 Command”改成F19`: 切换到Complex modifications --> Add rule --> "Change caps_lock to command+control+option+shift." --> 打开文件`~/.config/karabiner/karabiner.json` 把`caps_lock`替换成`right_command`
  ![`caps_lock`替换成`right_command`](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E5%A5%A5%E5%88%A9%E7%BB%99%E4%BD%A0%E7%9A%84iTerm2-%E5%BF%AB%E9%80%9F%E7%94%A8IDE%E6%89%93%E5%BC%80%E6%96%87%E4%BB%B6/Karabiner%20Element.png)
  - 我试了后, 把“右 Command”改成F19,发现我右 Command+delete还是经常用的，所以接着在Karabiner Element 的“Simple modifications” 把 "right_option" 改成了 “left_command”。
  - [遇到了macOS 10.14.6 Karabiner-Elements](https://www.v2ex.com/t/585453) 疑似无法正常使用的问题
  - 另外参考[Mac 自定义应用程序快捷键](https://lhajh.github.io/mac/2017/12/05/.Mac-custom-application-shortcut-keys.html)配置了Mac app，比如Chrome和iterm3的一些快捷键。免费，开源。

- [x] [**KeepingYouAwake**](https://github.com/newmarcel/KeepingYouAwake)，可保证Mac系统不自动休眠。原来用的[Caffeine](http://lightheadsw.com/caffeine/)，但是[MacOS更新到Mojave以后就不管用了](https://www.reddit.com/r/osx/comments/9pbl9u/macos_mojave_caffeine_replacement/)。可以改用Amphetamine 或者 KeepingYouAwake。免费，开源。
- [**TickTick滴答**](https://dida365.com/) ，任务管理，有MAC版和iPhone版，可以同步。[APP Store]
- [x] [**CleanMyMac 3**](https://macpaw.com/cleanmymac) 【我的百度网盘、硬盘】系统清理。
- [x] [RescueTime](https://www.rescuetime.com/dashboard)和[WakaTime](https://wakatime.com/dashboard)来记录你的时间，都有Chrome插件。RescueTime 手机端电脑端都有app。[命令行安装WakaTime](https://wakatime.com/terminal)
- [**runcat **] 【[App store](https://apps.apple.com/us/app/runcat/id1429033973?mt=12), 免费】顶部菜单栏随 CPU 越跑越快的猫。

# 工具

- [百度网盘](pan.baidu.com)
- office 365
- [x] [**Kiwi for Gmail**](http://kiwiforgmail.com/)，Gmail 客户端, 我用的免费的lite版，App store 要切换到美国。
- [x] [**Microsoft NTFS for Mac by Paragon Software**](https://www.seagate.com/pl/pl/support/software/paragon/) - 支持 NTFS 格式硬盘，因为原来买了希捷的移动硬盘，送的软件，一般、够用。
- Photoshop 收费，如果轻量级使用可以用网页在线工具[photopea](https://www.photopea.com/)代替。

## 输出

<!-- - [ ] [**Ulysses**](https://ulysses.app/)，笔记工具，从 [Bear](http://www.bear-writer.com/) 和 [Notion](https://www.notion.so/?r=159be429981b4725ad6f36c4f599bd98) 切到 Ulysses -->
- [x] [**Onenote**](https://www.onenote.com/signin?wdorigin=ondc)，笔记工具，从 [Evernote印象笔记](https://evernote.com/intl/zh-cn) （原来是会员，现在只是免费版） 切到 Onenote，感觉Onenote对markdown支持不好（只有windows版本有插件可以支持markdown），准备换[**Ulysses**](https://ulysses.app/)。不过我现在markdown一般都用vscode+github来写了。

- [x] [**OmniGraffle**](https://www.omnigroup.com/omnigraffle) + [**Xmind**](https://www.xmind.net/)
<!-- - [ ] + iPad 上的 [**Whiteboard**](https://apps.apple.com/us/app/microsoft-whiteboard/id1352499399)，分别用于画架构图和和脑图 -->
- [x] [**Gif Brewery 3**](https://apps.apple.com/cn/app/gif-brewery-3-video-to-gif/id1081413713?l=en&mt=12) ，GIF 录屏工具, 可以直接录屏并转换成gif动图。免费，App store 下载。

## 输入

- [x] [**Reeder**](http://reederapp.com/mac/)，RSS 阅读软件
<!-- 我的主要信息来源，没有提供 rss 源的我会先在 [**rsshub.app**](https://docs.rsshub.app/) 上找，再没有就自己写一个 serverless 服务部署在 [now](https://zeit.co/) 上，[now使用方法](http://object.ws/2017/09/10/nowsh-note/) -->

## 虚拟机

- [x] [**ParallelsDesktop**]()

## 工作必备

- [x] [GlobalProtect](https://vpn.microstrategy.com/global-protect/getsoftwarepage.esp) 【网址下载】 工作 VPN 软件
- [ ] Microsoft Remote Desktop [APP Store] 美版账号
- [ ] Zoom
- [ ] Slack

## 生活娱乐必备

- 各类视频软件
- [**iina**](https://iina.io/)，【免费】多媒体播放器， `brew install --cask iina`

# MAC 设置

## [高效 MacBook 工作环境配置](https://cloud.tencent.com/developer/article/1424480)

## Finder设置

- [10 个实用技巧，让 Finder 带你飞](https://sspai.com/post/27403)

- Mac 显示隐藏文件 命令 comand finder

```bash
defaults write com.apple.finder AppleShowAllFiles Yes && killall Finder //显示隐藏文件

defaults write com.apple.finder AppleShowAllFiles No && killall Finder //不显示隐藏文件
```

## 删除启动台（LaunchPad）残留的图标

- https://zhuanlan.zhihu.com/p/55866195

## 壁纸软件

- [Irvue](https://apps.apple.com/us/app/irvue/id1039633667?mt=12)： 【Apple store 美版账户， 免费】自动换壁纸，就不用再为切换壁纸这件事情消耗过多不必要的时间。它自动获取 Unsplash 上的高质量无版权图片作为壁纸。在其菜单栏菜单中的 Update interval（更新时间）中可以设置更新间隔，从每半小时到每月都可以设置，也可以选择手动更新。
- [Unsplash](https://link.zhihu.com/?target=https%3A//unsplash.com/) ：【Apple store 美版账户， 免费】作为质量最高的免费无版权图片资源网站之一，Unsplash 一直被众多第三方壁纸应用选为图片来源，而这个高质量的照片网站终于有官方的 [Mac 客户端](https://apps.apple.com/us/app/unsplash-wallpapers/id1284863847?mt=12)了。

参考文章：

- [少数派文章：mac桌面壁纸软件](https://www.zhihu.com/question/40021839/answer/257790965)
- [mac有哪些好用的桌面壁纸软件？](https://www.zhihu.com/question/40021839)
