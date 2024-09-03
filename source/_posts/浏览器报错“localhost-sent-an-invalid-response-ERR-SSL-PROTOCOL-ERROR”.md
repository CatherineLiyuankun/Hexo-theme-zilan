---
title: 浏览器报错“localhost sent an invalid response.ERR_SSL_PROTOCOL_ERROR”
catalog: true
date: 2024-09-03 18:02:25
subtitle:
header-img:
tags:
categories:
- TECH
---


当浏览器访问http的本地开发环境时，`http://localhost:4000/` , 浏览器报错：

```bash
localhost sent an invalid response.
ERR_SSL_PROTOCOL_ERROR
```

The `ERR_SSL_PROTOCOL_ERROR` in Chrome typically occurs when you're trying to access a local development server (like one running on `http://localhost:4000`) over HTTPS `https://localhost:4000` instead of HTTP. If your server isn't set up to handle HTTPS, Chrome may block the connection because it expects a valid SSL certificate, which isn't usually present on local servers.

## 解决方法

因为HSTS，浏览器会自动把我的http的网址`http://localhost:4000/` 自动redirect到HTTPS `https://localhost:4000`, 所以用方法1，2都可以解决。

### 前提 确保使用的是HTTP

Ensure You’re Using HTTP, Not HTTPS:

- Make sure you're visiting `http://localhost:4000` (not `https://localhost:4000`).
- Check the URL bar and explicitly type `http://` before `localhost:4000` if necessary.

### 方法一 清除HSTS设置

Disable HTTPS Enforcement in Chrome:
Chrome may automatically redirect to HTTPS if it previously visited the site over HTTPS. You can clear this by:

- Clearing the HSTS Settings for localhost:
  - Go to chrome://net-internals/#hsts in your Chrome browser.
  - Under the "Delete domain security policies" section, type localhost and click "Delete".

### 方法二 使用浏览器匿名模式 Incognito Window

Sometimes, Chrome caches HSTS settings. Opening an incognito window might avoid the cached redirection to HTTPS.

### 方法三 Check for Extensions or Proxy Settings

Ensure no Chrome extensions or proxy settings are forcing HTTPS. Disable any such extensions or settings temporarily to test.

### 方法四 Update Your Server Configuration (Optional)

If you need to serve your local site over HTTPS, configure your development server to support HTTPS. This typically involves generating a self-signed SSL certificate and configuring your server to use it.

### 方法五 ypass the SSL Error (Not Recommended for Regular Use)

If you still need to bypass the SSL check, you can type `thisisunsafe` directly on the error page in Chrome. It will bypass the SSL warning, but this is generally not recommended for regular use.

### 总结

- Start by confirming you're accessing `http://localhost:4000`, not `https://localhost:4000`.
- If Chrome still redirects to HTTPS or shows an SSL error, try clearing the HSTS settings for `localhost` or using an incognito window.
