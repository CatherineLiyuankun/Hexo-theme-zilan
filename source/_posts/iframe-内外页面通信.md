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

## 在iframe内获取iframe外的内容

- [`window.parent`](https://developer.mozilla.org/en-US/docs/Web/API/Window/parent) 获取上一级的window对象。 如果当前窗口是一个 `<iframe>`, `<object>`, 或者 `<frame>`,则它的父窗口是嵌入它的那个窗口。如果还是iframe则是该iframe的window对象, 如果没有parent，则返回自身的引用。
- [window.top](https://developer.mozilla.org/en-US/docs/Web/API/Window/top) 获取最顶级容器的window对象，即，就是你打开页面的window
- [window.self](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/self) 返回自身window的引用。可以理解 `window===window.self`
- [window.frames](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/frames) 当前窗口的所有直接子窗口
- window.open/window.opener 使用window.open返回的对象

![iframe之间parent关系](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fbd94862dba4460d970290261cdf3bf2~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp?)

例如，想在iframe内获取所有parent的`userAgent`，检查是否含有
HTML结构：

- parent.html
  - iframe    child1
  - iframe    child2

执行结果：![执行结果](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/iframe%E5%86%85%E5%A4%96%E9%A1%B5%E9%9D%A2%E9%80%9A%E4%BF%A1/iframeUserAgent.png)

<details>
  <summary>点击展开parent.html代码</summary>
  <p>
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>parent</title>
    <style>
        input {
            width: 97%;
        }

        iframe {
            width: 100%;
        }
    </style>
</head>

<body>
    <script type="text/javascript">
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

        setUserAgent(window, 'CustomUserAgent/1.0'); // append CustomUserAgent/1.0 to the original userAgent

        const a = document.createElement('input');
        a.value = 'parent ' + window.navigator.userAgent;
        document.body && document.body.appendChild(a);

        let isCustomUserAgent = window.navigator && window.navigator.userAgent.indexOf('CustomUserAgent') >= 0;
        let curWindow = window;
        // check if window.top equals window, if not, check it's parent
        while (window.top !== curWindow) {
            curWindow = curWindow.parent;
            const newUserAgent = curWindow.navigator.userAgent;
            if (newUserAgent && newUserAgent.indexOf('CustomUserAgent') >= 0) {
                isCustomUserAgent = true;
                break;
            }
        }

        const b = document.createElement('input');
        b.value = 'isCustomUserAgent ' + isCustomUserAgent;
        document.body && document.body.appendChild(b);

    </script>
    <iframe src="child1.html"></iframe>
</body>

</html>
```
  </p>
</details>

<details>
  <summary>点击展开child1.html代码</summary>
  <p>
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8" />
    <title>child1</title>

    <style>
        input {
            width: 97%;
        }

        iframe {
            width: 100%;
        }
    </style>
</head>

<body>
    <!--    我是child1 -->
    <script type="text/javascript">
        const currUserAgent = document.createElement('input');
        currUserAgent.value = 'child1 ' + window.navigator.userAgent;
        document.body && document.body.appendChild(currUserAgent);

        let isCustomUserAgent = window.navigator && window.navigator.userAgent.indexOf('CustomUserAgent') >= 0;
        let curWindow = window;
        let isParentPowerPoint;
        // check if window.top equals window, if not, check it's parent
        try {
            while (window.top !== curWindow) {
                curWindow = curWindow.parent;
                const newUserAgent = curWindow.navigator.userAgent;
                if (newUserAgent && newUserAgent.indexOf('CustomUserAgent') >= 0) {
                    isCustomUserAgent = true;
                    break;
                }
            }
        } catch (error) {
            console.log(error);
        }

        const b = document.createElement('input');
        b.value = 'isCustomUserAgent from ancestor ' + isCustomUserAgent;
        document.body && document.body.appendChild(b);
    </script>

    <iframe src="child2.html"></iframe>

</body>

</html>
```
  </p>
</details>

<details>
  <summary>点击展开child2.html代码</summary>
  <p>
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8" />
    <title>child2</title>
    <style>
        input {
            width: 97%;
        }

        iframe {
            width: 100%;
        }
    </style>
</head>

<body>
    <!--    我是child2 -->
    <script type="text/javascript">
        const currUserAgent = document.createElement('input');
        currUserAgent.value = 'child2 ' + window.navigator.userAgent;
        document.body && document.body.appendChild(currUserAgent);

        let isCustomUserAgent = window.navigator && window.navigator.userAgent.indexOf('CustomUserAgent') >= 0;
        let curWindow = window;
        // check if window.top equals window, if not, check it's parent
        while (window.top !== curWindow) {
            curWindow = curWindow.parent;
            const newUserAgent = curWindow && curWindow.navigator.userAgent;
            if (newUserAgent && newUserAgent.indexOf('CustomUserAgent') >= 0) {
                isCustomUserAgent = true;
                break;
            }
        }

        const b = document.createElement('input');
        b.value = 'isCustomUserAgent from ancestor ' + isCustomUserAgent;
        document.body.appendChild(b);
    </script>
</body>

</html>
```
  </p>
</details>

## 在iframe外获取iframe里的内容

### 方法一 `contentWindow`和`contentDocument`

- `iframe.contentWindow`可以获取iframe的window对象, [MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLIFrameElement/contentWindow)
- `iframe.contentDocument`可以获取iframe的document对象, [MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLIFrameElement/contentDocument)。

```javascript
// const iframe = document.getElementById("iframe1");
const iframe = document.querySelector("iframe");

const iContentWindow = iframe.contentWindow;

const idoc = iContentWindow.document;
const iContentDocument = iframe.contentDocument;
const isSameDoc = iframe.contentDocument === iframe.contentWindow.document; // true


console.log("iframe.contentWindow", iContentWindow); // 获取iframe的window对象 iframe.contentWindow
console.log("iframe.contentDocument", iContentDocument);  // 获取iframe的document  iframe.contentDocument
console.log("html", iContentDocument.documentElement); // 获取iframe的html
```

### 方法二 window.frames

结合Name属性，通过window提供的frames获取

- [window.frames](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/frames) 当前窗口的所有直接子窗口

```html
<iframe src ="/index.html" id="ifr1" name="ifr2" scrolling="yes">
  <p>Your browser does not support iframes.</p>
</iframe>
<script type="text/javascript">
    console.log(window.frames['ifr2'].window);
    console.dir(document.getElementById("iframe").contentWindow);
</script>
```

## 跨域通信

### 跨域

为了保证用户信息的安全，95年的时候Netscape公司引进了同源策略，里面的同源指的是三个相同：

- 协议（例如 https， http）
- 端口号（例如 8080,8443，443）
- 域名 (`document.domain`设置为相同的值)

违反了同源策略就会出现跨域问题，主要表现为以下三方面：

- 无法读取cookie、localStorage、indexDB
- DOM无法获得
- ajax请求无法发送

### iframe缺点以及解决方案

缺点:

- iframe会阻塞主页面的Onload事件；要确保在iframe加载完成后再进行操作，如果iframe还未加载完成就开始调用里面的方法或变量，会产生错误；
  - 判断iframe加载完成

```javascript
iframe.onload = function() {
    // TODO
}
```

- 相同域iframe和主页面共享http连接池，所以如果相同域用多个iframe会阻塞加载
  - 解决方案： 动态生成iframe，在主页面加载完成后去生产iframe加载，从而避免阻塞的影响
- iframe 对SEO不友好
  - 解决方案：在广告位以及内部系统等适合的场景中使用iframe
- 如果iframe所链接的是外部页面，因为安全机制不能使用同域名下的通信方式；

### 跨域通信方法一设置`document.domain`

例子：需要用iframe引入一个别人封装好的类似视频播放器的东西。iframe里面有一个全屏的按钮，点击后需要页面让iframe全屏，由于受到同源策略的限制，iframe无法告诉页面全屏。

`document.domain`作用是获取/设置当前文档的原始域部分，同源策略会判断两个文档的原始域是否相同来判断是否跨域。这意味着只要把这个值设置成一样就可以解决跨域问题了。
在此将domain设置为一级域名的值，a页面url为`a.demo.com`，a页面中iframe引用的b页面url为`b.demo.com`，具体设置为`document.domain = 'demo.com'`
设置完之后，在a页面的window上挂载使iframe全屏的方法

- a页面 `a.demo.com`
  - iframe b页面 `b.demo.com`

```javascript
// a页面
window.toggleFullScreen = () => {
    // do something
}
```

在b页面上可以直接获取到a页面的window对象并直接调用

```javascript
// b页面
window.parent.toggleFullScreen()
```

但是这个值的设置也有一定限制，只能设置为当前文档的上一级域或者是跟该文档的URL的domain一致的值。如url为`a.demo.com`，那domain就只能设置为`demo.com`或者`a.demo.com`。因此，设置domain的方法只能用于解决**主域相同而子域不同**的情况。

### 跨域通信方法二使用中间页面

我们还可以使用一个与a页面同域名但不同路由的c页面作为中间页面，b页面加载c页面，c页面调用a页面的方法，从而实现b页面调用a页面的方法。
在a页面的node层新开一个路由，此路由加载一个c页面作为中间页面，c页面的url为a.demo.com/c。c页面只是一个简单的html页面，在window的onload事件上调用了a页面的方法。

- a页面 `a.demo.com`
  - iframe b页面
    - iframe c页面 【中间页`a.demo.com/c`】(与a页面同域名但不同路由, c页面调用a页面的方法，从而实现b页面调用a页面的方法)

由于c页面和a页面是符合同源策略的，所以可以避开跨域问题，执行全屏的方法。

```html
<!-- c页面 -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <script>
        window.onload = function () {
            parent.parent.toggleFullScreen();
        }
    </script>
</body>
</html>
```

由于c页面和a页面是符合同源策略的，所以可以避开跨域问题，执行全屏的方法。

### 跨域通信方法三`window.postMessage`

[window.postMessage方法可以安全地实现跨源通信](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/postMessage)，写明目标窗口的协议、主机地址或端口就可以发信息给它。

- a页面 `a.demo.com`
  - iframe b页面 `b.demo.com`

```javascript
// b页面
parent.postMessage(
    value,
    "http://a.demo.com"
);
```

```javascript
// a页面
window.addEventListener("message", function( event ) {
    // 为了安全，收到信息后要检测下event.origin判断是否要收信息的窗口发过来的。
    if (event.origin !== 'http://b.demo.com') return;
    toggleFullScreen()
 });
```

#### 兼容性

需要注意的是postMessage API中的message在ie8/ie9等一些低版本浏览器中，中是不支持除String以外的其他类型时（因为不支持结构化克隆算法），所以，如果要兼容低版本ie，需要通过JSON.strigify以及JSON.parse去发送和接受。

### 父页面向子页面传递数据

利用location对象的hash值，通过它传递通信数据。在父页面设置iframe的src后面多加个data字符串，然后在子页面中通过某种方式能即时的获取到这儿的data。

### 浏览器Disable same origin policy

用本地文件测试frame的时候，在执行`curWindow.navigator.userAgent`的时候会报错：
`Uncaught DOMException: Blocked a frame with origin "null" from accessing a cross-origin frame.`

原因是浏览器默认开启了CORS的安全保护，不允许iframe跨域获取一些值。

解决方案：参考 [Disable same origin policy in Chrome](https://stackoverflow.com/questions/3102819/disable-same-origin-policy-in-chrome)， 命令行加参数`--disable-web-security`打开chrome浏览器

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

## 参考文章

- [JS对Iframe内外页面进行操作](https://juejin.cn/post/7017740414060855310)
- [iframe跨域的几种常用方法](https://juejin.cn/post/6844903831973675015)
- [Web前端之iframe详解](https://zhuanlan.zhihu.com/p/168764040)
- [Iframe父子窗口通信](https://juejin.cn/post/6961791208876146718)
- [MDN Window.parent](https://developer.mozilla.org/en-US/docs/Web/API/Window/parent)
- [Disable same origin policy in Chrome](https://stackoverflow.com/questions/3102819/disable-same-origin-policy-in-chrome)
- [不同源iframe跨域问题（window.postMessage）](https://blog.csdn.net/weixin_43959024/article/details/118152348)
