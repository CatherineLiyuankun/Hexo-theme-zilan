---
title: 程序猿的那些好用工具
catalog: true
subtitle: awesome-tools
header-img:
tags:
- MAC
categories:
- TECH
- Tools
---
本文在[awesome-tools](https://github.com/sorrycc/awesome-tools)基础上修改，添加自己使用的工具。有些是我也已经用的软件，有些是根据这篇文章才开始用的。
> 从 [Blog](https://github.com/sorrycc/blog/issues/83) 迁移到 GitHub 仓库维护，可以有历史记录。

# 翻墙

主 [**rixcloud**](https://home.rixcloud.me/aff.php?aff=1432)，备**阿里云香港**和**公司翻墙**。

- [ ] rixcloud 比较稳，特殊时期也能用，支持 surge 客户端，支持 netflix
- [ ] 软件方面，Mac 下用 [**ShadowsocksX-NG-R**](https://github.com/qinyuhang/ShadowsocksX-NG-R/releases)，iPhone 下用 [**ShadowRocket**](https://itunes.apple.com/us/app/shadowrocket/id932747118?mt=8)（切美区下载）
- [ ] 通过 [**Proxifier**](https://www.proxifier.com/) 实现命令行应用或其他应用翻墙，比如 iTerm2 下执行 npm publish 偶尔会被墙，并且实测下来比 `export http_proxy` 快
- [ ] 家里的路由器翻墙是用 [**RT-AC88U**](https://www.asus.com/us/Networking/RT-AC88U/) + **梅林小宝版固件**
- [ ] 电视上看 youtube 和 netflix 可以用 [**Nvidia Shield TV**](https://www.nvidia.com/en-us/shield/)，我买的美版，据说国版也可刷原生系统

# Mac 软件

- [ ] 用了 [SetApp](https://go.setapp.com/invite/sorrycc)，包含以下的不少付费应用，能省不少钱。

## 编辑器

- 主 [**VSCode**](https://code.visualstudio.com/) + [**IntelliJ**](https://www.jetbrains.com/idea/)
- 辅 [**WebStorm**](https://www.jetbrains.com/webstorm/)和 **Vim**。如果没有时间去折腾插件，那就选 WebStorm， 无需安装插件就很好用。

<!-- - [ ] 字体用 [**Dank Mono**](https://dank.sh/) 和 [**Operator Mono**](http://www.typography.com/fonts/operator/overview/)，轮着用，看厌一个切另一个
- [ ] WebStorm 使用 [**material-theme-jetbrains**](https://github.com/ChrisRM/material-theme-jetbrains)，Theme 选 Material One Dark，字号 16 号，行距 1.2，[效果图](https://gw.alipayobjects.com/zos/rmsportal/JKRPNvvHhPgFonHHXvPe.png)
- [ ] WebStorm 插件额外装了 **File Watchers**、**GitLink**、**Import Cost**、**Prettier** 和 **Rainbow Brackets** -->
- [x] [Vscode 配置和插件](http://liyuankun.top/Vscode-配置和插件.html)。

## Terminal

- [x] Terminal 用 [**iTerm2**](https://www.iterm2.com/) + [**zsh**](https://en.wikipedia.org/wiki/Z_shell) + [**oh-my-zsh**](https://github.com/robbyrussell/oh-my-zsh) 的组合，主题是 [robbyrussell](https://github.com/robbyrussell/oh-my-zsh/blob/master/themes/robbyrussell.zsh-theme)
- [x] zsh 的插件开了 git、autojump、brew、git、git-extra、git-flow、git-prompt、git-remote-branch、github、gitignore、history、history-substring-search、iterm2、node、npm、npx、nvm、tig、vscode、yarn、[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
- [] iTerm2 里配 `Run command...` 为 `/usr/local/bin/idea --path \2 \1` ([图](https://zos.alipayobjects.com/rmsportal/RmWdxKRQUWFMoVDjerNQ.png))，这样 Command + 点击文件路径，就会在 Intellij Idea 里打开
- [Mac 配置在Finder里用iTerm2打开当前目录](http://liyuankun.top/%E5%A5%A5%E5%88%A9%E7%BB%99%E4%BD%A0%E7%9A%84iTerm2-%E5%BF%AB%E9%80%9F%E7%94%A8IDE%E6%89%93%E5%BC%80%E6%96%87%E4%BB%B6.html#mac-%E9%85%8D%E7%BD%AEfinder%E5%BD%93%E5%89%8D%E7%9B%AE%E5%BD%95%E6%89%93%E5%BC%80iterm2)
  - [x] 方法一：安装Go2Shell【MAC OS 版本 <= Big Sur】,  `!!!!!亲测版本V2.5, Mac OS Big Sur可以使用，Monterey不能使用`【我的百度网盘】
  - [x] [方法二：安装OpenInTerminal【MAC OS 版本 >= Monterey】](http://liyuankun.top/%E5%A5%A5%E5%88%A9%E7%BB%99%E4%BD%A0%E7%9A%84iTerm2-%E5%BF%AB%E9%80%9F%E7%94%A8IDE%E6%89%93%E5%BC%80%E6%96%87%E4%BB%B6.html#%E9%99%A4go2shell%E7%9A%84%E5%85%B6%E4%BB%96%E6%96%B9%E6%B3%95-mac-os-%E7%89%88%E6%9C%AC-monterey)
    - [OpenInTerminal](https://github.com/Ji4n1ng/OpenInTerminal/blob/master/Resources/README-zh.md)  【推荐】个人目前选择使用这个开源软件了，不仅可以用iTerm2打开，还可以配置用其他IDE例如VScode, sublime打开。
- [x] 配置[MAC终端命令行下用sublime、vscode、atom打开文件或目录](https://www.cnblogs.com/hongrunhui/p/5928833.html)
  - [x] open .  用finder打开当前文件
  - [x] vsc .  用vscode打开当前文件
  - [x] subl .  用Sublime打开当前文件
  - [x] atom .  用Atom打开当前文件
  - [x] command + <-  / ->     切换tab
  - [x] control + w 回退一部分命令
- [tldr](https://tldr.sh/) Simplified and community-driven `man` pages. Quick install: `npm install -g tldr`.
  - Take `git` for example, while `man` `git` outputs more than 100 lines. `> tldr git`

## 开发辅助

- [x] [**Dash**](https://kapeli.com/dash) 快速查API文档。免费版本会在你搜索完后等10秒再显示，付费版：$29.99 无需等待。
- [x] [**SourceTree**](https://www.sourcetreeapp.com/)，git 辅助，由于 git 高级操作命令记不住，就只用借助 UI 了。
- [x] [**Paw**](https://paw.cloud/)，请求模拟，前后端联调API时用这个先走一遍。
- [x] [**Postman**](https://www.postman.com/)，请求模拟，前后端联调API时用这个先走一遍。
- [x] [**R**]()
- [x] [**RStudio**]()

- [x] [**Colloquy**]()
- [x] [**Cyberduck**](https://cyberduck.io/)
- [x] [**VNC Viewer**](https://www.realvnc.com/en/connect/download/viewer/)
- [x] [**Microsoft Remote Desktop**]() [APP Store] 美版账号

<!-- - [ ] [**Github Desktop**](https://github.com/desktop/desktop)，管理 github 仓库的变更和 PR，代替了 SourceTree 的部分工作，可以方便地把别人的 PR checkout 到本地验证 -->
- [x] [**Gas Mask**](https://github.com/2ndalpha/gasmask) ，[Hosts 管理](https://zhuanlan.zhihu.com/p/20466912)
- [x] [**ColorSnapper2**](https://colorsnapper.com/)，取色工具。付费，App store 没有。

### 抓包

- [x] [**Charles**](https://www.charlesproxy.com/)，抓包用，支持 https, 不免费，公司提供的付费账号。
- [x] [**OWASP ZAP**](https://www.zaproxy.org/download/) ​
  - ​开源免费的安全代理工具​​：由全球非营利组织 ​​OWASP​​ 开发和维护，提供完全免费的Web应用程序安全扫描与渗透测试功能，适用于开发、测试及生产环境。
  - ​​核心功能全面覆盖​​：支持​​被动扫描​​（自动分析流量）、​​主动扫描​​（模拟攻击探测漏洞如SQL注入/XSS）、​​爬虫遍历​​、​​模糊测试​​及​​代理拦截​​，可深度检测Web应用的安全风险。
  - ​​跨平台与易用性​​：兼容 ​​Windows、Linux、macOS​​ 及 ​​Docker​​，提供图形化界面与命令行操作，首次使用时通过浏览器代理配置（默认端口8080）即可快速启动扫描。
  - ​​灵活扩展与集成​​：支持超过100种插件（如主动扫描规则、Ajax爬虫），可通过API集成到 ​​CI/CD流水线​​ 实现自动化测试，并生成 ​​HTML/XML/Markdown​​ 格式的详细漏洞报告。
  - ​​适用多角色场景​​：既适合​​安全专家​​手动渗透测试（如断点调试、请求重放），也满足​​开发者与测试人员​​在开发阶段进行自动化漏洞扫描，提升应用安全性。
- [x] [**Progress Telerik Fiddler**]()
- [x] [**Wireshark**]()

### 虚拟机

- [x] [**ParallelsDesktop**]()
- [x] [**VirtualBox**]()

### 数据库

- [x] [**Sequel Pro**](https://www.sequelpro.com/)，Mysql数据库客户端, 开源客户端，目前只有Mac版本。
- [x] [**DB Browser for SQLite**]()
- [x] [**MongoDB Compass**]()

### 浏览器

- [x] [**Google Chrome**](https://www.google.com/chrome/) + [**Google Chrome Canary**](https://www.google.com/chrome/canary/) + [**Firefox**](https://www.mozilla.org/en-US/firefox/new/) + **Safari**，浏览器，调试用，IE 的测试会借助内网的云测平台

## 输出

<!-- - [ ] [**Ulysses**](https://ulysses.app/)，笔记工具，从 [Bear](http://www.bear-writer.com/) 和 [Notion](https://www.notion.so/?r=159be429981b4725ad6f36c4f599bd98) 切到 Ulysses -->
- [x] [**Onenote**](https://www.onenote.com/signin?wdorigin=ondc)，笔记工具，从 [Evernote印象笔记](https://evernote.com/intl/zh-cn) （原来是会员，现在只是免费版） 切到 Onenote，感觉Onenote对markdown支持不好（只有windows版本有插件可以支持markdown），准备换[**Ulysses**](https://ulysses.app/)。不过我现在markdown一般都用vscode+github来写了。
<!-- - [ ] [**OmniGraffle**](https://www.omnigroup.com/omnigraffle) + [**iThoughtsX**](https://www.toketaware.com/ithoughts-osx) + iPad 上的 [**Whiteboard**](https://apps.apple.com/us/app/microsoft-whiteboard/id1352499399)，分别用于画架构图和和脑图 -->
- [x] [**OmniGraffle**](https://www.omnigroup.com/omnigraffle) + [**Xmind**](https://www.xmind.net/) + iPad 上的 [**Whiteboard**](https://apps.apple.com/us/app/microsoft-whiteboard/id1352499399)，分别用于画架构图和和脑图
<!-- - [ ] [**LICEcap**](http://www.cockos.com/licecap/) ，GIF 录屏工具 -->
- [x] [**Gif Brewery 3**](https://apps.apple.com/cn/app/gif-brewery-3-video-to-gif/id1081413713?l=en&mt=12) ，GIF 录屏工具, 可以直接录屏并转换成gif动图。免费，App store 下载。

## 输入

- [x] [**Reeder**](http://reederapp.com/mac/)，RSS 阅读软件
<!-- 我的主要信息来源，没有提供 rss 源的我会先在 [**rsshub.app**](https://docs.rsshub.app/) 上找，再没有就自己写一个 serverless 服务部署在 [now](https://zeit.co/) 上，[now使用方法](http://object.ws/2017/09/10/nowsh-note/) -->
- [x] [**Kiwi for Gmail**](http://kiwiforgmail.com/)，Gmail 客户端, 我用的免费的lite版，App store 要切换到美国。

## 效率

- [x] [**Alfred**](https://www.alfredapp.com/) + [**Powerpack**](https://www.alfredapp.com/powerpack/)，应用启动、粘贴板管理、Workflow、Snippets 管理等。 同步问题可以参考：[Alfred 中如何在不同电脑上同步自定义设置？](https://www.zhihu.com/question/39098799) 和 [在Mac之间同步您的Alfred设置](https://mac.orsoon.com/news/337637.html)。免费功能：File search, Web search，app启动, Calculator, Dictionary, System。付费功能（需购买Powerpack）：Workflow，Action, Clipboard History，Snippets, Contacts, itunes, 1Password, Terminal.
<!-- - [ ] [**Paste**](https://pasteapp.me/)，粘贴板管理，[**Copied**](https://copiedapp.com/) 在 mac 10.15 下有 bug 就放弃了，再之前一直用 Alfred 的粘贴板 -->
<!-- - [ ] [**TaskPaper**](https://www.taskpaper.com/)，任务管理 -->
<!-- - [ ] [**OmniFocus**](https://www.omnigroup.com/omnifocus) ，任务管理，通过 Omni Sync Server 和 iPhone 同步 -->
- [x] [**TickTick滴答**](https://dida365.com/) ，任务管理，有MAC版和iPhone版，可以同步。
- [x] [**Thor**](https://github.com/gbammc/Thor)，一键直达应用， 免费，开源。
- [x] [**Karabiner Element**](https://pqrs.org/osx/karabiner/)，用于[把右 Command 和 Capslock 键利用起来](http://lucifr.com/2013/02/16/caps-lock-to-hyper-key/)，避免快捷键冲突，[简单 note](https://hackmd.io/s/rk4u9i-pG)，详见[sorrycc的《我的快捷键技巧》](https://www.bilibili.com/video/av44127555).
  - [ ] [Karabiner-Elements不生效解决方法](./Karabiner-Elements不生效.html)

## 摄影相关

### 图片
<!-- - [ ] [**ScreenFlow**](http://www.telestream.net/screenflow/overview.htm)，视频录制和剪辑 -->
<!-- - [ ] [**Final Cut Pro**](https://www.apple.com/final-cut-pro/)，视频剪辑 -->

- [x] [**imageoptim**](https://imageoptim.com/mac)免费且开源的 Mac 图片无损压缩优化工具。默认设置下，它的压缩号称是「无损」的，也就是说画质不会被改变，但体积却可以被减小。ImageOptim 支持 PNG、JPG、GIF 格式的图片压缩优化，你只需将文件拖放到它的界面上即可完成优化 (PS：处理后会覆盖原图 / 原图被移到垃圾桶，可手工恢复)，支持批量，使用上非常简单方便。
- [x] [**Image Capture**](https://www.pcpc.me/tech/mac-image-capture)macOS预先安装，自带app。可以使用iTunes或照片将iOS设备，相机或SD卡中的照片导入Mac。但是，如果您在使用这些应用程序时遇到麻烦，或者您希望使用界面更简单的应用程序，请尝试使用Image Capture。
- [x] [**Luminar 2018**](https://skylum.com/luminar) 修图工具。限时免费的时候下载的。

### 视频

- [x] [**RDM**](https://github.com/avibrazil/RDM)，分辨率切换，允许设置未支持的分辨率，比如我会在录屏时设置 720p(hd) 的分辨率。在使用多个外接显示屏的时候，也可以调整外接显示屏的分辨率，很方便。免费，开源。
- [x] [**KeyCastr**](https://github.com/keycastr/keycastr)，你在键盘上按了哪些键，会显示在屏幕上，适合录屏的时候使用。通过 homebrew cask 安装: `brew cask install keycastr`。记得mac设置Security & Privacy下的Input monitoring 和 Accessibility里面要加上并勾选。顺便把开始显示键盘的快捷键设置成了F19 + k。免费，开源。
- [x] [**DaVinci Resolve 16**](https://www.blackmagicdesign.com/products/davinciresolve/) 达芬奇，视频剪辑，有免费版本，影视飓风在B站有免费教程。
- [x] [**Blackmagic RAW Player**](https://apps.apple.com/cn/app/blackmagic-raw-player/id1435415804?mt=12) Blackmagic RAW Player是观看Blackmagic RAW格式片段的理想选择。Blackmagic RAW Player能够播放Blackmagic RAW格式的媒体文件，以及扩展名为.braw的媒体文件。App store 有，免费。
- [x] [**Blackmagic RAW Speed Test**](https://apps.apple.com/cn/app/blackmagic-raw-speed-test/id1466185689?mt=12) Blackmagic RAW Speed Test是一套CPU和GPU衡量工具，可用于测试系统上解码全分辨率Blackmagic RAW帧的速度。测试中多个CPU内核和GPU会被自动检测和使用，为您提供准确实际的结果。只需选择Blackmagic RAW固定比特率3:1、5:1、8:1或12:1，以及您想要的分辨率即可执行测试。测试结果以简单明了的表格形式展示，显示了您的计算机每秒解码所有支持分辨率的帧数。App store 有，免费。
- [x] [**PluralEyes 4**](https://www.blackmagicdesign.com/products/davinciresolve/) Red Giant PluralEyes for mac是Mac平台上一款专业的音视频同步剪辑软件，pluraleyes 4 mac支持使用轨道和媒体剪辑、跨区剪辑、临时同步文件、调整同步结果、微调同步、导出为媒体文件、导出时间轴等功能，能够轻松处理多机位的音视频同步问题。付费。

- [ ] [**Softorino YouTube Converter**](https://softorino.com/youtube-converter)，免费24小时，之后付费，YouTube 视频下载
- [ ] [**youtube-dl**](https://github.com/ytdl-org/youtube-dl/blob/master/README.md#readme) [命令行视频下载利器，选择下载视频，或是将视频流直接导出到自己想使用的播放器中](https://zhuanlan.zhihu.com/p/27718783)。国内类似版本： [You-Get](https://github.com/soimort/you-get)，对国内平台支持的更好。
<!-- - [ ] [**Downie 3**](http://software.charliemonroe.net/downie.php)，通用视频下载，付费，SetApp含有 -->
- [ ] [**Folx 5**](https://mac.eltima.com/download-manager.html) + [**qBittorrent**](https://www.qbittorrent.org/) + [**Motrix**](https://motrix.app/)，下载工具，Folx 下 http，qBittorrent 下 magnet，Motrix 是 aria2 的封装，可以[下百度云盘、115 等](https://www.yuque.com/moapp/help/extensions)
- [ ] [**f.lux**](https://justgetflux.com)，调节显示器色温，护眼，尤其是早上起来屏幕实在是刺眼
- [x] [**IINA**](https://github.com/iina/iina)，[IINA](https://iina.io/)视频播放。原来用的[VLC media player](https://www.videolan.org/vlc/index.zh.html)，后来[改用IINA](https://www.zhihu.com/question/19552878/answer/139035466)。开源，免费。

### 作图

- [x] [**SketchUp 2018**]()

## 其他

- [x] [**CleanMyMac **](https://macpaw.com/cleanmymac)，系统清理， 付费。
- [x] [**OmniDiskSweeper **](https://www.omnigroup.com/more) 系统文件清理。开源免费软件。

- [ ] [**1Password**](https://1password.com/)，密码管理
- [x] [**Last Password**](https://www.lastpass.com/)，密码管理 浏览器插件免费，手机app需要Premium会员（我iphone上用苹果的密码记录,就没使用Last Password）, 1Password也不错，这两个都可以。
<!-- - [ ] [**Bartender 3**](https://www.macbartender.com/)，管理系统右上菜单项，隐藏或收起不常用的，付费。 -->
- [x] [**KeepingYouAwake**](https://github.com/newmarcel/KeepingYouAwake)，可保证Mac系统不自动休眠。原来用的[Caffeine](http://lightheadsw.com/caffeine/)，但是[MacOS更新到Mojave以后就不管用了](https://www.reddit.com/r/osx/comments/9pbl9u/macos_mojave_caffeine_replacement/)。可以改用Amphetamine 或者 KeepingYouAwake。免费，开源。

- [x] [**Perculia**](https://itunes.apple.com/cn/app/perculia/id1462633284?mt=12) - 蓝牙设备管理，可以一键连耳机。App store 有，免费。
- [ ] [**截图**](https://jietu.qq.com/)，顾名思义，腾讯出的截图工具，App store 有，免费。
- [x] [**RunCat**](https://itunes.apple.com/nz/app/runcat/id1429033973?mt=12&ref=appinn) - 菜单栏显示奔跑的小猫，CPU 占用率越高跑地越快。App store 有，免费。
- [x] [**Slack**](https://slack.com/downloads/mac) + [**QQ**](https://im.qq.com/macqq/) + [**微信**](https://mac.weixin.qq.com/) + [**钉钉**](https://tms.dingtalk.com/markets/dingtalk/download)，通讯交流。App store 有，免费。
- [ ] [**Tuxera NTFS**](https://www.tuxera.com/products/tuxera-ntfs-for-mac/) - 支持 NTFS 格式硬盘，付费。
- [x] [**Microsoft NTFS for Mac by Paragon Software**](https://www.seagate.com/pl/pl/support/software/paragon/) - 支持 NTFS 格式硬盘，因为原来买了希捷的移动硬盘，送的软件，一般、够用。
- [x] [DriveDx](https://apps.apple.com/dk/app/drivedx/id526290112?mt=12) – 磁盘健康检测和监控工具，付费。

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

## Chrome 插件

### Github 相关

- [ ] [**OctoLinker**](https://github.com/OctoLinker/browser-extension)，根据 require/import 或 package.json 中的 dependencies 进行快速跳转
- [x] [**Refined Github**](https://github.com/sindresorhus/refined-github)，Github 改进
- [ ] [**npmhub**](https://github.com/npmhub/npmhub)，在 README 下方显示 npm 依赖信息
- [ ] [**Hide Files on GitHub**](https://github.com/sindresorhus/hide-files-on-github)，隐藏配置文件等非必要文件
- [ ] [**Github Hovercard**](https://github.com/Justineo/github-hovercard)，比如不用点进去就能看到 issue 详情
- [x] [**Git History Browser Extension**](https://chrome.google.com/webstore/detail/git-history-browser-exten/laghnmifffncfonaoffcndocllegejnf)，可视化的方式显示文件修改历史
- [x] [**File Icon for GitHub, GitLab and Bitbucket**](https://chrome.google.com/webstore/detail/file-icon-for-github-gitl/ficfmibkjjnpogdcfhfokmihanoldbfe)，更好看的文件 icon
- [x] [**octotree**](https://github.com/ovity/octotree)，显示文件树形目录

### 其他

- [x] [**Workona**](https://workona.com/)，tab 管理，基于使用场景，[Chrome插件地址](https://chrome.google.com/webstore/detail/workona/ailcmbgekjpnablpdkmaaccecekgdhlh?hl=en-GB)。非常推荐，让我可以抛弃原来的oneTab插件了，非常适合我这种什么网页都舍不得关的人。
- [x] [**Grammer**](https://app.grammarly.com/)，语法提醒插件，拼写错误和语法错误都可以提醒，主要辅助我工作上的英文交流。它现在不仅有浏览器插件、office插件，Mac上也有app了.
- [x] [**JSON Formatter**](https://github.com/callumlocke/json-formatter)，让 JSON 更易读
- [ ] [**Better History**](https://chrome.google.com/webstore/detail/chrome-better-history/aadbaagbanfijdnflkhepgjmhlpppbad?hl=en)，搜索历史记录用
- [ ] [**Tampermonkey**](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)，油猴，通过脚本定制网页
- [ ] [**uBlock Origin**](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm)，广告 Block
- [ ] [**Netflix Rating**](https://chrome.google.com/webstore/detail/imdb-ratings-for-netflix/dnbpnlalaijjbogmjbpdkdcohoibjcmp/related?hl=en)，在 netflix 上显示每个影片的 IMDB 的评分信息
- [ ] [**Select like a boss**](https://chrome.google.com/webstore/detail/select-like-a-boss/mnbiiidkialopoakajjpeghipbpljffi/related?hl=en)，可以选择链接里的内容
- [ ] [**Lingocloud Interpreter**](https://chrome.google.com/webstore/detail/lingocloud-interpreter/jmpepeebcbihafjjadogphmbgiffiajh/related)，全文翻译
- [ ] [**Video Speed Controller**](https://chrome.google.com/webstore/detail/video-speed-controller/nffaoalbilbmmfgbnbgppjihopabppdk/related?hl=en)，在视频上显示按钮可控制播放速度

# Mac 设置

- [x] [固定MAC窗口顺序](https://www.zhihu.com/question/49530172)

# iPhone 软件

## 每天用

- [x] **支付宝**
- [x] **微信**
- [x] **Chrome**，代替 Safari，好处是可以和电脑同步
- [x] **Gmail**
- [ ] **Reeder**，我是 RSS 重度用户
- [x] **钉钉**，工作交流
- [ ] **Shadowrocket**，你懂的，需切换美区安装
- [x] **Twitter**，感觉官方客户端够用了
- [ ] **Workflow**，最常用的一个 workflow 是 clipboard to instapaper，用于把微信文章经由 instapaper 保存到 github issue
- [x] **网易云音乐**
- [ ] **OmniFocus**，任务管理

更多 <https://github.com/sorrycc/ama/issues/12>

# 在线服务

### 免费

- [x] [**refiddle**](http://refiddle.com/) + [**regex101**](https://regex101.com/)，调正则表达式
- [x] [**30 seconds of code**](https://30secondsofcode.org/)，代码片段
- [x] [**astexplorer**](https://astexplorer.net/)，调 ast
<!-- - [ ] [**globtester**](http://www.globtester.com/)，调 glob -->
- [x] [**ghub.io**](http://ghub.io/)，redirect to an npm package's repository page
- [x] [**unpkg**](https://unpkg.com/)，npm 包的 cdn 服务，可以查看 npm 包发布后的内容
- [x] [**sketchboard**](https://sketchboard.me/) + [**draw.io**](https://www.draw.io/) + [**MindMeister**](https://www.mindmeister.com/) + [**Whimsical**](https://whimsical.com/)，在线画流程图
- [x] [**HackMD**](https://hackmd.io/recent)，在线笔记，有 PPT 展示功能
- [x] [**Slides**](https://slides.com/)，PPT 制作，带动画
- [x] [**CodeSandbox**](https://codesandbox.io/) + [**glitch**](https://glitch.com/) + [**repl.it**](https://repl.it/)+[codepen](https://codepen.io/)，在线代码编辑，前者支持 sandbox container，可以跑 npm scripts
- [x] [**node.green**](https://node.green/)，查询 NodeJS 的 ES2018 特性支持情况
- [x] [**Can I use**](https://caniuse.com/)，查询浏览器的特性支持情况
- [x] [**carbon**](https://carbon.now.sh/)，根据源码生成图片
- [x] [**Tell me when it closes**](https://tellmewhenitcloses.com)，github issue 关闭时发送邮件通知
- [x] [**Package Diff**](https://diff.intrinsic.com/)，比较 npm 包两个版本直接的区别
- [x] [**Firefox Send**](https://send.firefox.com/) + [**ffsend**](https://github.com/timvisee/ffsend)，文件分享服务
- [x] [**Cloud Convert**](https://cloudconvert.com/)，支持 218 种格式相互转换
- [x] [**SVGR**](https://www.smooth-code.com/open-source/svgr/playground/)，SVG 转 React 组件
- [x] （beta）[**Webpack config tool**](https://webpack.jakoblind.no/)，webpack 配置工具

### 付费

- [x] [**Oreilly Safari Books**](https://www.safaribooksonline.com/)，Oreilly 图书、视频教程、newsletter 等。付费，公司报销，很划算，等于我没掏钱。
<!-- - [ ] [**Frontend Masters**](https://frontendmasters.com/)，视频教程 -->
<!-- - [ ] [**Zeit Now**](https://zeit.co/now)，serverless 服务，域名等 -->
<!-- - [ ] [**name.com**](https://www.name.com/)，域名服务，之后会转到 Zeit Now 上 -->
<!-- - [ ] [**少数派 Power+ 2.0**](https://sspai.com/series/70)，提效相关文章 -->
- [x] [**网易云音乐**](https://music.163.com/)
<!-- - [ ] **百度云盘** + **115 网盘** + [**麦果网盘中转**](https://www.maiguopan.com/)，资料下载 -->
- [x] **爱奇艺**（苏宁会员） + **腾讯视频** + **优酷**（88会员） + **bilibili**，会员去广告
<!-- - [ ] [**Netflix**](https://www.netflix.com)，蹭 [pigcan](http://github.com/pigcan) 的账号 -->
<!-- - [ ] [**Youtube Premium**](https://www.youtube.com/)，主要为了 iPhone 上切换应用或锁屏后能继续播放 -->
<!-- - [ ] [**SetApp**](https://go.setapp.com/invite/sorrycc)，喊几个好友一起买，可以省不少钱 -->

# 硬件

## 电脑

- [ ] **MacBook Pro 15-inch, 2017**，公司配的，512 G 不太够用，但还行吧。自己的电脑**MacBook Pro 15-inch, 2013**准备用[三星 970](https://detail.tmall.com/item.htm?id=569327401210&spm=a1z09.2.0.0.76a52e8dZEojbU&_u=l1h6urtf206) 升了 1T 硬盘

## 电脑配件

<!-- - [ ] [**U28E590D**](https://detail.tmall.com/item.htm?id=523282229383) x2，三星显示器，应该是 4K 中最便宜的了 -->
- [ ] [**AOC 32英寸4K曲面显示器**](https://detail.tmall.com/item.htm?id=594024489687&spm=a1z09.2.0.0.260f2e8drJ2dpC&_u=cgkogtg55d4&sku_properties=5919063:6536025) 公司用的dell，家里用的AOC 32英寸4K曲面显示器。
<!-- - [ ] (**HHKB Pro 2 无刻** + [彩色键帽](https://item.taobao.com/item.htm?id=522721338431&_u=41h6urte838)) x2 -->
- [ ] [**带有数字小键盘的妙控键盘 - 银色**](https://www.apple.com.cn/shop/product/MRMH2CH/A?fnode=7b42677784b656a8070a65a4b45fb9bb0e53cf839f4843024382ab3c691eb0cad59601137a779152887a1ae9e81734d538be3e41128798b0946b68981dd0cc35f7adcc869bf70d088fdf71fc297938893a63c6baa2e12bbb3f288516a56954e5)
<!-- - [ ] [**Razer DeathAdder Chroma**](http://www.razerzone.com/store/razer-deathadder-chroma) x2 -->
- [ ] [**罗技无线鼠标**]()

## 家庭网络

<!-- - [ ] J1900 软路由 + UBNT 交换机 + （UBNT AP & [**华硕 RT-AC88U**](https://item.jd.com/2104499.html)） -->

## 手机

- [x] [**iPhoneXS MAX**](https://www.apple.com/iphone-x/)

## 耳机

- [x] [**Sony/索尼 WH-1000XM3**](https://detail.tmall.com/item.htm?id=577955986589&spm=a1z09.2.0.0.260f2e8drJ2dpC&sku_properties=5919063:6536025)，头戴式无线降噪蓝牙耳机1000X，天猫618买的。淘口令：(￥kusV1GSXOve￥)

## 相机

- [x] [**Sony A6000**](https://www.fujifilmusa.com/products/digital_cameras/x/fujifilm_x100t/) 准备换A7
- [x] [**大疆手机稳定器**](https://zh.shop.gopro.com/China/cameras/hero7-black/CHDHX-701-master.html)

# 参考链接

[awesome-tools](https://github.com/sorrycc/awesome-tools)
<!-- - [ ] [awesome-f2e-libs](https://github.com/sorrycc/awesome-f2e-libs) -我关注的前端库。
- [ ] [旧版本的装了啥](https://github.com/sorrycc/blog/issues/16) -->

## RSS 阅读器

Reeder 好，MACOS+IOS 但是要付费
NetNewsWire 免费，只有IOS

名称 | 内容简介 | 缺点 | 适用平台 | 评分
---|------|------|---|---
[InoReader](https://www.inoreader.com/?lang=zh_CN) | 用户体验非常好，界面简洁而且漂亮，不限制订阅源。 | 速度慢，有广告。 | Web/IOS/Android | 9.1
[Feedly](https://feedly.com/) | 老牌阅读器，创建于2008年，有网页版和手机APP。 | `部分功能收费`，速度慢。 | Web/IOS/Android | 9.0
[TinyTinyRSS](https://tt-rss.org/) | `开源免费`的RSS阅读器，功能上可以满足大部分人的需要。| 需要自己购买空间搭建。 | PC/手机 | 9.0
[Reeder](http://reederapp.com/) | IOS和Mac最佳RSS阅读器。| 没有网页版，产品为`付费`。 | IOS/Mac | 8.9
[NetNewsWire](https://ranchero.com/netnewswire/) | `免费`！！| 没有网页版。 | IOS/Mac | 8.9
[Miniflux](https://miniflux.net/) | 一款简洁`开源`RSS阅读器程序，功能简单但是实用。| 需要自己购买空间搭建程序。 | PC | 8.8
[RSSOwl](http://www.rssowl.org/) | 用 Java 编写，跨平台的桌面 Feed 阅读器。有强大的过滤和搜索功能、可定制的通知。| 没有Web, 没有手机端。 | Mac/Win/Linux | 8.6
[Digg Reader](http://digg.com/reader) | 老牌的`免费`在线RSS阅读器，出自Digg旗下，很稳定。| 速度慢，好久没有更新。 | PC/手机 | 8.5
[Feeder](https://feeder.co/) | 一个用户体验不错的RSS阅读器。| 有广告，速度慢。 | PC/手机 | 8.5
[Nextcloud News](https://wzfou.com/nextcloud/) | Nextcloud自带的RSS阅读插件，可以打造成一个RSS阅读器。| 需要自己搭建环境。 | PC/手机 | 8.3
[AOL Reader](http://reader.aol.com/) | 互联网媒体巨头AOL旗下的RSS阅读器。| 速度慢。 | PC/手机 | 8.3
[Feedspot](http://www.feedspot.com/) | 国外一个RSS阅读器，提供中文界面。 | PC/手机 | 8.0
QQ阅读空间 | QQ邮箱自带的一款在线RSS阅读器。| 长期不更新，不支持Https订阅源。 | PC | 8.0
[AZ Reader](http://azreader.net/) | 国内自建的RSS阅读器 | PC | 7.9
[FeedDemon](http://www.feeddemon.com/) | 老牌的RSS阅读器软件，从2013年不再更新，但是不影响使用。| 仅PC软件，无Web和APP。 | PC | 7.9
[Tickr](https://www.open-tickr.net/) | 桌面客户端，会将你的 Feed 标题如滚动新闻那样在桌面横栏上滚动显示。| 仅软件，没有Web和APP | PC | 7.7
[The Old Reader](https://theoldreader.com/) | 国外一家阅读器，有中文，可自定义站点分享。| 免费版最多100个订阅源 | PC/手机 | 7.6
[Bluereader](http://bluereader.org/) | 国产的RSS阅读器，速度快，有网页版和手机APP。| 不稳定，很少更新。 | PC/手机 | 7.5
[一览](http://www.yilan.io/) | 国产RSS阅读器，速度快。| 免费用户最多只能是100个订阅源。 | PC/手机 | 7.5
irreader | 国产RSS阅读器，速度快。除了基本的 OPML 导入外，它还提供了订阅源市场，收录了 600 余款精选 RSS 源，涵盖大部分常用网站。此外，irreader 还自带多种主题切换、 AdBlock 插件等。对于不支持 RSS 的网站，你还可以自定义抓取规则，手动获取更新。支持菜单栏速览功能。不用打开主界面，只需轻点菜单栏图标就能查看订阅内容标题，选择自己感兴趣的进行深入阅读。此外，irreader 的通知系统也十分完善，会聚合近期更新，方便了解更多动态。| 免费用户最多只能是100个订阅源。 | macOS/Win | 未知
[NewsBlur](https://newsblur.com/) | NewsBlur 免费账户支持 Training，Text 视图以及 IFTTT。| 免费用户最多64个源 | PC/手机 | 7.3
[G2Reader](https://g2reader.com/en/) | 国外一个Rss阅读器。| 访问速度慢。 | PC/手机 | 7.2

[四款好用的 RSS 阅读器推荐[全平台支持]](https://zhuanlan.zhihu.com/p/45120897)
[Mac 上的 RSS 阅读工具，你有这些好看实用的选择](https://sspai.com/post/55050)
[2020 RSS 阅读推荐](https://www.v1tx.com/post/best-rss-reader/)

## 请问 Mac 上有哪些硬盘检测工具？[如 Win 上 CrystalDiskInfo、HD Tune 之类](https://www.v2ex.com/t/175051)

DriveDx
可以用brew安装smartmontools查看SMART数据
[MacOS硬盘检测工具](https://kknews.cc/digital/562gly8.html) [SMART Utility 3.2.6](https://www.itpwd.com/215.html)
HD Tune Pro for Mac

### Mac 移动硬盘未挂载-解决办法

[Mac 移动硬盘未挂载-解决办法](https://www.jianshu.com/p/56d37a0002d7)
[Mac的移动硬盘不能装载该如何解决?](https://www.cnblogs.com/kaffeetrinken/p/10596740.html)
[Mac 下移动硬盘异常退出修复](https://zhuanlan.zhihu.com/p/83542978)
[解决macOS硬盘HFS+分区无法挂载问题](https://edonymu.com/2017/01/17/%E8%A7%A3%E5%86%B3macos%E7%A1%AC%E7%9B%98hfs%E5%88%86%E5%8C%BA%E6%97%A0%E6%B3%95%E6%8C%82%E8%BD%BD%E9%97%AE%E9%A2%98/)
[在Mac OS X下修复Disk Utility无法修复的移动硬盘分区](http://www.jeepxie.net/article/988702.html)
[请问硬盘修复失败导致无法挂载有什么解决办法吗？](https://www.v2ex.com/t/120433)
