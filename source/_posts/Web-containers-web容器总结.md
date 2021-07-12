---
title: web容器对比
catalog: true
date: 2021-07-12 16:53:32
subtitle: Tomcat、Weblogic、JBoss、GlassFish、Jetty、Resin、IBM Websphere
header-img:
tags:
categories:
- TECH
- BackEnd
- Java
---

# Web容器 Vs EJB容器 Vs Java EE容器

Web容器和EJB容器是Java EE容器的子集。 Java EE容器还包含应用程序客户端容器和applet容器。
*在文档中，他们使用多格式，但是实际上每个Java EE服务器只有一个Web容器和一个EJB容器。

> The deployment process installs Java EE application components in the Java EE containers.

> Application client container: Manages the execution of application client components. Application clients and their container run on the client.

> Applet container: Manages the execution of applets. Consists of a web browser and Java Plug-in running on the client together.

## EJB容器

> Enterprise JavaBeans (EJB) container: Manages the execution of enterprise beans for Java EE applications. Enterprise beans and their container run on the Java EE server.

## Java EE容器

> Java EE server: The runtime portion of a Java EE product. A Java EE server provides EJB [container and web container].

Java EE容器是一种应用程序服务器解决方案，它支持Web容器，EJB和其他Java EE API和服务。
Orace WebLogic服务器，GlassFish服务器，IBM WebSphere应用程序服务器，JBoss应用程序服务器和Caucho Resin是Java EE容器的示例

## Web容器

> Web container: Manages the execution of JSP page and servlet components for Java EE applications. Web components and their container run on the Java EE server.
管理Java EE应用程序的网页，Servlet和某些EJB组件的执行。 Web组件及其容器运行在Web服务器上，例如Jetty，tomcat。




# 对比表格

特性\web containers | Tomcat | WebLogic | WebSphere | JBOSS | Jetty
---------|----------|---------|---------|---------|---------
 1出品公司 | Apache 软件基金会的 Jakarta 项目中的一个核心项目，由 Apache、 Sun 和其他一些公司及个人共同开发而成。| 最早由WebLogic Inc.开发，后并入BEA公司，最终BEA公司又并入Oracle公司 | IBM 的集成软件平台 | 2006 年,Jboss 公司被 Redhat 公司收购
 2介绍 | Jsp和Servlet容器。由于有了 Sun 的参与和支持，最新的 S ervlet 和 JSP 规范总是能在 Tomcat 中得到体现， Tomcat 5 支持最新的 Servlet 2. 4 和 JSP 2.0 规范。因为 Tomcat 技术先进、性能稳定，而且免费，因而深受 Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的 Web 应用服务器。 | application server 确切的说是一个基于 j2ee 架构的中间件。用于开发、集成、部署和管理大型分布式 Web 应用、网络应用和数据库应用的 Java 应用服务器。将 Java 的动态功能和 Java Enterprise 标准的安全性引入大型网络应用的开发、集成、部署和管理之中。 | 它包含了编写、运行和监视全天候的工 业强度的随需应变 Web 应用程序和跨平台、 跨产品解决方案所需要的整个中间件基 础设施，如服务器、服务和工具。 WebSphere 提供了可靠、灵活和健壮的集成软件。 | JBoss是一个基于J2EE的管理EJB的容器和服务器，支持 EJB 1.1、EJB 2.0 和 EJB3.0 的 规范。但 JBoss 核心服务不包括支持 servlet/JSP 的 WEB 容器，一般与 Tomcat 或 Jetty 绑定使用。（Jboss作为应用服务器，而Tomcat做web服务器。在 3.0 之前 JBoss 使用 Jetty 作为 Web Container，之后 JBoss 使用了 Tomcat 作为他的一个基础服务提供了 Web Container，所以 JBoss 4.x 里面你会看到一个 Embbed Tomcat。）| Servlet容器
 3价位 | 免费 | 收费-高 对于开发者，有免费使用一年的许可证。| 收费-高 | 免费（文档要收费）| 免费
 开源性 | 开源 | 不 | 不 | 开源 | 开源
 优点| 轻便小巧 |  |  | 热deploy | 开源
 技术支持 | `EJB` No | WebLogic 与 WebSphere 都是对业内多种标准的全面支持， 包括 EJB、 JSB、 JMS、 JDBC、XML 和 WML，使 Web 应用系统的实施更为简单，并且保护了投资，同时也使基于标准的解决方案的开发更加简便。| | `EJB` Yes JBoss 是实现了EJB 容器，再集成了 Tomcat
 扩展性 |  | 高扩展的架构体系闻名于业内，包括客户机连接的共享、资源 pooling 以及动态网页和 EJB 组件群集。|  |  
 应用范围 | 小型的轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试 JSP 程序的首选。 | 大型企业的大型项目| 大型企业的大型项目 | EJB 服务的中小型公司 
 商业服务和技术支持 | 无 | 有 | 有 | 无
 与数据库的紧密结合性 |  | 如果硬件成本比软件成本高许多，那不如使用 Weblogic/Websphere。 | 
 安全性 | 相对低 | 相对高 | 相对高 | 相对低



# 相关CVE

## Tomcat

- [CVE-2020-1938](https://www.freebuf.com/vuls/228108.html)
- [CVE-2019-0232 远程代码执行](https://github.com/pyn3rd/CVE-2019-0232/)
- [CVE-2017-12615 任意文件写入](https://mp.weixin.qq.com/s?__biz=MzI1NDg4MTIxMw==&mid=2247483659&idx=1&sn=c23b3a3b3b43d70999bdbe644e79f7e5)
- CVE-2013-2067
- CVE-2012-4534
- CVE-2012-4431
- CVE-2012-3546
- CVE-2012-3544
- CVE-2012-2733
- CVE-2011-3375
- CVE-2011-3190
- CVE-2008-2938

## Weblogic

- CVE-2019-2725
  - wls-wsat 反序列化远程代码执行
- CVE-2019-2658
- CVE-2019-2650
- CVE-2019-2649
- CVE-2019-2648
- CVE-2019-2647
- CVE-2019-2646
- CVE-2019-2645
- CVE-2019-2618
  - https://github.com/jas502n/cve-2019-2618/
- CVE-2019-2615
- CVE-2019-2568
- CVE-2018-3252
- CVE-2018-3248
- CVE-2018-3245
- CVE-2018-3201
- CVE-2018-3197
- CVE-2018-3191
  - https://github.com/voidfyoo/CVE-2018-3191
  - https://github.com/Libraggbond/CVE-2018-3191
- CVE-2018-2894
  - 任意文件上传
  - https://xz.aliyun.com/t/2458
- CVE-2018-2893
  - 反序列化
  - https://www.freebuf.com/vuls/178105.html
- CVE-2018-2628
  - https://mp.weixin.qq.com/s/nYY4zg2m2xsqT0GXa9pMGA
- CVE-2018-1258
- CVE-2017-10271
  - [XMLDecoder 反序列化漏洞](http://webcache.googleusercontent.com/search?q=cache%3AsH7j8TF8uOIJ%3Awww.freebuf.com%2Fvuls%2F160367.html)

- CVE-2017-3248
- CVE-2016-3510
- CVE-2015-4852
  - https://github.com/roo7break/serialator

## JBoss

- CVE-2017-12149
  - 反序列化漏洞
  - 访问 /invoker/readonly ，页面存在即有反序列化漏洞


# 参考文章

- [Web安全学习笔记5.3.5. 容器](https://websec.readthedocs.io/zh/latest/language/java/container.html)
- [Java EE容器与Web容器](https://www.codenong.com/17181292/)