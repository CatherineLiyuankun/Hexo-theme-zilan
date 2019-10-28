---
title: HTTP CORS disable for chrome
catalog: true
date: 2019-10-21 15:51:01
subtitle: "chrome"
tags:
- CORS
categories:
- TECH
- Network
- Servlet/HTTP
---

CORS的基本原理请看上一篇：
[CORS的基本原理](../../../../2019/10/21/HTTP CORS disable)

简单关闭Chrome的CORS方法:
# MacOS
命令行里, 会另外打开一个Chrome窗口：
``` bash
➜   ✗ open -n -a "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --args --user-data-dir="/tmp/chrome_dev_test" --disable-web-security
```
> --user-data-dir 参数需要 Chrome 版本 49+ on OSX

如果想访问本地文件（开发目的来使用 AJAX 或 JSON），可以使用flag：
```
-–allow-file-access-from-files
```

# Windows
进入command prompt，进入到Chrome.exe文件夹，执行命令：
```
chrome.exe --disable-web-security
```
这个命令会禁掉CORS，而且可以访问本地文件。

# Reference Links:

[Disable same origin policy in Chrome](https://stackoverflow.com/questions/3102819/disable-same-origin-policy-in-chrome)