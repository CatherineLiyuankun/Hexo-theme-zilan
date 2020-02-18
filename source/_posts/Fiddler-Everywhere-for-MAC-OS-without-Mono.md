---
title: Fiddler Everywhere for MAC OS without Mono
catalog: true
date: 2020-02-05 20:10:02
subtitle: Fiddler可不用Mono直接在Mac上安装了！
header-img: https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Fiddler-Everywhere-for-MAC-OS-without-Mono/Fiddler.png
tags:
- Promise
categories:
- TECH
- Tools
- network tools
---

# Fiddler 版本历史
Fiddler著名的抓包工具，就不多说了。

在Mac上使用Fiddler也是血泪史，2016年出过Fiddler for OS X Beta 1, 必须通过Mono才可以在Mac上使用。但是在mac上使用是非常不稳定, 有非常多的问题.

现在终于有”Fiddler Everywhere“ 版本，可以直接在Mac上安装了！

因为之前他的mac版本非常不好用，后来就使用了其他的软件，像Charles，wireshark。下回可以写一篇这几个软件的对比文章。
2018年底就出来了Beta版本，我竟然一直不知道!  在网上随便一搜，知乎上、大家的博客写的也都是原来的2016年出的Fiddler for OS X的安装教程。所以索性就写一篇关于Fiddler的回顾，mark下。

时间 | 版本 | 系统 | 特性
---------|----------|---------|---------
 2007.1.5 | Fiddler v1.x | Windows | [Release History](https://www.telerik.com/support/whats-new/fiddler/release-history)
 2016年底  | Fiddler for OS X Beta 1 (Mono) | Mac OS |
 2018.11.8 | Fiddler Everywhere v0.1.0 | Windows, Mac and Linux | [Release History](https://www.telerik.com/support/whats-new/fiddler-everywhere/release-history)

 各个版本后来更新的小版本就不列出来了，可以点击Release History查看详细版本。


# 新版本：Fiddler Everywhere 介绍及下载

## Fiddler Everywhere 下载

现在终于有”Fiddler Everywhere“ 版本，可以直接在Mac上安装了！废话不多说，直接上[官方下载链接](https://www.telerik.com/download/fiddler-everywhere)。
然后跟安装其他mac软件一样直接安装就行了，简直喜大普奔。
[Release History 版本历史](https://www.telerik.com/support/whats-new/fiddler-everywhere/release-history)。

Fiddler使用方法网上一搜有很多，下回有空了再写。

## Fiddler Everywhere 介绍

官方介绍Fiddler Everywhere的blog: "[One Fiddler to Rule Them All](https://www.telerik.com/blogs/one-fiddler-to-rule-them-all)"

官方介绍Fiddler Everywhere的blog挑重点翻译过来：

> 您是否曾一再尝试将Fiddler设置为在Mac或Linux上运行，却又遇到另一个错误？
> 您是否对没有其他选择感到沮丧？
> 
> 多年来，将Fiddler移植到Mac和Linux一直是最受欢迎的功能请求之一。在2016年底，我们推出了使用 Mono的Beta版本，但是这种方法的问题和局限性似乎超过了获益。我们已经尝试过，我们已经了解到。
>
> 我们很高兴介绍下一个Fiddler – [Fiddler Everywhere](https://www.telerik.com/fiddler-everywhere)。 Fiddler Everywhere是从零开始构建的，可以在所有主要平台（Windows，Mac和Linux）上运行。这是您所询问的所有内容，以及更多：
> 
> 1. **跨平台支持**：基于Angular和.NET Core，它为Mac和Linux用户提供了与Windows用户相同的体验和生产力。
> 2. **流畅的用户界面**：自上次修改Fiddler的界面以来，UI的最佳做法已经有了长足发展。我们希望将最新的UI和UX改进引入Fiddler社区。 Kendo UI for Angular团队的同事们支持我们，这不是很好吗？
> 3. **完美的用户体验**：无论您是在构建API服务还是管理组织的流量，使用Fiddler都是小菜一碟。
> 4. 最重要的是，它是**免费**的。
> 
> 我们发布的第一个版本功能有限，但是我们将根据使用情况和您提供的反馈反复添加更多功能。
> 
> 但是旧的Fiddler – Windows版Fiddler呢？
> 我们将继续开发该版本，至少直到新的Fiddler具有与之相等的功能为止，并且可能在此之后很长时间。有两个主要原因：1有用 2每个人都喜欢它。

# 老版本： Fiddler for OS X Beta 1（Mono）
官方介绍Fiddler for OS X Beta 1 [Introducing Fiddler for OS X Beta 1](https://www.telerik.com/blogs/introducing-fiddler-for-os-x-beta-1)

## 安装方法
1. 如果您的Mac上未安装Mono框架，请[下载并安装](https://www.mono-project.com/download/stable/)。如果已经安装，请更新至最新版本。
2. 如果您刚刚安装了Mono，请打开Terminal并输入：
```bash
/Library/Frameworks/Mono.framework/Versions/<Mono版本> / bin / mozroots --import --sync
```
比如Mono版本5.10.1
```bash
/Library/Frameworks/Mono.framework/Versions/5.10.1/bin/mozroots --import —sync
```
> Mono框架具有自己的受信任的根证书存储。当前（在Mono版本4.2.4中），在OS X上安装Mono后，此存储仍然为空。Fiddler使用此存储中的证书来验证所访问网站的证书。因此，您需要使用一组普遍信任的根权限填充该存储，以避免Fiddler不断收到证书警告。 mozroots工具从Mozilla LXR导入受信任的权威。

3. 下载[fiddler-mac.zip](https://www.telerik.com/download/fiddler)解压缩到具有写权限的文件夹。建议Fiddler安装文件夹的完整路径不包含任何Windows路径非法字符。 （目前，某些Fiddler功能（例如各种文件导出或Fiddler脚本）可能无法处理此类路径。）
4. 打开终端并导航到第3步文件夹。
5. 在终端中输入`mono Fiddler.exe`

## 局限性，已知问题和解决方法
- **不稳定的用户界面**

> 用于OS X的Fiddler与Windows的Fiddler具有相同的外观，但是它建立在开源WinForms Mono实现的基础上。该实现的质量明显低于Microsoft WinForms的质量，这会导致不理想的用户体验。当我们意识到在开始使用macOS版本的Fiddler时，我们选择了这种方式，以便我们可以更快地实现对OS X的支持，而不必牺牲Windows的Fiddler路线图，而将我们的未来工作作为基础实际使用情况。

> 对于Beta 1版本，UI中最有问题的区域是调整窗口大小和调整窗口内部元素的大小。通常，这会导致所有受影响元素的重画效果差或拖延。不过，将鼠标悬停或单击受影响的区域通常会解决问题。

- 当Fiddler正在运行且“解密HTTPS流量”处于打开状态时，Safari无法访问某些受欢迎的网站（Facebook / Twitter / GitHub等）
> 当前，此效果仅限于Safari，并且只有在您打开Fiddler之前访问该网站时才会发生。清除受影响站点的浏览历史记录（只是历史记录不缓存或cookie）可以解决此问题。

> 我们的初步研究表明，使用TLS版本大于1.0的网站会出现此问题。缺少TLS 1.1和1.2的Mono实现，将Fiddler for macOS限制为仅使用TLS 1.0。不幸的是，Fiddler TLS 1.0连接是在对同一域建立TLS 1.2连接之后出现的，Safari无法接受该域。

- **不支持TLS 1.1和1.2**
这是Mono框架中TLS实现的当前状态引入的硬限制。因此，OS X的Fiddler目前无法使用这些协议。

- **SSL / TLS握手属性不可用**
Fiddler for OS X Beta目前无法显示这些内容。这项工作正在进行中。

- **自动更新**
Fiddler for OS X的初始版本只能手动更新。

- **使用寿命有限**
此版本的Fiddler for OS X可以使用60天，然后需要进行更新。


所以说知道老版本的缺点，你就知道为什么原来要弃用了。就知道为什么现在要喜大普奔又可以用回来了。