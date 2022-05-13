---
title: DevTool debug tips
catalog: true
date: 2022-05-13 16:00:48
subtitle:
header-img:
tags:
- devtool
categories:
- TECH
- FrontEnd
---

### Emulate a focused page in DevTools to debug overlay elements

当焦点丢失时，一些覆盖元素（如下拉菜单或弹出菜单）会自动隐藏/删除。 每当您切换到 DevTools 时，页面不再聚焦并且元素被隐藏。

> Some overlay elements like dropdowns or flyout menus automatically hide/remove themselves when the focus is lost. Whenever you switch to the DevTools the page is not focused anymore and the element gets hidden.

为了解决这个问题，我们可以使用Chrome DevTools的`Emulate a focused page`功能来模拟focus到page的状态，这样覆盖元素（如下拉菜单或弹出菜单）就不会被自动隐藏了。

- The Chrome DevTools have a feature to emulate page focus. Open the DevTools, press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS) and search for "Emulate a focused page".

- A checkbox in `Rendering` panel
![20220513Emulateafocusedpage](https://cdn.jsdelivr.net/gh/CatherineLiyuankun/PictureBed@master/blog/post/20220513Emulate%20a%20focused%20page.png)

#### 参考文章

- [Emulate a focused page in DevTools to debug overlay elements](https://tinytip.co/tips/devtools-focused-page/)
- [Emulate a focused Page option not available in Chrome Developer Tools](https://stackoverflow.com/questions/64456886/emulate-a-focused-page-option-not-available-in-chrome-developer-tools)
