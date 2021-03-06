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
## A 与 B 什么不同？
不同的域、协议或端口。

![CORS](https://mdn.mozillademos.org/files/14295/CORS_principle.png)

# 1. 简单请求（simple request）
>（1) 请求方法是以下三种方法之一：
>* HEAD
>* GET
>* POST

>（2）HTTP的头信息不超出以下几种字段：
>* Accept
>* Accept-Language
>* Content-Language
>* Last-Event-ID
>* Content-Type：只限于三个值application/x-www-form-urlencoded、multipart/form-data、text/ plain
>* DPR
>* Downlink
>* Save-Data
>* Viewport-Width
>* Width

>（3）请求中的任意XMLHttpRequestUpload 对象均没有注册任何事件监听器；XMLHttpRequestUpload 对象可以使用 XMLHttpRequest.upload 属性访问。
>（4）请求中没有使用 ReadableStream 对象。

假如站点 http://Server-b.com 的网页应用想要访问 http://bar.other 的资源。
A向B请求，那么A就是Orign.
![简单请求（simple request）](https://mdn.mozillademos.org/files/14293/simple_req.png)

# 2. 非简单请求（not-so-simple request）
> 非简单请求是那种对服务器有特殊要求的请求，比如请求方法是PUT或DELETE，或者Content-Type字段的类型是application/json。

>（1) 使用了下面任一 HTTP 方法：
>* PUT
>* DELETE
>* CONNECT
>* OPTIONS
>* TRACE
>* PATCH

>（2) 人为设置了对 CORS 安全的首部字段集合之外的其他首部字段。该集合为：
>* Accept
>* Accept-Language
>* Content-Language
>* Content-Type (需要注意额外的限制)
>* DPR
>* Downlink
>* Save-Data
>* Viewport-Width
>* Width

>（3) Content-Type 的值不属于下列之一:
>* application/x-www-form-urlencoded
>* multipart/form-data
>* text/plain

>（4) 请求中的XMLHttpRequestUpload 对象注册了任意多个事件监听器。

>（5) 请求中使用了ReadableStream对象。

假如站点 http://foo.example 的网页应用想要访问 http://bar.other 的资源。

![预检请求+真实请求](https://mdn.mozillademos.org/files/16753/preflight_correct.png)

## 2.1 预检请求 OPTION
OPTION 由于跨域请求被拦截，返回503：
 ![OPTION 503](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/HTTP-CORS/OPTION%20503.png)

 Error:
```javascript
Access to XMLHttpRequest at 'https://B' from origin 'https://A' 
has been blocked by CORS policy: 
Response to preflight request doesn't pass access control check: It does not have HTTP ok status.
```

## 2.2 真实请求

# 3 附带身份凭证的请求
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

![附带身份凭证的请求](https://mdn.mozillademos.org/files/14291/cred-req.png)

# 总结流程
来源：[CORS 简单请求+预检请求（彻底理解跨域）](https://github.com/amandakelake/blog/issues/62)
![CORS请求流程](https://user-images.githubusercontent.com/25027560/50205881-c409b080-03a4-11e9-8a57-a2a6d0e1d879.png)

# Reference Links:

[跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)
[HTTP访问控制（CORS）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)
[CORS 简单请求+预检请求（彻底理解跨域）](https://github.com/amandakelake/blog/issues/62)