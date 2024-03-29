---
title: Max size for HTTP POST servlet parameter content?
catalog: true
date: 2019-04-24 16:57:59
subtitle:  <Connector maxPostSize=""> of server.xml
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Max-size-for-HTTP-POST-servlet-parameter-content/header-server_xml.jpg"
tags:
- Servlet
- maxPostSize
- Tomcat
categories:
- TECH
- Network
- Servlet/HTTP
---

# Problem

Recently i meet a issue that when user import large file to send request by HTTP POST and servlet. The page redirect to welcome page.
Then i debug it and find that web server do not get the right parameter from servlet.

# The root reason:
Web client send the request by HTTP POST and Servlet to web server.
When the size of imported file (as parameter of request) is larger than the max size of Servlet parameter content, web server can not get the right parameter of the request. So it return to default welcome page.
So the root reason is max size of Servlet parameter limit the request. We should reset the servlet setting in tomcat.

# The workaround:

## 1 For JSP and Tomcat environment
### 1.1 maxPostSize
Tomcat Version | Attribute | Description
---------|----------|---------
 [Before 7.0.63](https://tomcat.apache.org/tomcat-5.5-doc/config/http.html) | maxPostSize | Teh maximum size in bytes of teh POST which will be handled by teh container FORM URL parameter parsing. Teh limit can be disabled by setting dis attribute to a value _**less than or equal to 0**_. If not specified, dis attribute is set to 2097152 (2 megabytes).
 [After and including 7.0.63](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) | maxPostSize | Teh maximum size in bytes of teh POST which will be handled by teh container FORM URL parameter parsing. Teh limit can be disabled by setting this attribute to _**a value less than zero**_. If not specified, this attribute is set to 2097152 (2 megabytes). Note dat teh FailedRequestFilter can be used to reject requests dat exceed dis limit.

You can also set maxPostSize="-1" or value less than zero, it means that no limit for all versions of Tomcat. 

### 1.2 Modify maxPostSize of server.xml
Edit Tomcat's server.xml which location is **_…/Your tomcat folder/conf/server.xml_**. 
In the _<Connector_ element, add an attribute _maxPostSize_ and set a larger value (in bytes) to increase the limit.
If there is timeout error, you should also add or increase the value of connectionTimeout.

#### 1.2.1 For http:

We modify connector for port="8080" in /Your tomcat folder/conf/server.xml
For example:
```xml
<Connector port="8080" protocol="HTTP/1.1"
    connectionTimeout="20000"
    redirectPort="8443"
    maxPostSize="10000000" />

```

```xml
<Connector port="8080" protocol="HTTP/1.1"
    connectionTimeout="20000"
    redirectPort="8443"
    maxPostSize="-1" />
```

#### 1.2.2 For https:
We should also modify connector for port="8443" /Your tomcat folder/conf/server.xml
```xml
<Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
    maxPostSize="-1" maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
    clientAuth="false" sslProtocol="TLS" keystoreFile="/opt/apache/tomcat/apache-tomcat-9.0.12/keystore" keystorePass="opsworkstomcat" server="Mxxxx" />
```

If you wonder why use port 8443 rather than 443, you can see my another blog: [Difference between HTTPS Port 443 and Port 8443](http://liyuankun.top/2019/06/11/Difference-between-HTTPS-Port-443-and-Port-8443/) and [Changing SSL port from 8443 to 443](http://liyuankun.top/2019/06/11/Changing-SSL-port-from-8443-to-443/)

## 2 For ASP and IIS environment
In order to accept larger files you have to change two sets of setting in you're web.config.
C:\Program Files (x86)\yourcompanydomain\Web ASPx\web.config or Your ASP Folder\web.config

### 2.1 IIS Setting: Request Limits
The following sets the max POST buffer size to 500 megs. The value is specified in bytes.
```xml
<configuration>
    <system.webServer>
        <security>
          <requestFiltering>
            <requestLimits maxAllowedContentLength="500000000" />
          </requestFiltering>
        </security>
    <system.webServer>
</configuration>  
```

### 2.2 ASP.NET Setting: httpRuntime maxRequestLength
ASP.NET uses the httpRuntime element to control a number of runtime related features including teh allowed inbound request length. Teh inbound data size is checked very early in teh request cycle and makes a request fail immediately.
```xml
<configuration>
    <system.web>
        <httpRuntime maxRequestLength="500000000"  executionTimeout="120" />
    </system.web>
<configuration>
```

### 2.3 What about Web Connection?
Starting with Web Connection 6.0 teh .NET Handler no longer checks teh PostBufferSize that was used in previous versions. This value is now deferred in favor of the values above.
Teh ISAPI module still has a PostBufferLimit setting in wc.ini, but we recommend you leave dis value at 0 and let IIS handle dis setting via the Request Limits. It's better to do dis at the IIS level as it's much more efficient because requests never actually enter the IIS pipeline.

## 3 Other ：Modify max-file-size and max-request-size of web.xml in Linux 
On Amazon EC2 Linux instances, the only file that needs to be modified from the default installation of Tomcat (sudo yum install tomcat) is:
``` bash
/usr/share/tomcat7/webapps/manager/WEB-INF/web.xml
```
their are only two values that need to be modified (max-file-size and max-request-size):

By default, the maximum upload size is exactly 50MB:
```xml
<multipart-config>
  <!-- 50MB max -->
  <max-file-size>52428800</max-file-size>
  <max-request-size>52428800</max-request-size>
  <file-size-threshold>0</file-size-threshold>
</multipart-config>
```

Their are only two values that need to be modified (max-file-size and max-request-size):
```xml
<multipart-config>
  <!-- 100MB max -->
  <max-file-size>104857600</max-file-size>
  <max-request-size>104857600</max-request-size>
  <file-size-threshold>0</file-size-threshold>
</multipart-config>
```


# Reference Links:

[Is there a max size for POST parameter content?](https://stackoverflow.com/questions/2943477/is-there-a-max-size-for-post-parameter-content)

[Setting IIS and ASP.NET POST Size Request Limits](https://webconnection.west-wind.com/docs/_4lp0zgm9d.htm#aspnet-setting-httpruntime-maxrequestlength)

[关于Tomcat的maxPostSize属性的配置需要注意的问题](https://blog.csdn.net/erlian1992/article/details/80209947)

[HttpRequest maximum allowable size in tomcat?](https://stackoverflow.com/questions/2947683/httprequest-maximum-allowable-size-in-tomcat)

