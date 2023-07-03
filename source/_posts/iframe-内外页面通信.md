---
title: iframe 内外页面通信
catalog: true
date: 2023-07-03 19:48:07
subtitle:
header-img:
categories:
- TECH
- FrontEnd
---

## Disable same origin policy in Chrome

用本地文件测试frame的时候，在执行`curWindow.navigator.userAgent`的时候会报错：
`Uncaught DOMException: Blocked a frame with origin "null" from accessing a cross-origin frame.`

原因是浏览器默认开启了CORS的安全保护，不允许iframe跨域获取一些值。

解决方案：参考 [Disable same origin policy in Chrome](https://stackoverflow.com/questions/3102819/disable-same-origin-policy-in-chrome)， 命令行加参数`--disable-web-security`打开chrome浏览器

```bash
# Mac Chrome
open /Applications/Google\ Chrome.app --args --user-data-dir="/var/tmp/Chrome dev session" --disable-web-security
# Mac Chrome Canary
#open /Applications/Google\ Chrome\ Canary.app --args --user-data-dir="/var/tmp/Chrome dev session" --disable-web-security

# For Linux run:
$ google-chrome --disable-web-security

# For Windows go into the command prompt and go into the folder where Chrome.exe is and type
chrome.exe --disable-web-security
```

## 参考文章

- [JS对Iframe内外页面进行操作](https://juejin.cn/post/7017740414060855310)
- [Web前端之iframe详解](https://zhuanlan.zhihu.com/p/168764040)
- [Iframe父子窗口通信](https://juejin.cn/post/6961791208876146718)
- [MDN Window.parent](https://developer.mozilla.org/en-US/docs/Web/API/Window/parent)
- [Disable same origin policy in Chrome](https://stackoverflow.com/questions/3102819/disable-same-origin-policy-in-chrome)
- [不同源iframe跨域问题（window.postMessage）](https://blog.csdn.net/weixin_43959024/article/details/118152348)
