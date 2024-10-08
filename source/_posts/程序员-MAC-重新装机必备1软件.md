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

# 发现好app

- [Product Hunt](https://www.producthunt.com/) 国际最流行的初创公司展示自己产品的平台，这里有各种奇妙的想法和产品，保证能够让你的脑洞大开。在这个平台上，你可以和创始人交流对话，提出意见，并发现各种好玩的产品和工具。简介：科技圈非常有名的平台，在美国有什么新产品（不论网站、APP还是插件）都会先往上前面挂。在国内原来也有些类似产品出现，但最终都没有做下去，而ProductHunt却流量很不错，有一大拨人经常关注着，是获取种子用户做冷启动的首选之地。可以免费上。可以人工影响排名和曝光。
- [G2](https://www.g2.com/) 目前海外最大的软件选型平台，估值是超10亿美元的独角兽，国内SaaS点评网、36氪企服点评等类似网站基本都在学习这家。G2给厂商提供会员、广告、数据等服务，通用类软件流量大。想曝光想好看要花钱，评价审核非常严格。类似网站非常多，当然流量也会少，有些收费有些不收费。同类如GetApp、SaaSWorthy等很多家
- [SaaSHub](https://www.saashub.com/?ref=producthunt) 月访客约200万。介于上面两类之间，有按时间分布的热榜列表，也有产品评价和类似推荐，但网站结构较为简单。类似这种列表、找同类型的网站也有不少。免费上，可以人工干预上榜首。有流量，有转化。
- [Sourceforge](https://sourceforge.net/) 月访客约2100万，比较知名开源软件平台，后来有了专门的商业软件模块，提供面向商业软件的会员服务。如果是开源软件，推荐上去免费获取流量，但是商业软件要在上面推广费用不低，效果看情况。类似开源软件平台还不少，而类似的软件下载站更是非常多，比如流量更大的Softonic，拥有多语言站点，但是入驻麻烦且收费。可免费，可付费，人工干预影响小。
- [PartnerStack](https://partnerstack.com/) 月访客约72万。专门针对SaaS的分销管理 系统&分销平台，帮助厂商管理线索生态伙伴，也帮个人和企业找供应商。在海外线索伙伴是非常重要的，比如HubSpot就曾有很大比例来自于这块。类似平台还有，不多介绍。服务SaaS的SaaS，买吧。（老余也想做一个类似产品，对此有兴趣的朋友欢迎勾搭交流

# 编程必备

- [x] [**Google Chrome**](https://www.google.com/chrome/) + [**Google Chrome Canary**](https://www.google.com/chrome/canary/) + [**Firefox**](https://www.mozilla.org/en-US/firefox/new/) + [**Edge**](https://www.microsoft.com/en-us/edge) + **Safari**，浏览器，调试用，IE 的测试会借助公司.

## 命令行工具和配置

内容略多，用另一篇文章来展开： [程序员-MAC-重新装机必备2命令行-环境配置](../程序员-MAC-重新装机必备2命令行-环境配置.html)

## IDE

- Xcode  [APP Store]
- [Vscode](https://code.visualstudio.com/) + 插件Settings Sync （用gitHub账号创建gist同步配置和插件）+ [Vscode 配置和插件](http://liyuankun.top/Vscode-配置和插件.html)。
- [Toolbox](https://www.jetbrains.com/toolbox-app/) + [**IntelliJ**](https://www.jetbrains.com/idea/) + PyCharm：  用Toolbox来管理和下载IntelliJ，PyCharm
  - [IntelliJ 官方文档-Share settings through a settings repository](https://www.jetbrains.com/help/idea/sharing-your-ide-settings.html#settings-repository)
- [Sublime](https://www.sublimetext.com/)

## Database

- [DB Browser for SQLite](https://sqlitebrowser.org/) DB Browser for SQLite (DB4S) is a high quality, visual, open source tool to create, design, and edit database files compatible with SQLite.
- [MongoDB Compass](https://www.mongodb.com/products/compass) The GUI for MongoDB。

## 编程辅助

- [SourceTree](https://www.sourcetreeapp.com/) git 辅助，由于 git 高级操作命令记不住，就只用借助 UI 了。
- [Docker Desktop](https://www.docker.com/products/docker-desktop)

- [**ColorSnapper2**](https://colorsnapper.com/)，取色工具。付费，App store 没有。

- [Anaconda](https://www.anaconda.com/) Python data science库集合。

## 开发文档查看器

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

- [**Paw**](https://paw.cloud/)，【付费】请求模拟，前后端联调API时用这个先走一遍。
- [**Postman**](https://www.postman.com/)，【免费】请求模拟，前后端联调API时用这个先走一遍。

- [**Charles**](https://www.charlesproxy.com/)，【付费】抓包用，支持 https，公司提供的付费账号。
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

- [x] [**Alfred**](https://www.alfredapp.com/) + [**Powerpack**](https://www.alfredapp.com/powerpack/) 【付费，我的百度网盘、硬盘】应用启动、粘贴板管理、Workflow、Snippets 管理等。 同步问题可以参考：[Alfred 中如何在不同电脑上同步自定义设置？](https://www.zhihu.com/question/39098799) 和 [在Mac之间同步您的Alfred设置](https://mac.orsoon.com/news/337637.html)。免费功能：File search, Web search，app启动, Calculator, Dictionary, System。付费功能（需购买Powerpack）：Workflow，Action, Clipboard History，Snippets, Contacts, itunes, 1Password, Terminal. 【我的百度网盘、硬盘】
  - [Alfred auto paste on return 自动粘贴失效解决方法](https://www.jianshu.com/p/594fac7950c4) 确认下 System Preferences -> Security & Privacy -> Accessibility 里有没有勾选 Alfred。如果已经勾上了 取消掉 重新选择勾上试试。
- [x] [**Raycast**](https://www.raycast.com/)，【开源免费】，Alfred太贵了，Raycast是很好用的平替。"打开application/文件夹"，"snippet"，"剪贴板"等功能都有。

- [x] [**shortcutdetective**](https://formulae.brew.sh/cask/shortcutdetective)，【网址下载】检测keyboard shortcut(hotkey) 冲突， 免费。例如control + A, 可以检测出哪些application设置有这个快捷键，避免冲突。
- [x] [**Thor**](https://github.com/gbammc/Thor)，【网址下载】或者[APP Store + 国外账号]一键直达应用， 免费，开源。
- [x] [**Karabiner Element**](https://pqrs.org/osx/karabiner/)，用于[把右 Command 和 Capslock 键利用起来](http://lucifr.com/2013/02/16/caps-lock-to-hyper-key/)，避免快捷键冲突，[简单 note](https://hackmd.io/s/rk4u9i-pG)，详见[sorrycc的《我的快捷键技巧》](https://www.bilibili.com/video/av44127555)
  - [Karabiner-Elements不生效解决方法](./Karabiner-Elements不生效.html)
  - 另外参考[Mac 自定义应用程序快捷键](https://lhajh.github.io/mac/2017/12/05/.Mac-custom-application-shortcut-keys.html)配置了Mac app，比如Chrome和iterm3的一些快捷键。免费，开源。

## 时间管理

- Apple官方日历，简称iCalendar， 用来日程记录。
- TimeView， [APP Store 免费版限制2个card; 付费版，5.99美元买断] iCalendar并没有提供官方的数据统计和分析功能，所以我们需要借助第三方软件TimeView。TimeView可以理解为是一个数据透视图，透视的数据都来自你在日历中记录的东西。进去之后设置规则，比如我想要统计健身的时间，可以新建一条卡片，设置规则：选取「健康」日历，并包含「健身」关键词。然后我们就可以一张透视统计图，拉取了所有相关的日程，即使课程的命名不规则，只要「健身」关键词标记准确，就可以准确统计。
- [**TickTick滴答**](https://dida365.com/) ，任务管理，有MAC版和iPhone版，可以同步。[APP Store]
- [x] [RescueTime](https://www.rescuetime.com/dashboard)和[WakaTime](https://wakatime.com/dashboard)来记录你的时间，都有Chrome插件。RescueTime 手机端电脑端都有app。[命令行安装WakaTime](https://wakatime.com/terminal)

文章：

- [记录并统计时间都去哪里了](https://sspai.com/post/57956)

## MACOS 工具

- [x] [**KeepingYouAwake**](https://github.com/newmarcel/KeepingYouAwake)，【免费，开源】可保证Mac系统不自动休眠。原来用的[Caffeine](http://lightheadsw.com/caffeine/)，但是[MacOS更新到Mojave以后就不管用了](https://www.reddit.com/r/osx/comments/9pbl9u/macos_mojave_caffeine_replacement/)。可以改用Amphetamine 或者 KeepingYouAwake。
- 【[**runcat **App store](https://apps.apple.com/us/app/runcat/id1429033973?mt=12), 免费】顶部菜单栏随 CPU 越跑越快的猫。
- [x] [**Hidden Bar**](https://github.com/dwarvesf/hidden)，【免费，开源】菜单栏图标隐藏工具。

## 文件

### 解压

- [**MacZip**](https://ezip.awehunt.com/) 【免费】解压/压缩工具, 查看、编辑压缩包，无需解压！一直想找到Windows上7zip的mac替代品，终于满足了。
- [**the-unarchiver**](https://theunarchiver.com/) 【[App store](https://apps.apple.com/us/app/the-unarchiver/id425424353?mt=12), 免费】解压/压缩工具,`brew install --cask the-unarchiver`

### 文件比较/查看

- [**Meld**](http://meldmerge.org/) 【开源免费】文件比较， [Meld git下载](https://github.com/yousseb/meld/releases/)
- [**Qmenu**](https://apps.apple.com/cn/app/qmenu/id1567442612?l=en&mt=12) 【免费, App strore】访达扩展，拥有QSpace【付费, App strore】的部分功能。Support open in more Apps, such as Atom, MacVim, Emacs, CotEditor, Typora, Android Studio, HBuilderX, IDEA, AppCode, CLion, DataGrip, DataSpell, GoLand, PhpStorm, PyCharm, PyCharm CE, Rider, RubyMine, WebStorm.
  - 【新建文件】
  - 【**计算文件哈希值**】
  - 【Open in Item2】
  - 【Open in VScode】
  - 【Open in IntelliJ IDEA】
  - 【Open in PyCharm CE】
  - 【Open in Typora】
  - 【Copy path】
<!-- Qmenu升级1.2后包含了OpenInTerminal的功能，所以OpenInTerminal就不用了。
- [OpenInTerminal](https://github.com/Ji4n1ng/OpenInTerminal/blob/master/Resources/README-zh.md)  【开源免费】访达扩展，不仅可以用iTerm2打开，还可以配置用其他IDE打开。
  - Support Terminal: iTerm, Hyper, Alacritty and kitty.
  - Support TextEdit, Visual Studio Code, VSCode Insiders, Atom, Sublime Text, VSCodium, BBEdit, TextMate, CotEditor, MacVim, JetBrains(AppCode, CLion, GoLand, IntelliJ IDEA, PhpStorm, PyCharm, RubyMine, WebStorm), and Typora.
  - 因为部分功能与`Qmenu`重复，所以`OpenInTerminal`只设置了下面选项：
    - 【Open in IntelliJ IDEA】
    - 【Open in PyCharm】
    - 【Copy path】 -->

### 文件清理

- [x] [**CleanMyMac **](https://macpaw.com/cleanmymac) 【我的百度网盘、硬盘】系统清理。付费软件。
- [x] [**OmniDiskSweeper **](https://www.omnigroup.com/more) 系统文件清理。开源免费软件。

# 工具

## 云盘

- [百度网盘](pan.baidu.com)
- [OneDrive](https://www.microsoft.com/en-us/microsoft-365/onedrive/online-cloud-storage)
- [x] [**Kiwi for Gmail**](http://kiwiforgmail.com/)，Gmail 客户端, 我用的免费的lite版，App store 要切换到美国。
- [x] [**Microsoft NTFS for Mac by Paragon Software**](https://www.seagate.com/pl/pl/support/software/paragon/) - 支持 NTFS 格式硬盘，因为原来买了希捷的移动硬盘，送的软件，一般、够用。

- [x] [**RDM**](https://github.com/avibrazil/RDM)，【免费，开源】分辨率切换，允许设置未支持的分辨率，比如我会在录屏时设置 720p(hd) 的分辨率。在使用多个外接显示屏的时候，也可以调整外接显示屏的分辨率，很方便。

## 笔记/阅读

- [x] [**Onenote**](https://www.onenote.com/signin?wdorigin=ondc)，笔记工具，从 [Evernote印象笔记](https://evernote.com/intl/zh-cn) （原来是会员，现在只是免费版） 切到 Onenote，准备换[**Ulysses**](https://ulysses.app/)。不过我现在markdown一般都用vscode+github来写了。
  - Onenoted 优点
    - 0 免费 + 实时同步到onedrive
    - 1 多级目录（note - stack section - section - page - subpage）
    - 2 笔记间可相互引用：可复制page link和section link
  - Onenoted 缺点
    - 对markdown支持不好（只有windows版本有插件可以支持markdown）
- [有道云笔记](https://note.youdao.com/)【免费，支持markdown】推荐。[APP store 可下载](https://apps.apple.com/cn/app/%E6%9C%89%E9%81%93%E4%BA%91%E7%AC%94%E8%AE%B0-%E7%AC%94%E8%AE%B0%E6%95%88%E7%8E%87%E5%8A%9E%E5%85%AC/id1600668116?l=en&mt=12)
  - 支持markdown
  - 免费版（非会员）2-3G空间
- [Typora](https://typora.io/) 专门写markdown的编辑器。
- [x] [**Reeder**](http://reederapp.com/mac/)，RSS 阅读软件
 <!-- 我的主要信息来源，没有提供 rss 源的我会先在 [**rsshub.app**](https://docs.rsshub.app/) 上找，再没有就自己写一个 serverless 服务部署在 [now](https://zeit.co/) 上，[now使用方法](http://object.ws/2017/09/10/nowsh-note/) -->

- [uPic](https://github.com/gee1k/uPic) 【免费，开源】Mac图床客户端。我当然用的免费开源版。需要在 系统偏好设置 - 扩展 - 访达扩展 中添加扩展，否则点击会没有反应，[参照](https://blog.svend.cc/upic/#%E4%B8%8B%E8%BD%BD%E5%AE%89%E8%A3%85)
  - 支持图床： smms、 又拍云 USS、七牛云 KODO、 阿里云 OSS、 腾讯云 COS、微博、Github、 Gitee、 Amazon S3、自定义上传接口等
  - [中文使用说明](https://blog.svend.cc/upic/)
  - [App store 也可下载收费版￥30](https://apps.apple.com/cn/app/upic-a-powerful-hosting-tool/id1549159979?l=en&mt=12) 只有 AppStore 是最新版本。 其他安装留在`v0.21.1'。可以拉取代码自行编译打包。

## 作图

<!-- - [ ] [**Ulysses**](https://ulysses.app/)，笔记工具，从 [Bear](http://www.bear-writer.com/) 和 [Notion](https://www.notion.so/?r=159be429981b4725ad6f36c4f599bd98) 切到 Ulysses -->
- Photoshop 【收费】，如果轻量级使用可以用网页在线工具[photopea](https://www.photopea.com/)代替。

- [x] [**OmniGraffle**](https://www.omnigroup.com/omnigraffle) 画图工具.
- [x] [**Xmind**](https://www.xmind.net/) 脑图工具。
<!-- - [ ] + iPad 上的 [**Whiteboard**](https://apps.apple.com/us/app/microsoft-whiteboard/id1352499399)，分别用于画架构图和和脑图 -->

## 截图

- [Shottr](https://shottr.cc/) 【免费，MAC M1】Screenshot tool fordesigners，front-end engineers，mobile developers those who care about pixels.
  - 可以量尺寸pixels
  - Text recognition (OCR) 图片识别文字
  - Scrolling Screenshots on Mac 长截图
  - Color picker 取色器

## 修图

[修图软件](./%E5%9B%BE%E7%89%87%E5%A4%84%E7%90%86%E8%BD%AF%E4%BB%B6%E6%8E%A8%E8%8D%90.html)


## 视频

## 视频播放

- [x] [**Gif Brewery 3**](https://apps.apple.com/cn/app/gif-brewery-3-video-to-gif/id1081413713?l=en&mt=12) ，GIF 录屏工具, 可以直接录屏并转换成gif动图。免费，App store 下载。
- 各类视频软件
- [x] [**IINA**](https://github.com/iina/iina)，[IINA](https://iina.io/)视频播放。原来用的[VLC media player](https://www.videolan.org/vlc/index.zh.html)，后来[改用IINA](https://www.zhihu.com/question/19552878/answer/139035466)。【开源免费】多媒体播放器，支持多倍速播放。 `brew install --cask iina`

### 视频编辑

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

## 虚拟机

- [x] [**ParallelsDesktop**](https://www.parallels.com/) 【付费】Mac上跑Windows虚拟机，与Mac集成的非常好。
- [x] [**VirtualBox**](https://www.virtualbox.org/) 【免费】Oracle虚拟机。

## 翻译

- [DeepL](https://www.deepl.com/translator)  网页版，app版，浏览器插件 都有。Pro版本收费，普通版免费。

## 工作必备

- [x] [GlobalProtect](https://vpn.microstrategy.com/global-protect/getsoftwarepage.esp) 【网址下载】 工作 VPN 软件
- [x] [Microsoft Remote Desktop](https://apps.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12) [APP Store] 美版账号，连接远程虚拟机。
- [x] [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)【免费】连接远程虚拟机。
- [x] [Zoom](https://zoom.us/) 在线会议。
- [x] [Slack](https://slack.com) 办公聊天。
- [x] [Grammarly](https://www.grammarly.com/) Chrome extension + Mac application 英文写作必备，可以提示语法错误并自动改正。
- [Microsoft office 365](https://apps.apple.com/cn/app-bundle/microsoft-365/id1450038993?l=en&mt=12) 微软全家桶。

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

- <https://zhuanlan.zhihu.com/p/55866195>

## 壁纸软件

- [Irvue](https://apps.apple.com/us/app/irvue/id1039633667?mt=12)： 【Apple store 美版账户， 免费】自动换壁纸，就不用再为切换壁纸这件事情消耗过多不必要的时间。它自动获取 Unsplash 上的高质量无版权图片作为壁纸。在其菜单栏菜单中的 Update interval（更新时间）中可以设置更新间隔，从每半小时到每月都可以设置，也可以选择手动更新。
- [Unsplash](https://link.zhihu.com/?target=https%3A//unsplash.com/) ：【Apple store 美版账户， 免费】作为质量最高的免费无版权图片资源网站之一，Unsplash 一直被众多第三方壁纸应用选为图片来源，而这个高质量的照片网站终于有官方的 [Mac 客户端](https://apps.apple.com/us/app/unsplash-wallpapers/id1284863847?mt=12)了。

参考文章：

- [少数派文章：mac桌面壁纸软件](https://www.zhihu.com/question/40021839/answer/257790965)
- [mac有哪些好用的桌面壁纸软件？](https://www.zhihu.com/question/40021839)
