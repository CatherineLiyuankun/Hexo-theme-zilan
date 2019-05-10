---
title: 从微信链接爬取音频
catalog: true
date: 2019-04-24 17:04:14
subtitle: mpvoice
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E4%BB%8E%E5%BE%AE%E4%BF%A1%E9%93%BE%E6%8E%A5-mpvoice-%E7%88%AC%E5%8F%96%E9%9F%B3%E9%A2%91/header-html5-audio.jpg"
tags:
- Weixin
- <mpvoice>
categories:
- TECH
- FrontEnd
---
# 故事是这样的
报名了某英语课程, 进群后老师会发微信课程链接, 链接里有音频视频等. 我就想做笔记把这个文字和音频视频内容保存下来.

# 看代码去
微信链接在浏览器打开, 视频的很好找 `<video origin_src="里面的就是视频的链接">` , 把链接直接粘贴到浏览器里就好了,右键save as 就可以保存下来了.
![视频](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E4%BB%8E%E5%BE%AE%E4%BF%A1%E9%93%BE%E6%8E%A5-mpvoice-%E7%88%AC%E5%8F%96%E9%9F%B3%E9%A2%91/%E8%A7%86%E9%A2%91.png)

有的音频的资源source也很好找, `<audio src="里面的就是视频的链接">`, 把链接直接粘贴到浏览器里就好了,右键save as 就可以保存下来了.
![音频1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E4%BB%8E%E5%BE%AE%E4%BF%A1%E9%93%BE%E6%8E%A5-mpvoice-%E7%88%AC%E5%8F%96%E9%9F%B3%E9%A2%91/%E9%9F%B3%E9%A2%911.png)

但是后来遇到了个看不出直接source的`<mpvoice>`, 应该是微信的自定义html标签. 随便在网上一搜, 就看到了跟我一样目的童鞋, 哈哈. 
![音频2](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E4%BB%8E%E5%BE%AE%E4%BF%A1%E9%93%BE%E6%8E%A5-mpvoice-%E7%88%AC%E5%8F%96%E9%9F%B3%E9%A2%91/%E9%9F%B3%E9%A2%912.png)

按照他的方法试了, 果然可以. Network中有获取media的请求 (开发者工具 --> Network ---> "media" tab). 而且`<mpvoice>`标签上voice_encode_fileid属性的值就是mediaid的值。同样的粘贴链接"https://res.wx.qq.com/voice/getvoice?mediaid=MzI1NDMxNTIxNF8xMDAwMDIxNjg="到浏览器里就好了,右键save as 就可以保存下来了.
![request](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/%E4%BB%8E%E5%BE%AE%E4%BF%A1%E9%93%BE%E6%8E%A5-mpvoice-%E7%88%AC%E5%8F%96%E9%9F%B3%E9%A2%91/request.png)

# Todo 写个脚本自动爬

# 参考文章
[一个简单的逻辑英语音频小爬虫](http://haijd.tech/golang/%E4%B8%80%E4%B8%AA%E7%AE%80%E5%8D%95%E7%9A%84%E9%80%BB%E8%BE%91%E8%8B%B1%E8%AF%AD%E9%9F%B3%E9%A2%91%E5%B0%8F%E7%88%AC%E8%99%AB/)
