---
title: 'How to modify UserAgent - JS, IOS and Android'
catalog: true
date: 2023-07-03 17:41:45
subtitle:
header-img:
tags:
- Learning Notes
categories:
- TECH
- FrontEnd
---

# [UserAgent](https://developer.mozilla.org/zh-CN/docs/Glossary/User_agent)

## [`User-agent` Header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent)

### UserAgent Headers Chrome bug

> <https://developer.mozilla.org/en-US/docs/Glossary/Forbidden_header_name>
> "Note: The User-Agent header is no longer forbidden, as per spec — see forbidden header name list (this was implemented in Firefox 43) — it can now be set in a Fetch Headers object, or with the setRequestHeader() method of XMLHttpRequest. However, Chrome will silently drop the header from Fetch requests (see [Chromium bug 571722](https://crbug.com/571722))."

User-Agent header 不再被禁止更改，现在可以设置在 Fetch 的 Headers 对象中，或者通过 XMLHttpRequest 的 setRequestHeader() 方法设置。但是，Chrome 会不做提示地从 Fetch 请求中丢弃这个Header（请参阅 [Chromium bug 571722](https://crbug.com/571722)）
看了下这个bug 从 2015年就有了, 而且仍然是open状态，2023.7月亲自试了下，直接在fetch request里面设置`"User-agent": "Custom User Agent"`，发现确实chrome仍然有这个bug, Firefox 和Safari 都可以成功修改User-agent Header。

测试版本：

- Google Chrome Version 114.0.5735.198 (Official Build) (arm64)
- Firefox 113.0.2
- Safari Version 16.5 (18615.2.9.11.4)

```javascript
fetch("https://httpbin.org/user-agent", (credentials: "include", method: "GET', headers: /
"User-agent": "Custom User Agent"
Promise ([PromiseStatus]]: "pending", ((PromiseValue]]: undefined}
```

![Chromium bug 571722](https://bugs.chromium.org/p/chromium/issues/attachment?aid=85876&signed_aid=vqq4JDSv_sqKpBUcF8wJ1A==&inline=1)

## [UserAgent string](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/userAgent)

`window.navigator`返回一个`Navigator`对象的引用, 用于请求运行当前代码的应用程序的相关信息.

`Navigator`对象包含了一些关于浏览器的信息, 具体可以查阅[Navigator MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator)

```javascript
// 用户代理的字符串可以被 JavaScript 在客户端中使用 navigator.userAgent 获取
const userAgent = window.navigator.userAgent;
// 例如： Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.64 Mobile Safari/537.36
```

## JavaScript修改UserAgent string

[navigator.userAgent属性是只读属性，不建议修改](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/userAgent)。

但是仍然可以通过override navigator的get方法来修改, 参考代码[Override user agent on all browsers](https://gist.github.com/thorsten/148812e9cc4fb6a19215ce22afd4e5a8)。
需要注意的是这种修改方法：

- 不会修改request里面的`User-agent` Header
- 只是修改了navigator.userAgent （navigator的get方法）得到的userAgent string

```javascript
    function setUserAgent(window, customUserAgent) {
        const newUserAgent = `${navigator.userAgent} ${customUserAgent}`;
        // Works on Firefox, Chrome, Opera and IE9+
        if (navigator.__defineGetter__) {
            navigator.__defineGetter__('userAgent', function () {
                return newUserAgent;
            });
        } else if (Object.defineProperty) {
            Object.defineProperty(navigator, 'userAgent', {
                get: function () {
                    return newUserAgent;
                },
            });
        }
        // Works on Safari
        if (window.navigator.userAgent.indexOf(customUserAgent) < 0) {
            const userAgentProp = {
                get: function () {
                    return newUserAgent;
                },
            };
            try {
                Object.defineProperty(window.navigator, 'userAgent', userAgentProp);
            } catch (e) {
                window.navigator = Object.create(navigator, {
                    userAgent: userAgentProp,
                });
            }
        }
    }

    setUserAgent(window, 'CustomUserAgent/1.0'); // 在原来的userAgent后面append 'CustomUserAgent/1.0'
    // 例如： Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.64 CustomUserAgent/1.0
```

改进版本，抽取一些函数：

```javascript

function getNewUserAgent(userAgent, customUserAgent) {
    return userAgent.indexOf(customUserAgent) < 0 ? `${userAgent} ${customUserAgent}` : userAgent;
}

function getNewUserAgentProp(userAgent, customUserAgent) {
    return {
        get: function () {
            return getNewUserAgent(userAgent, customUserAgent);
        },
    };
}

function setUserAgent2(window, customUserAgent) {
    const userAgent = navigator.userAgent;
    const winUserAgent = window.navigator.userAgent;
    // Works on Firefox, Chrome, Opera and IE9+
    if (navigator.__defineGetter__) {
        navigator.__defineGetter__('userAgent', function () {
            return getNewUserAgent(userAgent, customUserAgent);
        });
    } else if (Object.defineProperty) {
        Object.defineProperty(navigator, 'userAgent', getNewUserAgentProp(userAgent, customUserAgent));
    }
    // Works on Safari
    if (winUserAgent.indexOf(customUserAgent) < 0) {
        try {
            Object.defineProperty(
                window.navigator,
                'userAgent',
                getNewUserAgentProp(winUserAgent, customUserAgent)
            );
        } catch (e) {
            window.navigator = Object.create(navigator, {
                userAgent: getNewUserAgentProp(navigator.userAgent, customUserAgent),
            });
        }
    }

    // Check if the browser supports the userAgentData API
    if (navigator.userAgentData) {
        // Get the User-Agent header data
        navigator.userAgentData.getHighEntropyValues(['uaFull']).then(function (uaData) {
            // Append "customUserAgent" to the User-Agent header
            uaData.uaFull = getNewUserAgent(uaData.uaFull, customUserAgent);

            // Override the User-Agent header with the modified value
            navigator.userAgentData.setHighEntropyValues(uaData);
        });
    }
}

setUserAgent2(window, 'CustomUserAgent/1.0'); // 在原来的userAgent后面append 'CustomUserAgent/1.0'

```

## Mobile client 修改UserAgent Header

- [WKWebView 设置自定义UserAgent正确姿势](https://juejin.cn/post/6844903632152821773)
- [iOS修改WebView的UserAgent](https://juejin.cn/post/6844904030980800519)
  - [iOS修改UserAgent](https://juejin.cn/post/6844903848671199239)

## 浏览器中修改UserAgent Header

Chrome中修改一下userAgent:

- 首先打开开发者工具(F12)
- 点开关闭箭头左侧更多选项, 选择More tools, 然后选择Network conditions
- 在开发者工具下方会多出来一个Network conditions菜单栏, 这里有User agent配置, 取消勾选Use browser default, 然后选择一些其他的选项或者自己输入一些内容.
- 刷新页面后， `window.navigator`, 和网络请求头中的User Agent都会变成了刚才修改的内容

## 利用userAgent检测浏览器

### userAgent string直接判断

```javascript
const isIE = !!document.all,
        docMode = document.documentMode, // available in IE browsers, The documentMode only works in Internet Explorer. All other browsers return undefined. https://www.w3schools.com/jsref/prop_doc_documentmode.asp
        ua = navigator.userAgent,
        isIE6 = false,
        isIE7 = false,
        isIE8 = false,
        isIE9 = false,
        isIE10 = false,
        isIE11 = !isIE && 'ActiveXObject' in window, // IE11 dose not act like IE<=10
        isDXIE = false;
    isIE = isIE || isIE11;

    if (isIE) {
        if (isEdgeModeEnabled) {
            isIE6 = !!ua.match(/MSIE 6/);
            isIE7 = ((!!ua.match(/MSIE 7/) && !docMode) || docMode === 7);  // IE7 or IE in IE7 Standards Mode
            isIE8 = (docMode === 8);    // IE in IE8 Standards Mode
            isIE9 = (docMode === 9);    // IE in IE9 Standards Mode
            isIE10 = (docMode === 10);  // IE in IE10 Standards Mode
            isDXIE = (!docMode || docMode <= 9); // IE9- supports DX filters
        } else {
            isIE6 = !!ua.match(/MSIE 6/);
            isIE7 = !!ua.match(/MSIE 7/);
            isIE8 = !!ua.match(/MSIE 8/);
            isIE9 = !!ua.match(/MSIE 9/);
            isIE10 = !!ua.match(/MSIE 10/);
            isDXIE = !isIE10;
        }
    }

    const isFireFox = !isIE && !!ua.match(/Firefox/),
        isAndroid = !!ua.match(/Android/),
        isIPad = !!ua.match(/iPad/),
        isIPhone = !!ua.match(/iPhone/),
        // iPad will default loading desktop website on iOS 13+
        isIOSTouchWithDesktopWebsite = !!ua.match(/Macintosh/) && 'ontouchend' in document,
        tch = !!document.createTouch || isAndroid,
        isPlayBook = !!ua.match(/PlayBook/),
        isWinPhone = !!ua.match(/Windows Phone/),
        isIEW3C = !isIE && !!ua.match(/Trident.*rv/),
        CSS3_PREFIX = isFireFox ? '-moz-' : (isIE || isIEW3C) ? '' : '-webkit-',
        CSS3_TRANSFORM_PREFIX = isFireFox ? 'Moz' : (isIE10 || isIEW3C) ? '' : isIE ? 'ms' : 'webkit',
        CSS3_T_INITIAL = ((isIE10 || isIEW3C) ? 't' : 'T'),
        CSS3_TRANSITION = CSS3_TRANSFORM_PREFIX + CSS3_T_INITIAL + 'ransition'; // IE9: N/A, IE10: transition, Chrome: webkitTransition, Moz: transition or MozTransransition
```

### 第三方库[ua-parser-js](https://www.npmjs.com/package/ua-parser-js)

包装了一些常用方法，使用起来更方便，[github](https://github.com/faisalman/ua-parser-js)。

```javascript
import UAParser from 'ua-parser-js';

let uaParser = new UAParser();
const osName = uaParser.getOS().name;
const deviceType = uaParser.getDevice().type;

export function getBrowserVersion() {
    return uaParser.getBrowser().version;
}

export function isSafari() {
    return uaParser.getBrowser().name === 'Safari' || uaParser.getBrowser().name === 'Mobile Safari';
}

export function isFirefox() {
    return uaParser.getBrowser().name === 'Firefox';
}

export function isChrome() {
    return uaParser.getBrowser().name === 'Chrome' || uaParser.getBrowser().name === 'Chrome WebView';
}

export function isIE() {
    return uaParser.getBrowser().name === 'IE' || uaParser.getBrowser().name === 'IE Mobile';
}

export function isEdge() {
    return uaParser.getBrowser().name === 'Edge';
}

export function isDesktop() {
    return ((isMacOS() || isWindows()) && window.navigator.maxTouchPoints <= 1) || isLinux();
}

export function isIpadIOS13AndAbove() {
    return isMacOS() && window.navigator.maxTouchPoints > 1;
}

export function isWindowsTablets() {
    return isWindows() && window.navigator.maxTouchPoints > 1;
}

export function isLinux() {
    return osName === 'Linux';
}

export function isMacOS() {
    return osName === 'Mac OS';
}

export function isWindows() {
    return osName === 'Windows';
}

export function isIPad() {
    return osName === 'iOS' && deviceType === 'tablet';
}
export function isIPhone() {
    return osName === 'iOS' && deviceType === 'mobile';
}

export function isIOS() {
    return osName === 'iOS';
}

export function isAndroid() {
    return osName === 'Android';
}

export function isAndroidPhone() {
    return osName === 'Android' && deviceType === 'mobile';
}

export function isMobile() {
    return deviceType === 'mobile';
}

export function isTouchable() {
    const maxTouchPoints = navigator.maxTouchPoints || navigator.msMaxTouchPoints;
    return (
        'ontouchstart' in window ||
        maxTouchPoints > 0 ||
        // Surface Laptop Firefox:
        // Touch is enabled and behaving as expect, but window.maxTouchPoints=0, which looks like a bug;
        // Use below method to detect instead.
        (window.matchMedia && matchMedia('(any-pointer: coarse)').matches)
    );
}

export function isSurface() {
    return osName === 'Windows' && isTouchable();
}

export function isTablet() {
    return deviceType === 'tablet' || isSurface();
}

export function isMobileOrTabletDevice() {
    return isTablet() || isMobile();
}
```

## 参考文章

- [userAgent是什么?如何根据它判断浏览器信息?](https://juejin.cn/post/7068080777195421709)
- [WKWebView 设置自定义UserAgent正确姿势](https://juejin.cn/post/6844903632152821773)
- [iOS修改WebView的UserAgent](https://juejin.cn/post/6844904030980800519)
  - [iOS修改UserAgent](https://juejin.cn/post/6844903848671199239)
- [Setting a custom userAgent in HTML or JavaScript](https://stackoverflow.com/questions/23248525/setting-a-custom-useragent-in-html-or-javascript)
- [How to change the UserAgent of a window opened with window.open(), if possible?](https://stackoverflow.com/questions/73744290/how-to-change-the-useragent-of-a-window-opened-with-window-open-if-possible)
