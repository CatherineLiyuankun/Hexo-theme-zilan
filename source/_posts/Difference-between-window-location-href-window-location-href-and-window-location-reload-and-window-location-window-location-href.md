---
title: >-
  Difference between window.location.href=window.location.href and
  window.location.reload() and window.location=window.location.href
catalog: true
date: 2021-03-18 11:32:57
subtitle: 你真的会页面刷新吗？
header-img:
tags:
categories:
- TECH
- FrontEnd
- JavaScript
---

# Compare table 对比表格

> Re-POST：reloads the current page with POST data. 发送POST请求加载当前页面。

Refresh page | Re-POST | Static scan tool warning: Veracode | SonarQube | JSLint
---------|----------|---------|---------|---------
`window.location = window.location.href` | `No` | `Yes` "CWE ID 601 URL Redirection to Untrusted Site ('Open Redirect')" | `No` | `No`
`window.location.href = window.location.href` | `No` | `Yes` | `Yes` | `Yes` "Weird assignment"
`window.location.reload()` | Maybe, depends on browsers 也许，不同浏览器有不同行为 [Test Code](https://codepen.io/catherineliyuankun/pen/bGByZbe) | `No` | `No` | `No`

`window.location.reload()` reloads the current page **with POST data**, while `window.location.href=window.location.href` **discarding the POST data(perform a GET request)** 通过GET请求reload页面.


## window.location.href=window.location.href

## window.location=window.location.href

`window.location = window.location.href` works the same as `window.location.href = window.location.href` in all these browsers.
`window.location = window.location.href`和 `window.location.href = window.location.href` 的行为在各个浏览器上完全一致。

`window.location.href=window.location.href` will not reload the page if there's an anchor (#) in the URL - You must use window.location.reload() in this case.
如果页面URL中包含锚`#`, `window.location.href=window.location.href` 不会reload页面。

可以通过判断hash解决：

```JavaScript
if (!window.location.hash) {
    window.location.href = window.location.href;
} else {
    window.location.reload();
}

```

## window.location.reload()

JavaScript `window.location` object can be used

- to get current page address (URL)
- to redirect the browser to another page
- to reload the same page

`window`: in JavaScript represents an open window in a browser.

`location`: in JavaScript holds information about current URL.

The location object is like a fragment of the window object and is called up through the window.location property.

`location` object has three methods:

assign(): used to load a new document
reload(): used to reload current document 与点击”Refesh“ 按钮效果相同。
replace(): used to replace current document with a new one

### Re-POST

- Chrome 12 and Safari 5.0.5 on Mac do not re-POST with `.reload()`
- FF 2.0, 3.6, 4.0, 5.0 on Mac present the user with the "resend form dialog" with `.reload()`, `.reload(true)`, and `.reload(false)`
- IE6, IE8(standards), IE8(IE7 mode,standards) in XP; and IE9 and IE10-tech-preview in Win7 behave the same as FF on Mac
- [Test Code](https://codepen.io/catherineliyuankun/pen/bGByZbe)

### skipCache

`window.location.reload()` takes an additional argument `skipCache`.

`window.location.reload()`可以有额外的参数：`skipCache`.
- Using `window.location.reload(true)` the browser will skip the cache and reload the page from the server. `skipCache` 为`true`, 浏览器忽略cache， 从服务器重新加载页面。
- `window.location.reload(false)` will do the opposite, and load the page from cache if possible. `skipCache` 为`false`, 浏览器优先从cache重新加载页面，若没有cache则从服务器加载页面。
- default value for window.location.reload() is false. `skipCache` 默认值为(false)。

## window.location.assign(wd.location.href) : go to the URL
## window.location.replace(wd.location.href) : go to the URL and replace previous page in history

From w3schools: "The difference between assign() and replace(), is that replace() removes the URL of the current document from the document history, meaning that it is not possible to use the "back" button to navigate back to the original document."

The difference from the assign() method is that after using replace() the current page will not be saved in session History, meaning the user won't be able to use the back button to navigate to it.

# Summary 总结

- 如果不想要发送POST请求，使用`window.location = window.location.href`。注意！如果页面URL中包含锚`#`, `window.location.href=window.location.href` 不会reload页面，需要额外判断。
- 如果不介意使用POST请求，使用`window.location.reload()`， 这种用法在各个代码扫描工具中都不会有warning。

# Reference Links

- [Difference between window.location.href=window.location.href and window.location.reload()](https://stackoverflow.com/questions/2405117/difference-between-window-location-href-window-location-href-and-window-location)

- [window.location.href = window.location.href and JSLint](https://stackoverflow.com/questions/6751641/window-location-href-window-location-href-and-jslint)
- [MDN：Window.location](https://developer.mozilla.org/en-US/docs/Web/API/Window/location)
- [Location: reload()](https://developer.mozilla.org/en-US/docs/Web/API/Location/reload)
- [How to reload a page using JavaScript](https://stackoverflow.com/questions/3715047/how-to-reload-a-page-using-javascript)
- [What's the difference between window.location= and window.location.replace()?](https://stackoverflow.com/questions/1865837/whats-the-difference-between-window-location-and-window-location-replace)

