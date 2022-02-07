---
title: Mac风扇不转or狂转不停？用smcFanControl手动控制风扇速度
catalog: true
date: 2020-04-16 18:49:12
subtitle:
header-img: 'https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Mac%E9%A3%8E%E6%89%87%E4%B8%8D%E8%BD%ACor%E7%8B%82%E8%BD%AC%E4%B8%8D%E5%81%9C%EF%BC%9F%E7%94%A8smcFanControl%E6%89%8B%E5%8A%A8%E6%8E%A7%E5%88%B6%E9%A3%8E%E6%89%87%E9%80%9F%E5%BA%A6/%E5%B0%81%E9%9D%A2.png'
tags:
- MAC
categories:
- TECH
- Tools
---

# 起因
气死我了，最近我Mac Pro不知道怎么了，整个电脑没用两天就热的卡的不行。
都濒临死机状态了，风扇也没怎么转。
我本来都以为我电脑风扇坏了，这可怎么办，波兰这儿还是疫情期间，没法修啊，嘤嘤嘤。
在网上搜了搜，就发现了smcfancontrol这个软件，可以自己控制电脑的风扇速度。
心想，那就试试吧，反正是**免费**软件。
一试，提高风扇转速，有用啊！我终于听到风扇的声音了！
喜大普奔！不是风扇坏了。
电脑凉爽多了！！！
这么好用，顺便安利给大家。
这个软件同样可以解决风扇狂转不止的问题。

# smcfancontrol V2.6 下载地址
* smcfancontrol V2.6 [下载地址1](http://www.macupdate.com/info.php/id/23049 ).

* smcfancontrol V2.6 [下载地址2](https://github.com/hholtmann/smcFanControl/releases/download/2.6.1%C3%9F1/smcFanControl_2_6_1.zip)

* smcfancontrol V2.6 下载地址3：链接:https://pan.baidu.com/s/1AKkGjJxMeuXNzuvIAHqs2w  密码:nmxq

# smcfancontrol 介绍
smcFanControl控制每台Intel Mac的风扇，使其运行温度更低。
smcFanControl允许用户设置内置风扇的最低速度。因此，您可以提高最低风扇速度，以使Mac运行温度更低。但是，为了不损坏计算机，smcFanControl不允许您将最低速度设置为低于Apple默认值的值。

## smcFanControl 的新功能
2.6版：注意：现在需要OS X 10.7或更高版本

新功能：
* 添加了法语本地化
* 更新了Sparkle Updater
* smcFanControl现在需要macOS 10.7或更高版本

已解决：
* Macbook 12"崩溃问题。
* 在macOS Sierra上的Dark模式下“看不见文本”。

免费：
基础功能都是免费的，我觉得够用了。良心软件啊！

会员版：
* 解锁个性化应用推荐
* 获得会员独享的折扣
* 轻松跟踪您的下载和购买历史记录
* 开始为最大的Mac社区做出贡献

YouTube英文版使用视频：
不想看英文的可以看我后面的图文介绍。

<iframe width="560" height="315" src="https://www.youtube.com/embed/Fco5F5EPwUo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## smcFanControl 安装

下载完后解压,复制smcFanControl.app到应用程序：
![安装](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Mac%E9%A3%8E%E6%89%87%E4%B8%8D%E8%BD%ACor%E7%8B%82%E8%BD%AC%E4%B8%8D%E5%81%9C%EF%BC%9F%E7%94%A8smcFanControl%E6%89%8B%E5%8A%A8%E6%8E%A7%E5%88%B6%E9%A3%8E%E6%89%87%E9%80%9F%E5%BA%A6/%E5%A4%8D%E5%88%B6%E5%88%B0%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F.gif)

双击smcFanControl.app打开，出现alert直接点击continue：
![alert](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Mac%E9%A3%8E%E6%89%87%E4%B8%8D%E8%BD%ACor%E7%8B%82%E8%BD%AC%E4%B8%8D%E5%81%9C%EF%BC%9F%E7%94%A8smcFanControl%E6%89%8B%E5%8A%A8%E6%8E%A7%E5%88%B6%E9%A3%8E%E6%89%87%E9%80%9F%E5%BA%A6/smcfancontrol-alert.jpg)

使用：
打开后，会在状态栏上显示 smcFanControl 目前设备温度和转速，也许刚打开时候 rpm 显示错误，重开一次 smcFanControl 即可，可先点「Preferences」进行设置。
![状态栏](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Mac%E9%A3%8E%E6%89%87%E4%B8%8D%E8%BD%ACor%E7%8B%82%E8%BD%AC%E4%B8%8D%E5%81%9C%EF%BC%9F%E7%94%A8smcFanControl%E6%89%8B%E5%8A%A8%E6%8E%A7%E5%88%B6%E9%A3%8E%E6%89%87%E9%80%9F%E5%BA%A6/%E7%8A%B6%E6%80%81%E6%A0%8F.png)

默认软件里面会有两组预设设定，分别为 Default 、 Higher RPM（高转速） 两个选项，如果想自定义转速，也可以通过右侧「+」新增。
如要自定义名称可自己输入，比如「低速」、「高速」、等，设定完后点击「Save」储存。
可以通过min.Speed 拉杆手动调整风扇转速，往左调整速度越慢，往右调整速度越快，相对越快风扇就会越大声，底下Menubar也可以选择数字颜色，至于下面选项则可参考底下翻译：

* Check for updates on startup：启动时检查更新
* Autostart smcFanControl after login：开机后自动开启smcFanControl
* Autoapply favorite when powersource changes：连接电源线自动切换风扇频率

![使用](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Mac%E9%A3%8E%E6%89%87%E4%B8%8D%E8%BD%ACor%E7%8B%82%E8%BD%AC%E4%B8%8D%E5%81%9C%EF%BC%9F%E7%94%A8smcFanControl%E6%89%8B%E5%8A%A8%E6%8E%A7%E5%88%B6%E9%A3%8E%E6%89%87%E9%80%9F%E5%BA%A6/Preferences.gif)

通常使用方式只要从 Active Setting 内选择你想使用的模式，过一会风扇就会调整。通常我是用来降温用，如发现 MacBook Pro 温度高过于50°就可以启动smcFanControl来增强风扇转速，提升散热效果。
![Active Setting](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Mac%E9%A3%8E%E6%89%87%E4%B8%8D%E8%BD%ACor%E7%8B%82%E8%BD%AC%E4%B8%8D%E5%81%9C%EF%BC%9F%E7%94%A8smcFanControl%E6%89%8B%E5%8A%A8%E6%8E%A7%E5%88%B6%E9%A3%8E%E6%89%87%E9%80%9F%E5%BA%A6/active%20setting.png)

