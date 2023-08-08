---
title: HTTP CORS disable for browser
catalog: true
date: 2019-10-21 15:51:01
subtitle: "Blocked a Frame with Origin 'xxx' From Accessing a Cross-Origin Frame Error"
tags:
- CORS
categories:
- TECH
- Network
- Servlet/HTTP
---

CORS的基本原理请看上一篇：
<!-- [CORS的基本原理](../../../../2019/10/21/HTTP CORS disable) -->
[CORS的基本原理](../HTTP-CORS.html)
[iframe内外页面通信](../iframe-%E5%86%85%E5%A4%96%E9%A1%B5%E9%9D%A2%E9%80%9A%E4%BF%A1.html)

用本地文件测试frame的时候，在执行`curWindow.navigator.userAgent`的时候会报错：
`Uncaught DOMException: Blocked a frame with origin "null" from accessing a cross-origin frame.`

原因是浏览器默认开启了CORS的安全保护，不允许iframe跨域获取一些值。

关闭同源策略 (CORS) 只会影响您的浏览器。此外，在浏览器中禁用同源安全设置会允许任何网站访问跨源资源，这是非常危险的，只能用于开发目的。现在，只有 `window.postMessage()` 才是`frame/iframe` 之间交互的最佳方式。

## 解决方案1 关闭浏览器CORS limit [临时解决]

Run a browser with `cross-domain web security/same-origin` policy disabled

```bash
# Mac Chrome
open /Applications/Google\ Chrome.app --args --user-data-dir="/const/tmp/Chrome dev session" --disable-web-security
# Mac Chrome Canary
#open /Applications/Google\ Chrome\ Canary.app --args --user-data-dir="/const/tmp/Chrome dev session" --disable-web-security

# For Linux run:
$ google-chrome --disable-web-security

# For Windows go into the command prompt and go into the folder where Chrome.exe is and type
chrome.exe --disable-web-security
```

### MacOS

命令行里, 加参数`--disable-web-security`打开chrome浏览器，会另外打开一个Chrome窗口：

``` bash
# Mac Chrome
open /Applications/Google\ Chrome.app --args --user-data-dir="/const/tmp/Chrome dev session" --disable-web-security

# --user-data-dir 
open -n -a "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --args --user-data-dir="/tmp/chrome_dev_test" --disable-web-security

# Mac Chrome Canary
# open /Applications/Google\ Chrome\ Canary.app --args --user-data-dir="/const/tmp/Chrome dev session" --disable-web-security
```

> --user-data-dir 参数需要 Chrome 版本 49+ on OSX

如果想访问本地文件（开发目的来使用 AJAX 或 JSON），可以使用flag：

```bash
-–allow-file-access-from-files
```

### Windows

进入command prompt，进入到Chrome.exe文件夹，执行命令：

```bash
# For Windows go into the command prompt and go into the folder where Chrome.exe is and type
chrome.exe --disable-web-security
```

这个命令会禁掉CORS，而且可以访问本地文件。

### Linux

```bash
# For Linux run:
$ google-chrome --disable-web-security
```

## 解决方案2 Extensions “xampp” or “Live Server” [临时解决]

You could solve it by installing xampp and moving all files to htdocs or using an extension like “Xampp”.

## 解决方案3 try-catch [跨域时无法获取想要的值，只是不抛错]

```javascript
// iframe 内的javascript
    try {
        const parent = window.parent && window.parent.navigator;
    } catch (error) {
        console.warn(`Error - ${error}`);
    }
```

## 解决方案4 `window.postMessage()` [终极解决]

同源策略可防止脚本访问不同源的网站内容，您可以使用 `window.postMessage()` 安全地在 Window 对象之间实现跨源通信。

```javascript
postMessage(message,targetOrigin)
postMessage(message,targetOrigin, [transfer])
```

## Reference Links

- [Disable same origin policy in Chrome](https://stackoverflow.com/questions/3102819/disable-same-origin-policy-in-chrome)
- [Resolving the Blocked a Frame with Origin "null" From Accessing a Cross-Origin Frame Error](https://hackernoon.com/resolving-the-blocked-a-frame-with-origin-null-from-accessing-a-cross-origin-frame-error)
