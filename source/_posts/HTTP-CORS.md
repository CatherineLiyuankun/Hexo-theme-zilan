---
title: HTTP CORS
catalog: true
date: 2019-10-12 15:51:01
subtitle: "跨域资源共享（Cross-origin resource sharing）"
tags:
- CORS
categories:
- TECH
- Network
- Servlet/HTTP
---

Reference Links里的两篇文章讲述的已经很详细了。简单列一下：

# 0 CORS

简单说就是从A网址（origin (domain) ）向B网址发送请求，称为跨域。从A网址向A网址发送请求就是，同域。
- [Cross-Origin Resource Sharing (CORS)](https://web.dev/cross-origin-resource-sharing/?utm_source=devtools#preflight-requests-for-complex-http-calls)
- [MDN 跨源资源共享（CORS）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)
<!-- [Cross-Origin Resource Sharing (CORS)](https://web.dev/i18n/en/cross-origin-resource-sharing/) -->

## Same-origin

A 与 B 什么不同？
[同源策略 Same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy?ref=hackernoon.com)
> 如果两个 URL 的协议、端口（如果有指定的话）和主机都相同的话，则这两个 URL 是同源的。

[What is a URL?](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL)

Different origin：

- 协议 protocol
- 主机/域 host， host可能是 `domain name`,或者是`IP address`
- 端口 port

例如 `https://localhost:8443/test/to/myfile.html`

- Protocol/Scheme: `https`
- Host: `localhost`
- port: `8443`
- path: `/test/to/myfile.html`
- Origin: <https://localhost:8443>

违反了同源策略就会出现跨域问题，主要表现为以下三方面：

- 无法读取cookie、localStorage、indexDB
- DOM无法获得
- ajax请求无法发送
- can't access an <iframe> with different origin using JavaScript, browsers block scripts trying to access a frame with a different origin.

## Cross-Origin

![CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS/cors_principle.png)

## [CORS headers](https://developer.mozilla.org/en-US/docs/Glossary/CORS#cors_headers)

[Access-Control-Allow-Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Origin)
指示响应的资源是否可以被给定的origin共享。

[Access-Control-Allow-Credentials](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Credentials)
指示当请求的凭证标记为 true 时，是否可以公开对该请求响应。

[Access-Control-Allow-Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Headers)
用在对预检请求的响应中，指示实际的请求中可以使用哪些 HTTP 标头。

[Access-Control-Allow-Methods](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Methods)
指定对预检请求的响应中，哪些 HTTP 方法允许访问请求的资源。

[Access-Control-Expose-Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Expose-Headers)
通过列出标头的名称，指示哪些标头可以作为响应的一部分公开。

[Access-Control-Max-Age](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Max-Age)
指示预检请求的结果能被缓存多久。

[Access-Control-Request-Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Request-Headers)
用于发起一个预检请求，告知服务器正式请求会使用哪些 HTTP 标头。

[Access-Control-Request-Method](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Request-Method)
用于发起一个预检请求，告知服务器正式请求会使用哪一种 HTTP 请求方法。

[Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Origin)
指示获取资源的请求是从什么源发起的。

# CORS请求流程

来源：[CORS 简单请求+预检请求（彻底理解跨域）](https://github.com/amandakelake/blog/issues/62)
![CORS请求流程](https://user-images.githubusercontent.com/25027560/50205881-c409b080-03a4-11e9-8a57-a2a6d0e1d879.png)

# Disable CORS limit

关闭浏览器CORS：[Disable CORS limit](../HTTP-CORS-disable.html)

# 访问控制场景

## 1. 简单请求（simple request）
>
>（1) 请求方法是以下三种方法之一：
>
>- HEAD
>- GET
>- POST

>（2）HTTP的头信息不超出以下几种字段：
>
>- Accept
>- Accept-Language
>- Content-Language
>- Last-Event-ID
>- Content-Type：只限于三个值application/x-www-form-urlencoded、multipart/form-data、text/ plain
>- DPR
>- Downlink
>- Save-Data
>- Viewport-Width
>- Width

>（3）请求中的任意XMLHttpRequestUpload 对象均没有注册任何事件监听器；XMLHttpRequestUpload 对象可以使用 XMLHttpRequest.upload 属性访问。
>（4）请求中没有使用 ReadableStream 对象。

假如站点 <http://Server-b.com> 的网页应用想要访问 <http://bar.other> 的资源。
A向B请求，那么A就是Orign.
![简单请求（simple request）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS/simple-req.png)

## 2. 非简单请求（not-so-simple request）
>
> 非简单请求是那种对服务器有特殊要求的请求，比如请求方法是PUT或DELETE，或者Content-Type字段的类型是application/json。

>（1) 使用了下面任一 HTTP 方法：
>
>- PUT
>- DELETE
>- CONNECT
>- OPTIONS
>- TRACE
>- PATCH

>（2) 人为设置了对 CORS 安全的首部字段集合之外的其他首部字段。该集合为：
>
>- Accept
>- Accept-Language
>- Content-Language
>- Content-Type (需要注意额外的限制)
>- DPR
>- Downlink
>- Save-Data
>- Viewport-Width
>- Width

>（3) Content-Type 的值不属于下列之一:
>
>- application/x-www-form-urlencoded
>- multipart/form-data
>- text/plain

>（4) 请求中的XMLHttpRequestUpload 对象注册了任意多个事件监听器。

>（5) 请求中使用了ReadableStream对象。

假如站点 <http://foo.example> 的网页应用想要访问 <http://bar.other> 的资源。

![预检请求+真实请求](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS/preflight_correct.png)

### 2.1 预检请求 OPTION

OPTION 由于跨域请求被拦截，返回503：
 ![OPTION 503](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/HTTP-CORS/OPTION%20503.png)

 Error:

```javascript
Access to XMLHttpRequest at 'https://B' from origin 'https://A' 
has been blocked by CORS policy: 
Response to preflight request doesn't pass access control check: It does not have HTTP ok status.
```

### 2.2 真实请求

## 3 附带身份凭证的请求
>
> 它其实必然是1 简单请求（simple request）2. 非简单请求（not-so-simple request）的其中一种。只是多加了对Cookie和HTTP认证信息的判断。
CORS请求默认不发送Cookie和HTTP认证信息。如果要把Cookie发到服务器，一方面要服务器同意，指定Access-Control-Allow-Credentials字段。

```javascript
Access-Control-Allow-Credentials: true
```

另一方面，开发者必须在AJAX请求中打开withCredentials属性。

```javascript
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;
```

否则，即使服务器同意发送Cookie，浏览器也不会发送。或者，服务器要求设置Cookie，浏览器也不会处理。

但是，如果省略withCredentials设置，有的浏览器还是会一起发送Cookie。这时，可以显式关闭withCredentials。

```javascript
xhr.withCredentials = false;
```

A向B请求。`需要注意的是，如果要发送Cookie，Access-Control-Allow-Origin就不能设为星号，必须指定明确的、与请求网页A一致的域名。`否则报错：

```javascript
Access to XMLHttpRequest at 'https://B' from origin 'https://A' has been blocked by CORS policy: 
The value of the 'Access-Control-Allow-Origin' header in the response must not be 
the wildcard '*' when the request's credentials mode is 'include'.
The credentials mode of requests initiated by the XMLHttpRequest 
is controlled by the withCredentials attribute.
```

 同时，Cookie依然遵循同源政策，只有用服务器域名B设置的Cookie才会上传，其他域名的Cookie并不会上传，且（跨源）原网页A代码中的document.cookie也无法读取服务器域名下的Cookie。

![附带身份凭证的请求](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS/cred-req-updated.png)

# Reference Links

- [Cross-Origin Resource Sharing (CORS)](https://web.dev/cross-origin-resource-sharing/?utm_source=devtools#preflight-requests-for-complex-http-calls)
- [MDN HTTP访问控制（CORS）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)
- [跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)
- [CORS 简单请求+预检请求（彻底理解跨域）](https://github.com/amandakelake/blog/issues/62)
