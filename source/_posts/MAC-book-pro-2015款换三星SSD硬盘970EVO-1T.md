---
title: MAC book pro 2015款换三星SSD硬盘970EVO 1T
catalog: true
date: 2021-05-31 20:49:58
subtitle:
header-img:
tags:
- MAC
categories:
- TECH
- Tools
---


升级MacBook Pro（15英寸，带有Retina显示屏，2015年）中的SSD硬盘。原SSD硬盘容量只有256GB, 相当不够用.
虽然电脑是15款的，但还很好用，不如只换个SSD就行了。既然都换了，不如直接上1T的。

# 1 准备

## 1.1 硬件准备

- P5 螺丝刀 + T6 螺丝刀 + 碳棒（或者不导电的其他工具，用于在2.2步骤里拆除电池连接器）
- SSD硬盘：三星SSD硬盘970EVO 1T  ￥1296
- M.2 NGFF转Macbook SSD转接卡：￥18
  虽然MacBook专用的SSD接口比较特殊，但是它仅仅只是接口形态有别于常规M.2，金手指定义和缺口位置不一样，转接卡甚至都不需要芯片，非常简单成本也很低，同时得益于它长度比一般常规的2280规格的M.2 SSD还更长一点，加个转接卡在前面装回去也完全可行。
![M.2 NGFF转Macbook SSD转接卡](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/0%E8%BD%AC%E6%8E%A5%E5%8D%A1.jpeg)

## 1.2 软件准备

- 系统升级到 macOS Hight Serria (10.13)及以上：在 macOS 10.13 正式发布之后，支持原生 NVME 协议。
- Time Machine 备份系统，可以实现整个系统完整迁移。
- [制作U盘系统盘，安装全新的MAC OS系统](../制作MAC-OS-系统安装U盘.md)。
  

# 2 硬件-换SSD

## 2.1拆底部盖板

取出固定Macbook Pro底壳的五角梅花螺丝，每颗螺丝按原位置摆放好，如下：
- 8颗3.1mm
- 两颗2.3mm

![M.2 NGFF转Macbook SSD转接卡](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/1.1.png)

从屏幕转轴一侧的边缘抬起，把底部盖板从MacBook Pro上抬起来。

![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/1.11.png)

底部盖板上有两个塑料夹子（红色），在上面的箱子里卡扣（橙色）可以装进塑料夹子。
在重新组装过程中，轻轻地将盖板的中心推到它的两个塑料夹上。

![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/1.12.png)

![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/1.13.png)

## 2.2 拆除电池连接器

* 把电池连接器上的标签撕掉， 不撕也可以。
* 在逻辑板上轻轻抬起电池连接器的每一端，将连接器从其插座上撬开。
* 将连接器弯曲，确保电池连接器不意外地与逻辑板接触。

![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/2.21.png)

![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/2.22.png)

## 2.3 拆除旧SSD（固态硬盘）

* 拧开将 SSD 固定在主板上的一颗 2.9 mm T5 梅花螺丝。
* 把SSD抬起足够高来从扬声器上方拿出。不要把SSD抬得太高，否则你可能会损坏触点或者插槽。
* 把SSD从主板上的插槽中拉出。

![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/2.31.png)

![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/2.32.png)

## 2.4 换上新的SSD

- 把NVMe M.2 固态硬盘插在转接卡上
- 再安装到MacBook主板的SSD接口上。注意一定要卡紧咯。

![M.2 NGFF转Macbook SSD转接卡](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/0%E8%BD%AC%E6%8E%A5%E5%8D%A1.jpeg)

![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/2.4.png)

- 安装好电池连接器，安装底部盖板。

# 3 软件-安装系统

1. 电脑插上制作好之后的macOS Big Sur 系统启动U盘
2. 点击电源键，启动Mac
3. 一直按住`option`键，直到出现“安装 Big Sur”再松开，然后点击“安装 Big Sur”开始安装macOS Big Sur系统。

> 不要”command + R“, 否则后续”磁盘工具“内找不到新装的SSD硬盘。

![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/3.3.png)

4. 出现白色apple 图标，读进度条(这一步可能出现，有些电脑不会出现)
5. 选择语言 (这一步可能出现，有些电脑不会出现)
![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/3.5.png)

6. 出现“macOS 实用工具“ 界面, 选择”磁盘工具“
   ![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/3.6.png)
7. 格式化（抹掉）新装的SSD硬盘

选择显示全部（这一步很重要！很重要！很重要！否则接下来你抹掉磁盘时有可能找不到 GUID 分区图的选项哦）
找到新硬盘，抹掉，名称自定义（这里我为磁盘取名 Macintosh HD），方案：
- 格式：`Mac OS扩展（日志式）`或者 `APFS`格式
- 方案：`GUID`
![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/3.7.png)
![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/3.71.png)
![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/3.72.png)

8. 退出”磁盘工具“， 回到“macOS 实用工具“ 界面, 选择”安装MacOS“ 或者 ”从Time machine 备份进行恢复“。
![](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/MAC-book-pro-2015%E6%AC%BE%E6%8D%A2%E4%B8%89%E6%98%9FSSD%E7%A1%AC%E7%9B%98970EVO-1T/3.8.png)

# 4 测试

系统安装完后，apple store （美国区）安装软件‎Blackmagic Disk Speed Test， 测试SSD速度。
测试一下速度，读28xxMB/s，写24xxMB/s。

# 参考文章

- [换个SSD再战3年，15款MacBook Pro升级1TB SSD，附13-17款升级指南](https://post.smzdm.com/p/a783vk9g/)