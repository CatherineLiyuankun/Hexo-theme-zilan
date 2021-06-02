---
title: 制作MAC OS 系统安装U盘
catalog: true
date: 2021-05-31 23:09:43
subtitle:
header-img:
tags:
- MAC
categories:
- TECH
- Tools
---

## 1 U盘

在创建macOS U盘启动之前，必须拥有一个U盘。

- U盘大小 >= 16G
- U盘确保 不含有重要数据，因为会初始化U盘.
  
插入u盘，将U盘在「磁盘工具」中初始化，其中`MyVolume`代表自己的U盘名称. 可以命名为其他名称，但要和步骤3中的命令一致。

* 格式：Mac OS扩展（日志式）
* 方案：GUID 分区图

![格式化](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E5%88%B6%E4%BD%9CMAC-OS-%E7%B3%BB%E7%BB%9F%E5%AE%89%E8%A3%85U%E7%9B%98/u%E7%9B%98%E6%A0%BC%E5%BC%8F%E5%8C%96.jpg)

## 2 下载macOS 系统

Apple Store 官方下载链接：
- 下载：[macOS Big Sur](https://apps.apple.com/cn/app/macos-big-sur/id1526878132?mt=12)、[macOS Catalina](https://apps.apple.com/cn/app/macos-catalina/id1466841314?mt=12)、[macOS Mojave](https://apps.apple.com/cn/app/macos-mojave/id1398502828?mt=12) 或 [macOS High Sierra](https://apps.apple.com/cn/app/macos-high-sierra/id1246284741?mt=12) 
这些内容会作为名为“安装 macOS [版本名称]”的 App 下载到您的`应用程序`文件夹。
如果安装器在下载后打开，请退出而不要继续安装。要获取正确的安装器，请从运行 [macOS Sierra 10.12.5 或更高版本](https://support.apple.com/zh-cn/HT201260)或者 El Capitan 10.11.6 的 Mac 上进行下载。如果您是企业管理员，请通过 Apple 下载，而不要通过本地托管的软件更新服务器进行下载。
- 下载：[OS X El Capitan](http://updates-http.cdn-apple.com/2019/cert/061-41424-20191024-218af9ec-cf50-4516-9011-228c78eda3d2/InstallMacOSX.dmg)
这个内容会作为名为“InstallMacOSX.dmg”的磁盘映像下载。在与 El Capitan 兼容的 Mac 上，打开下载的磁盘映像，并运行其中名为“InstallMacOSX.pkg”的安装器。这时会在您的“应用程序”文件夹中安装一个名为“安装 OS X El Capitan”的 App。您将通过这个 App（而不是通过磁盘映像或 .pkg 安装器）创建可引导安装器。

## 3 在“终端”中使用“createinstallmedia”命令

`MyVolume`代表自己的U盘名称, 要和步骤1中U盘名称一致.

例如安装Big Sur*：

```bash
sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

Catalina*：

```bash
sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

Mojave*：

```bash
sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

High Sierra*：

```bash
sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

El Capitan：

```bash
sudo /Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume --applicationpath /Applications/Install\ OS\ X\ El\ Capitan.app
```

> 如果您的 Mac 运行的是 macOS Sierra 或更低版本，请使用 --applicationpath 参数和安装器路径，具体方法与在适用于 El Capitan 的命令中完成这个操作的方法类似。

键入命令后：

1. 按下 Return 键以输入这个命令。
2. 出现提示时，请键入您的管理员密码，然后再次按下 Return 键。在您键入密码时，“终端”不会显示任何字符。
3. 出现提示时，请键入 `Y` 以确认您要抹掉宗卷，然后按下 Return 键。在抹掉宗卷的过程中，“终端”会显示进度。
4. 宗卷被抹掉后，您可能会看到一条提醒，提示“终端”要访问可移除宗卷上的文件。点按“好”以允许继续拷贝。
5. 当“终端”显示操作已完成时，相应宗卷将拥有与您下载的安装器相同的名称，例如“安装 macOS Big Sur”。您现在可以退出“终端”并弹出宗卷。

![ 在“终端”中使用“createinstallmedia”命令](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E5%88%B6%E4%BD%9CMAC-OS-%E7%B3%BB%E7%BB%9F%E5%AE%89%E8%A3%85U%E7%9B%98/macos-big-sur-terminal-create-bootable-installer.jpg)

# 参考链接

[如何创建可引导的 macOS 安装器](https://support.apple.com/zh-cn/HT201372)