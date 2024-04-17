---
layout: 
title: MacOS Karabiner-Elements不生效解决方法
subtitle: MacOS 10.14.6 or 14.4
date: 2020-07-29 05:14:01
tags:
- MAC
categories:
- TECH
- Tools
---

每回MacOS一升级，总会遇到Karabiner-Elements不生效的问题，所以统一总结一下

## Karabiner-Elements

[**Karabiner Element**](https://pqrs.org/osx/karabiner/)，作用是键盘按键改键。

我通常用于[把右 Command 和 Capslock 键利用起来](http://lucifr.com/2013/02/16/caps-lock-to-hyper-key/)，避免快捷键冲突，[简单 note](https://hackmd.io/s/rk4u9i-pG)，详见[sorrycc的《我的快捷键技巧》](https://www.bilibili.com/video/av44127555)

- “`右 Command”改成F19`: 切换到Complex modifications --> Add rule --> "Change caps_lock to command+control+option+shift." --> 打开文件`~/.config/karabiner/karabiner.json` 把`caps_lock`替换成`right_command`
  ![`caps_lock`替换成`right_command`](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E5%A5%A5%E5%88%A9%E7%BB%99%E4%BD%A0%E7%9A%84iTerm2-%E5%BF%AB%E9%80%9F%E7%94%A8IDE%E6%89%93%E5%BC%80%E6%96%87%E4%BB%B6/Karabiner%20Element.png)
- 我试了后, 把“右 Command”改成F19,发现我右 Command+delete还是经常用的，所以接着在Karabiner Element 的“Simple modifications” 把 "right_option" 改成了 “left_command”。
- 另外参考[Mac 自定义应用程序快捷键](https://lhajh.github.io/mac/2017/12/05/.Mac-custom-application-shortcut-keys.html)配置了Mac app，比如Chrome和iterm3的一些快捷键。免费，开源。

## 通用解决方法

系统权限保证都设置正确
打开System Settings > Security & Privacy > Privacy

### Full Disk Access

- Karabiner-Elements
  - /Applications/Karabiner-Elements.app
- karabiner_grabber
  - 路径： /Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_grabber

### Input monitoring

- Karabiner-Eventviewer
  - /Applications/Karabiner-EventViewer.app
- karabiner_grabber
  - /Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_grabber
- karabiner_observer
  - /Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_observer

### Accessibility

- karabiner_grabber
  - /Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_grabber
- karabiner_observer
  - /Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_observer

### Allow driver

打开System Settings > Security & Privacy > Security
Allow driver:
<https://karabiner-elements.pqrs.org/docs/help/troubleshooting/allow-button-does-not-appear/>

### 重启

重启电脑
多次重启Karabiner-Elements
如果还不成功，就杀进程后重启Karabiner-Elements

```shell
sudo killall karabiner_grabber
sudo killall karabiner_observer
```

## MacOS 14.4.1 Karabiner-Elements不生效

额外把'karabiner_grabber' full disk access rights makes it work. However, I had to restart Karabiner twice afterwards and 重启电脑.

参考链接：<https://github.com/pqrs-org/Karabiner-Elements/issues/3620#issuecomment-1765946996>

## MacOS 10.14.6 Karabiner-Elements不生效

遇到了[macOS 10.14.6 Karabiner-Elements](https://www.v2ex.com/t/585453) 疑似无法正常使用的问题
参考[Does not work on MacOS Catalina #1867](https://github.com/pqrs-org/Karabiner-Elements/issues/1867)

For some reason the permission prompt is not showing up for me when I open `Karabiner-EventViewer`. And EventViewer says "EventViewer failed to observe keyboard devices". So I cannot find out a way to use saagarjha's method as stated above.

1. add `karabiner_grabber` and `karabiner_observer` to “Security & Privacy > Privacy > Accessibility” apps.
2. And after sudo killall-ing both processes, Karabiner-Elements is working for me again.

```shell
sudo killall karabiner_grabber
sudo killall karabiner_observer
```

In order to fix, I needed to add the following entries to the Security & Privacy > Privacy > Input Monitoring list:

/Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_grabber
/Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_observer

## 其他改键工具

Some other tools that should work for you are:

1. hidutil: macOS-native remapping tool. See [MX Keys not active in logi options+ via bluetooth #3082 (comment)](https://github.com/pqrs-org/Karabiner-Elements/issues/3082#issuecomment-1137009173).   Only work for simple modifications
2. skhd: <https://github.com/koekeishiya/skhd>.
3. Hammerspoon or BetterTouchTool.
