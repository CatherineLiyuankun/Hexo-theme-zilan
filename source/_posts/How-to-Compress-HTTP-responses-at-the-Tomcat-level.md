---
title: How to Compress HTTP responses at the Tomcat level
catalog: true
date: 2023-01-18 17:27:01
subtitle: Tomcat 内存与优化
header-img:
tags:
- Tomcat
categories:
- TECH
- BackEnd
- Java
---

## Tomcat应用程序服务器级别压缩选项

有时可能会注意到 HTTP 流量很高，有可能因为服务器正试图将大量数据返回给浏览器。 
在这种情况下，如果正在运行 Tomcat，则可以添加在应用程序服务器级别打开压缩的选项。 这样做会压缩 HTTP 响应，并且可以在性能上产生很大的差异，尤其是对于文本密集型的流量。 压缩文本的大小可以减少 90% 以上，如果您的未压缩数据以 MB 为单位，这会产生很大的不同。

1. 关闭 Tomcat 服务器。

2. 编辑在 Tomcat 的 `conf/server.xml` 文件。

3. 将以下属性添加到连接器（compression、compressMinSize、noCompressionUserAgents 和 compressibleMimeType），如下例所示：

```xml
<Connector 
    compressibleMimeType ="text/html,text/xml,text/css,text/javascript,application/javascript,application/json"
    compression="on"
    compressionMinSize="128"
    connectionTimeout="20000"
    noCompressionUserAgents="gozilla, traviata"
    port="8080"
    redirectPort="8443" 
    protocol="HTTP/1.1" />
```

注意MimeType 是改过名字的！！！否则启动中是有warining的

```log
[main] org.apache.catalina.startup.SetAllPropertiesRule.begin [SetAllPropertiesRule]{Server/Service/Connector} Setting property 'compressableMimeType' to 'text/html,text/xml,application/javascript,text/css,text/plain' did not find a matching property.
```

Tomcat version | MimeType | 
---------|----------|---------
[tomcat-5.5](https://tomcat.apache.org/tomcat-5.5-doc/config/http.html#Standard_Implementation) | compress`a`bleMimeType | C1
[tomcat-6.0](https://tomcat.apache.org/tomcat-6.0-doc/config/http.html#Standard_Implementation) | compress`a`bleMimeType | C1
[Tomcat 7.0 文档](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html#Standard_Implementation) | compress`i`bleMimeType | C2
[Tomcat 8.5 文档](https://tomcat.apache.org/tomcat-8.5-doc/config/http.html#Standard_Implementation) | compress`i`bleMimeType | C2
[Tomcat 9 文档](https://tomcat.apache.org/tomcat-9.0-doc/config/http.html) | compress`i`bleMimeType | C3
[Tomcat 10 文档](https://tomcat.apache.org/tomcat-10.0-doc/config/http.html) | compress`i`bleMimeType | C3

参数说明：

- org.apache.coyote.http11.Http11NioProtocol：调整工作模式为Nio
- maxThreads：最大线程数，默认150。增大值避免队列请求过多，导致响应缓慢。
- minSpareThreads：最小空闲线程数。
- acceptCount：当处理请求超过此值时，将后来请求放到队列中等待。
- disableUploadTimeout：禁用上传超时时间
- connectionTimeout：连接超时，单位毫秒，0代表不限制
- URIEncoding：URI地址编码使用UTF-8
- enableLookups：关闭dns解析，提高响应时间
- compression：启用压缩功能
- compressionMinSize：最小压缩大小，单位Byte
- compressibleMimeType ：压缩的文件类型
- noCompressionUserAgents: 该值是一个正则表达式（使用java.util.regex），与user-agent不应使用压缩的HTTP客户端的头部相匹配，因为这些客户端虽然宣称支持该功能，但实现方式却不一致。默认值是一个空字符串（禁用正则表达式匹配）。

4. 重启Tomcat服务器

---

注意：压缩compression与 `useSendFile` 配置不兼容。 有关详细信息，请参阅文档
- [Tomcat 9 文档](https://tomcat.apache.org/tomcat-9.0-doc/config/http.html)
- [Tomcat 8.5 文档](https://tomcat.apache.org/tomcat-8.5-doc/config/http.html#Standard_Implementation)

## Tomcat 内存与优化

### Tomcat 运行环境介绍

1. Tomcat 本身无法直接在计算机上运行，需要依赖硬件基础上的操作系统和Java虚拟机；
2. Java 程序启动时JVM都会分配一个初始内存和最大内存给这个应用；
3. 当应用程序用到最大内存的时刻，就会触发JVM做垃圾回收(GC)动作，释放被占用的内存；
4. 因此想要调整Java程序启动时的初始内存和最大内存，需要向JVM申请；
5. 如果初始内存大小设置过小，且此时初始化的应用对象过多，虚拟机就必须重复的加载内存来满足使用；
6. 基于以上原因，最好把初始内存大小(Xms)和最大内存(Xmx)设置成一样；
7. JVM上所有的对象都在"""堆区(heap)"""上分配内存(也有在"栈"上分配内存的)
8. 堆区的大小是可以动态扩展的，但"""堆"""的大小受限于系统使用的物理内存，当应用程序需要的内存超出"堆"的最大值时，JVM虚拟机就会抛出内存溢出异常，并且导致应用程序奔溃；
9. 基于以上原因，建议“堆”的大小设置成物理内存的80%

### Linux下的tomcat

需要找到`catalina.sh`，在`cygwin=false`的上面一行加上：

```bash
JAVA_OPTS="-Xms256m -Xmx512m -Xss1024K -XX:PermSize=128m -XX:MaxPermSize=256m"
```

### Windows下解压版的tomcat

要通过startup.bat启动tomcat才能加载配置

要添加在tomcat 的bin 下catalina.bat 里

rem Guess CATALINA_HOME if not defined
`set CURRENT_DIR=%cd%`后面添加,红色的为新添加的.

```bash
1 set JAVA_OPTS=-Xms256m -Xmx512m -XX:PermSize=128M -XX:MaxNewSize=256m -XX:MaxPermSize=256m -Djava.awt.headless=true
```

#### 情况二:安装版的Tomcat ,没有catalina.bat

安装版的Tomcat下没有catalina.bat

如果tomcat 6 注册成了windows服务，或者windows2003下用tomcat的安装版，在/bin/tomcat6w.exe里修改就可以了。

如果tomcat 5, windows服务执行的是bin\tomcat.exe.他读取注册表中的值,而不是catalina.bat的设置.
修改注册表HKEY_LOCAL_MACHINE\SOFTWARE\Apache Software Foundation\Tomcat Service Manager\Tomcat5\Parameters\JavaOptions
原值为
`-Dcatalina.home="C:\ApacheGroup\Tomcat 5.0"
-Djava.endorsed.dirs="C:\ApacheGroup\Tomcat 5.0\common\endorsed"
-Xrs`
加入 `-Xms300m -Xmx350m`
重起tomcat服务,设置生效

## 参考文章

- [How to Compress HTTP responses at the Tomcat level](https://community.jaspersoft.com/wiki/how-compress-http-responses-tomcat-level)
- [Apache Tomcat 8.5 安全配置与高并发优化](https://blog.csdn.net/bluetjs/article/details/77449535)
- [tomcat优化配置属性含义解释，转自官网 ](https://www.cnblogs.com/hardxuexi/articles/8817897.html)
- [Tomcat参数调优](https://juejin.cn/post/7085588638255284260)
  - https://juejin.cn/post/7067745436555182087

