---
title: Vscode 配置和插件
catalog: true
date: 2020-05-26 22:20:04
subtitle:
header-img:
tags:
categories:
- TECH
- Tools
- IDE
---

# 插件

## [setting sync在线同步Vscode设置](http://shanalikhan.github.io/2015/12/15/Visual-Studio-Code-Sync-Settings.html)

[使用方法](http://www.chengpengfei.com/2018/08/27/)

如果是第一次使用，点击“Login with github”直接用github账号登陆，可以直接自动生成token，不需要自己手动生成。

即使你更换了新电脑B，只要你记得第三个步骤里保存的 token，同步也是非常方便的。
不记得的话 老电脑A cmd + shift + P –> sync 高级选项 Advanced Options –> Open setting 里面有Access Token 和 Gist ID。
你可以通过 新电脑B cmd + shift + P –> sync 高级选项 Advanced Options –> 编辑本地扩展设置 syncLocalSettings ，将你的 token 粘贴在配置文件里，然后再执行同步/下载的配置即可。
cmd + shift + P –> sync 高级选项 Advanced Options –> Open setting 里勾选Auto Download， Auto Upload， Remove Extensions 
Sync Extensions。

# 设置

## 代码高亮颜色设置

1. File-》Preferences-》settings

2. 在search settings中输入workbench.colorCustomizations

```json
  "workbench.colorCustomizations": {
    "editor.selectionBackground": "#135564", // 选中代码后，当前选中部分显示的颜色
    "editor.selectionHighlightBackground": "#f9e44ae0", // 选中代码后，相同代码显示的颜色
    "editor.lineHighlightBackground": "#f9c1c168", // 光标所在行的背景颜色
    "editor.lineHighlightBorder": "#f8bcbc80" // 光标所在行的背景边框颜色
  }
```

# Links

[VSCode前端必备插件，有可能你装了却不知道如何使用？](https://juejin.im/post/5db66672f265da4d0e009aad#heading-31)
