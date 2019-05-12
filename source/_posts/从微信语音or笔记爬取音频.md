---
title: 从微信语音or笔记爬取音频
catalog: true
date: 2019-04-25 10:42:46
subtitle: 如何导出微信【收藏】中的语音文件？
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E4%BB%8E%E5%BE%AE%E4%BF%A1%E9%93%BE%E6%8E%A5-mpvoice-%E7%88%AC%E5%8F%96%E9%9F%B3%E9%A2%91/header-html5-audio.jpg"
tags:
- Weixin
categories:
- TECH
- FrontEnd
---

# 方法
[Leon 的回答](https://www.zhihu.com/question/30112442/answer/561089000)比较符合我的需求, 转化下就是:
```
If (MacOS)
    If (语音 in 电脑微信窗口记录)
        在聊天窗口找个图片;
        右键-->打开文件夹;
        里面看到的silk文件就是聊天的语音;

    If (语音 not in 电脑微信窗口记录)
        收藏(语音);
        播放(语音);
        去到("/Users/{用户名}/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/");
        搜索(Favorites目录);
        然后data下面就有silk文件 
        使用[kn007/silk-v3-decoder](https://github.com/kn007/silk-v3-decoder)
            > brew install lame
            > brew install ffmpeg  --enable-libmp3lame

        将silk文件转为wav
            > silk-v3-decoder/converter.sh ab.silk wav

    If (语音 in 电脑微信窗口记录的链接内)
        open(链接);
        播放(语音);
        去到("/Users/{用户名}/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/");
        搜索(⁨OpenData⁩);
        下面的某个文件里的音频.wav文件
        例如:Macintosh HD⁩ ▸ ⁨Users⁩ ▸ ⁨muzilan⁩ ▸ ⁨Library⁩ ▸ ⁨Containers⁩ ▸ ⁨com.tencent.xinWeChat⁩ ▸ ⁨Data⁩ ▸ ⁨Library⁩ ▸ ⁨Application Support⁩ ▸ ⁨com.tencent.xinWeChat⁩ ▸ ⁨2.0b4.0.9⁩ ▸ ⁨f68564a536bd7f4613c075bf2be66c8e⁩ ▸ ⁨Message⁩ ▸ ⁨MessageTemp⁩ ▸ ⁨9e20f478899dc29eb19741386f9343c8⁩ ▸ ⁨OpenData⁩ ▸ ⁨177⁩▸a8b51cec5109b6774a1efcac305692c4.wav
        直接拷贝;

        搜索(⁨Audio);
        下面的某个文件里的音频.silk文件
        例如:‎⁨ Macintosh HD⁩ ▸ ⁨Users⁩ ▸ ⁨muzilan⁩ ▸ ⁨Library⁩ ▸ ⁨Containers⁩ ▸ ⁨com.tencent.xinWeChat⁩ ▸ ⁨Data⁩ ▸ ⁨Library⁩ ▸ ⁨Application Support⁩ ▸ ⁨com.tencent.xinWeChat⁩ ▸ ⁨2.0b4.0.9⁩ ▸ ⁨f68564a536bd7f4613c075bf2be66c8e⁩ ▸ ⁨Message⁩ ▸ ⁨MessageTemp⁩ ▸ ⁨fce9f67a422f2c52cee716585240bf41⁩ ▸ ⁨Audio ▸ 111.aud.silk

        使用[kn007/silk-v3-decoder](https://github.com/kn007/silk-v3-decoder)
            > brew install lame
            > brew install ffmpeg  --enable-libmp3lame

        将silk文件转为wav
            > silk-v3-decoder/converter.sh ab.silk wav

        Or 按修改时间排序，最近被改的文件夹
        ‎⁨Macintosh HD⁩ ▸ ⁨Users⁩ ▸ ⁨muzilan⁩ ▸ ⁨Library⁩ ▸ ⁨Containers⁩ ▸ ⁨com.tencent.xinWeChat⁩ ▸ ⁨Data⁩ ▸ ⁨Library⁩ ▸ ⁨Application Support⁩ ▸ ⁨com.tencent.xinWeChat⁩ ▸ ⁨2.0b4.0.9⁩ ▸ ⁨f68564a536bd7f4613c075bf2be66c8e⁩ ▸ ⁨Message⁩ ▸ ⁨MessageTemp

```

# 参考链接
[知乎: 如何导出微信【收藏】中的语音文件？](https://www.zhihu.com/question/30112442)
