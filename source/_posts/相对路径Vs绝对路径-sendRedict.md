---
title: 相对路径Vs绝对路径 & sendRedict
catalog: true
date: 2022-05-29 15:46:38
subtitle: URI,relative/absolute URL
header-img:
tags:
- Java
categories:
- TECH
- BackEnd
- Java
---

<!-- ## 相对路径Vs绝对路径 -->

## 相对URL Vs 绝对URL

### URI

- `URI` (`Uniform Resource Identifier`)：[统一资源标志符](https://developer.mozilla.org/en-US/docs/Glossary/URI)。 A `URI`  is a string that refers to a resource.
  - `URL` (`Univeral Resource Locator`): [统一资源定位符](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL)
    > The most common are URLs, which identify the resource by giving its location on the Web.
  - `URN`(`Univeral Resource Name`) [统一资源定名称](https://developer.mozilla.org/en-US/docs/Glossary/URN)
    > by contrast, refer to a resource by a name, in a given namespace, such as the `ISBN` of a book. URN (Uniform Resource Name) is a URI in a standard format, referring to a resource without specifying its location or whether it exists. This example comes from RFC3986: urn:oasis:names:specification:docbook:dtd:xml:4.1.2

    `URN`只命名资源而不指定如何定位资源，例如：urn:isbn:0451450523 指定了一本书的`ISBN`，可以唯一标识这本书，但没有指定到哪里定位这本书。

`URL`和`URN`都是`URI`的子集。

### URL结构

![URL结构](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL/mdn-url-all.png)

`Scheme`(Protocol), `Domain name`(Host), `Port`, `Path`, `Parameters`(queryString) and `Anchor`(#, also known as the `fragment identifier`).

### Valid 相对URL Vs 绝对URL

The [URL standard](https://url.spec.whatwg.org/#absolute-url-string) defines

- [absolute URL string](https://url.spec.whatwg.org/#absolute-url-string): A URI is absolute if, and only if, it has a `scheme` component.
- [relative URL string](https://url.spec.whatwg.org/#relative-url-string), to distinguish them from [URL objects](https://url.spec.whatwg.org/#url) (which are in-memory representations of URLs).


>A URL specifies the location of a target stored on a local or networked computer. The target can be a file, directory, HTML page, image, program, and so on.

>An `absolute URL` contains all the information necessary to locate a resource.

>A `relative URL` locates a resource using an absolute URL as a starting point. In effect, the "complete URL" of the target is specified by concatenating the absolute and relative URLs.

>An absolute URL uses the following format: scheme://server/path/resource

>A relative URL typically consists only of the path, and optionally, the resource, but no scheme or server. The following tables define the individual parts of the complete URL format.

### 判断相对路径Or绝对路径

```java
// java/net/URI.java
    /**
     * Tells whether or not this URI is absolute.
     *
     * <p> A URI is absolute if, and only if, it has a scheme component. </p>
     *
     * @return  {@code true} if, and only if, this URI is absolute
     */
    public boolean isAbsolute() {
        return scheme != null;
    }
```

### URL参考文章

- [What is a URL?](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL)
- [What is a URL? 中文版](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_is_a_URL)
- [Are URIs case-insensitive?](https://stackoverflow.com/questions/15641694/are-uris-case-insensitive)
- [URL, valid URL string, URL parser, and URL serializer](https://url.spec.whatwg.org/#urls)
- [Relative URL containing just the querystring](https://stackoverflow.com/questions/15291307/relative-url-containing-just-the-querystring)
- [How to test if a URL string is absolute or relative in javascript?](https://stackoverflow.com/questions/10687099/how-to-test-if-a-url-string-is-absolute-or-relative)
- [determine if a string is absolute URL or relative URL in java](https://stackoverflow.com/questions/4390800/determine-if-a-string-is-absolute-url-or-relative-url-in-java)

## HTML File Paths

当前页面如果是`https://www.w3schools.com/html/tryit.asp?filename=tryhtml_files_absoulute` 和 `http://localhost:8080/webapp/servlet/web`

| 分类 | Relative Path | Absolute Path  | Description
| ------| ------------- | ---------------- | ---------------- |
| 1 相对当前路径 `.`表示当前路径，在通道情况下可以省略，只有在特殊的情况下不能省略 | `<img src="picture.jpg">`  |`https://www.w3schools.com/html/picture.jpg` `http://localhost:8080/webapp/servlet/picture.jpg`  | The "picture.jpg" file is located in **the same folder as the current page** |
| . | `<img src="./picture.jpg">`  |`https://www.w3schools.com/html/picture.jpg` `http://localhost:8080/webapp/servlet/picture.jpg`  | The "picture.jpg" file is located in **the same folder as the current page** |
| `././`同`./` | `<img src="././picture.jpg">`  |`https://www.w3schools.com/html/picture.jpg` `http://localhost:8080/webapp/servlet/picture.jpg`  | The "picture.jpg" file is located in **the same folder as the current page** |
| . | `<img src="images/picture.jpg">` |`https://www.w3schools.com/html/images/picture.jpg` `http://localhost:8080/webapp/servlet/images/picture.jpg` | The "picture.jpg" file is located in the images folder in the **current folder**|
| queryString | `<a href="?filename=tryhtml_files_relative">Next</a>`| `https://www.w3schools.com/html/tryit.asp?filename=tryhtml_files_relative`  | The "picture.jpg" file is located **the same folder as the current page**  |
|2 相对根路径| `<img src="/images/picture.jpg">` | `https://www.w3schools.com/images/picture.jpg` `http://localhost:8080/images/picture.jpg` | The "picture.jpg" file is located in the images folder at the **root of the current web** |
|3 相对上一层路径| `<img src="../picture.jpg">`| `https://www.w3schools.com/picture.jpg` `http://localhost:8080/webapp/picture.jpg` | The "picture.jpg" file is located in the folder **one level up** from the current folder  |
| 上两层，有几个`../`，就向上跳几级 | `<img src="../../picture.jpg">`| 因为../已经到根目录，../../无法再向上一层目录`https://www.w3schools.com/picture.jpg` `http://localhost:8080/picture.jpg` | The "picture.jpg" file is located in the folder **two level up** from the current folder  |
| 上一层 | `<img src=".././picture.jpg">`| `https://www.w3schools.com/picture.jpg` `http://localhost:8080/webapp/picture.jpg` | The "picture.jpg" file is located in the folder **one level up** from the current folder  |
| `./` 和`../`可结合多个一起使用 | `<img src="../images/.././picture.jpg">`| `https://www.w3schools.com/picture.jpg` `http://localhost:8080/webapp/picture.jpg` | The "picture.jpg" file is located in the folder **one level up** from the current folder |


```javascript
function getRealPath(){
   var curPath = window.document.location.href; // 'https://www.w3schools.com/html/tryit.asp?filename=tryhtml_files_absoulute'
   var pathName = window.document.location.pathname; // '/html/tryit.asp'
   var localhostPath=curPath.substring(0, curPath.indexOf(pathName)); // 'https://www.w3schools.com'
   var projectName = pathName.substring(0,pathName.substr(1).indexOf('/')+1); // '/html'
   return localhostPath + projectName; // 'https://www.w3schools.com/html'
}

```

### HTML File Paths参考文章

- [HTML File Paths](https://www.w3schools.com/html/html_filepaths.asp)

## Web Servlet `sendRedict()` 使用相对路径

可以使用相对URL作为sendRedirect的参数，而不是指定完整的"http:/www...”.
`相对URL`有两种类型：

- 前面有斜线(“/”): 相对于web容器的根目录（relative to the root of this web Container）。
- 没有斜线： 相对于当前路径。

> You can use a relative URL as the argument to sendRedirect(), instead of specifying the whole “<http://www>...” thing. Relative URLs come in two flavors: with or without a starting forward slash (“/”).

`sendRedirect`能够处理相对URL，自动把它们转换成绝对URL，如果地址是相对的，没有一个‘/’，那么Web container就认为它是相对于当前的请求URI的。

- 如果为`response.sendRedirect("login.jsp")`，则会从当前servlet 的URL路径下找login.jsp： `http://10.1.18.8:8081/dms/servlet/Servlet` 重定向的URL: `http://10.1.18.8:8081/dms/servlet/login.jsp`
- 如果为`response.sendRedirect("/login.jsp")`则会从当前应用路径下查找url: `http://10.1.18.8:8081/login.jsp`。而forward不能这样处理相对路径。

### 相对URL without “/”

假设客户原来所在页面是：

<!-- > Imagine the client originally typed in: -->

`http://www.wickedlysmart.com/myApp/cool/bar.do`

相对URL没有用斜线开头：

![`sendRedirect("foo/stuff.html");`](https://www.oreilly.com/library/view/head-first-servlets/9780596516680/httpatomoreillycomsourceoreillyimages2242605.png.jpg)

容器会相对于原先的请求URL建立完整的URL（需要把它放在HTTP响应
的“Location”首部中）
`http://www.wickedlysmart.com/myApp/cool/foo/stuff.html`

### 相对URL with “/”

> But if the argument to sendRedirect() DOES start with a forward slash: `sendRedirect("/foo/stuff.html')`
> The Container builds the complete URL relative to the web Container itself, instead of relative to the original URL of the request. So the new URL will be:

但是如果sendRedirecto的参数确实以一个斜线开头：

![`sendRedirect("/foo/stuff.html')`](https://www.oreilly.com/library/view/head-first-servlets/9780596516680/httpatomoreillycomsourceoreillyimages2242607.png.jpg)

容器就会相对于Web应用本身建立完整的URL，而不是相对于请求原来的URL。 所以新的URL是：

![`http://www.wickedlysmart.com/foo/stuff.html`](https://www.oreilly.com/library/view/head-first-servlets/9780596516680/httpatomoreillycomsourceoreillyimages2242609.png.jpg)

>**WATCH IT!**
**You can’t do a sendRedirect() after writing to the response!**
That’s probably obvious, but it’s the LAW so we’re just making sure.
If you look up sendRedirect() in the API, you’ll see that it throws an IllegalStateException if you try to invoke it after “the response has already been committed.”
By “committed”, they mean that the response has been sent. That just means the data has been flushed to the stream.
For practical purposes, it means **you can’t write to the response and then call sendRedirect()!**
But some picky professor will tell you that technically, you could write to the stream without flushing, and then sendRedirect() wouldn’t cause an exception. But it would be a completely stupid thing to do, so we won’t talk about it. (Except that we just did... talk about it...)
In your servlet, for gosh sakes make a decision! Either handle the request or do a sendRedirect() to have someone ELSE handle the request.
(By the way, this idea that “once it’s committed it’s too late” also applies to setting headers, cookies, status codes, the content-type, and so on...)

>**NOTE**
**sendRedirect() takes a String, NOT a URL object!**
Well, it takes a String that IS a URL. The point is, sendRedirect() does NOT take an object of type URL. You pass it a String that’s either a complete URL or a relative one. If the Container can’t build a relative URL into a full one, it’ll throw an IllegalStateException. The tricky part is to remember that THIS is wrong: sendRedirect(new URL(“www.oreilly.com”));

### Servlet参考文章

- [How to send redirect from Java Servlet](https://www.codejava.net/java-ee/servlet/how-to-send-redirect-from-java-servlet)
- [Using relative URLs in sendRedirect()](https://learning.oreilly.com/library/view/head-first-servlets/9780596516680/ch04s27.html)
