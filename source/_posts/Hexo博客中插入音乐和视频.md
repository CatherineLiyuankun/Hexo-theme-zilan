---
title: Hexo博客中插入音乐和视频
catalog: true
date: 2020-04-21 22:13:46
subtitle:
header-img:
tags:
- Hexo
- Blog
categories:
- TECH
- Hexo
---

# 方法一：Markdown 直接插入HTML标签

Markdown作为轻量级的标记语言，兼容html语法，我们可以直接在Markdown格式的.md文件中使用 html 语法。

大多数的视频，点击“分享”，都可以得到嵌入视频的HTML代码（大多数都是使用）`<iframe>`标签或者flash`<embed>`标签播放，直接拷贝粘贴到 Markdown 文档中即可使用就行了。

虾米音乐：
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="750" height="110" loading="lazy" sandbox="allow-popups allow-scripts allow-same-origin" src="https://www.xiami.com/webapp/embed-player?autoPlay=1&id=1900020217"></iframe>


## `<iframe>`标签

这个例子是拷贝我上传在YouTube视频：

```html
<iframe width="560" height="315" 
    src="https://www.youtube.com/embed/Fco5F5EPwUo"
    allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
    frameborder="0" allowfullscreen>
</iframe>
```

![YouTube视频分享](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Hexo%E5%8D%9A%E5%AE%A2%E4%B8%AD%E6%8F%92%E5%85%A5%E9%9F%B3%E4%B9%90%E5%92%8C%E8%A7%86%E9%A2%91/youtube.gif)

### YouTube效果

<iframe width="560" height="315" src="https://www.youtube.com/embed/_9aM609I-m0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### bilibili

![bilibili](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Hexo%E5%8D%9A%E5%AE%A2%E4%B8%AD%E6%8F%92%E5%85%A5%E9%9F%B3%E4%B9%90%E5%92%8C%E8%A7%86%E9%A2%91/bilibili.png)

<iframe width="560" height="315" src="//player.bilibili.com/player.html?aid=98312470&bvid=BV1pE411F7BX&cid=167824910&page=1" frameborder="0" framespacing="0"  allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen> </iframe>

## flash插件 `<embed>`标签
网易云音乐：
![网易云音乐](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Hexo%E5%8D%9A%E5%AE%A2%E4%B8%AD%E6%8F%92%E5%85%A5%E9%9F%B3%E4%B9%90%E5%92%8C%E8%A7%86%E9%A2%91/neteaseMusic.png)

```html
<embed src="//music.163.com/style/swf/widget.swf?sid=1372350500&type=2&auto=1&width=320&height=66"
    width="340" height="86"  allowNetworking="all">
</embed>
```

网易云音乐效果：
<embed src="//music.163.com/style/swf/widget.swf?sid=1372350500&type=2&auto=1&width=320&height=66"
    width="340" height="86"  allowNetworking="all">
</embed>

## `<script>`标签

```html
<script type="text/javascript" src="http://www.xiami.com/widget/player-single?uid=32329501&sid=1776238762&mode=js">
</script>
```

## `<vedio>`标签

```html
<video style="max-width: 100%; display: block; margin-left: auto; margin-right: auto;" controls src="https://www.bilibili.com/video/BV1Ta4y1t7UX/">
</video>
```

----

# 方法二：Hexo视频/音乐插件

----

## 音乐播放aplayer

> hexo-tag-aplayer: https://github.com/grzhan/hexo-tag-aplayer

### 命令行安装

Hexo-theme-zilan文件夹下，执行：

```bash
npm install hexo-tag-aplayer --save
```

### [使用方法](https://github.com/MoePlayer/hexo-tag-aplayer/raw/master/docs/README-zh_cn.md)

```markdown
{% aplayer title author url [picture_url, narrow, autoplay, width:xxx, lrc:xxx] %}
```

#### 标签参数

* title : 曲目标题
* author: 曲目作者
* url: 音乐文件 URL 地址
* picture_url: (可选) 音乐对应的图片地址
* narrow: （可选）播放器袖珍风格
* autoplay: (可选) 自动播放，移动端浏览器暂时不支持此功能
* width:xxx: (可选) 播放器宽度 (默认: 100%)
* lrc:xxx: （可选）歌词文件 URL 地址

当开启 Hexo 的 文章资源文件夹 功能时，可以将图片、音乐文件、歌词文件放入与文章对应的资源文件夹中，然后直接引用：

### 例子

```markdown
{% aplayer "岚坤爷" "岚坤爷" "https://www.xiami.com/webapp/embed-player?autoPlay=1&id=1900020217" "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/base/chatHead.jpg" %}
```

{% aplayer "岚坤爷" "岚坤爷" "https://www.xiami.com/webapp/embed-player?autoPlay=1&id=1900020217" "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/base/chatHead.jpg" %}

## 视频播放dplayer

> hexo-tag-dplayer: https://github.com/NextMoe/hexo-tag-dplayer

### 命令行安装

```bash
npm install hexo-tag-dplayer --save
```

### 标签参数

```
{% dplayer key=value ... %}
```

参数：

```
dplayer options:
    'autoplay', 'loop', 'screenshot', 'hotkey', 'mutex', 'dmunlimited' : bool options, use "yes" "y" "true" "1" "on" or just without value to enable
    'preload', 'theme', 'lang', 'logo', 'url', 'pic', 'thumbnails', 'vidtype', 'suburl', 'subtype', 'subbottom', 'subcolor', 'subcolor', 'id', 'api', 'token', 'addition', 'dmuser' : string arguments
    'volume', 'maximum' : number arguments
container options:
    'width', 'height' : string, used in container element style
other:
    'code' : value of this key will be append to script tag
```

### 例子

```markdown
{% dplayer "url=https://player.bilibili.com/player.html?aid=98312470&bvid=BV1pE411F7BX&cid=167824910&page=1" "api=http://dplayer.daoapp.io" "pic=https://www.xiami.com/webapp/embed-player?autoPlay=1&id=1900020217" "id=9E2E3368B56CDBB4" "loop=yes" "theme=#FADFA3" "autoplay=false" "token=tokendemo" %}
```

{% dplayer "url=https://player.bilibili.com/player.html?aid=98312470&bvid=BV1pE411F7BX&cid=167824910&page=1" "api=http://dplayer.daoapp.io" "pic=https://www.xiami.com/webapp/embed-player?autoPlay=1&id=1900020217" "id=9E2E3368B56CDBB4" "loop=yes" "theme=#FADFA3" "autoplay=false" "token=tokendemo" %}

# 其他相关文章

[Git Pages + Jekyll/Hexo Build your own blog 构建个人博客-你想知道的都在这里了](../Git-Pages-Jekyll-Hexo-Build-your-own-blog.html)