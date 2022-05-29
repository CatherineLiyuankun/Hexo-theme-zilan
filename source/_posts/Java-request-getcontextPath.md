---
title: Java request.getcontextPath()
catalog: true
date: 2019-07-14 13:57:11
subtitle:
header-img:
tags:
- Java
categories:
- TECH
- BackEnd
- Java
---

# 解决相对路径的问题

`request.getContextPath()`：是在开发Web项目时，经常用到的方法，是为了解决相对路径的问题，可返回站点的根路径。

比如：要生成一个文件放在服务器上得一个目录下,可以使用request.getContextPath()+/dir,组成一个完整得目录结构.

当使用Tomcat作为Web服务器，项目一般部署在Tomcat下的webapps的目录下。具体来说主要用两种部署的路径：

- 将web项目中的webRoot下的文件直接拷贝到webapps/ROOT下（删除ROOT下的原有文件）；

- 在Tomcat下的webapps中创建以项目名称命名（当然也可以用其他的名称）的文件夹，并将webRoot下的文件直接拷贝到该文件夹下。

对于第一部署方法，`request.getContextPath()`的返回值为空（即：`""`,中间无空格，注意区分`null`)。

对于第二部署方法，其返回值为：`/创建的文件夹的名称`。


## URL实例

假定你的web application 名称为liyuankun,你在浏览器中输入请求路径：

`http://localhost:8080/liyuankun/main/test.jsp`

则执行下面向行代码后打印出如下结果：

1. `System.out.println(request.getContextPath());`

打印结果：`/liyuankun`

2. `System.out.println(request.getServletPath());`

打印结果：`/main/test.jsp`

3. `System.out.println(request.getRequestURI());`

打印结果：`/liyuankun/main/test.jsp`

4. `System.out.println(request.getRealPath("/"));`

打印结果：`\Tomcat所在目录\webapps\liyuankun\test`

`request.getSchema()`可以返回当前页面使用的协议，http、https等, 这里是`http`;

`request.getServerName()`可以返回当前页面所在的服务器的名字, 这里是`localhost`;

`request.getServerPort()`可以返回当前页面所在的服务器使用的端口,这里是`8080`;

实际应用中，一般用来解决jsp测试和生产环境路径不同的问题：

```JSP
<%
 String appContext = request.getContextPath();
 String basePath =request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort() + appContext; 
%>

```

```java
public static String buildAbsoluteUrl(HttpServletRequest request, String relativePath, String queryString) {
   return UrlUtils.buildFullRequestUrl(request.getScheme(), request.getServerName(), request.getServerPort(), request.getContextPath() + relativePath, queryString);
}
```

## 参考链接

- [request.getcontextPath() 详解](https://blog.csdn.net/haojiahj/article/details/8796472)
