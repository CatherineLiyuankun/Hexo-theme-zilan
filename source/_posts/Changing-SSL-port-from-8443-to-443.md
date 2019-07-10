---
title: Changing SSL port from 8443 to 443
catalog: true
date: 2019-06-11 15:12:44
subtitle:
header-img:
tags:
- Tomcat
categories:
- TECH
- Network
- Servlet/HTTP
---


My another blogs: [Difference between HTTPS Port 443 and Port 8443](../../../../2019/06/11/Difference-between-HTTPS-Port-443-and-Port-8443/) and [Changing SSL port from 8443 to 443](../../../../2019/06/11/Changing-SSL-port-from-8443-to-443/)

We modify connector under /Your tomcat folder/conf/server.xml

# modify non-SSL HTTP/1.1 Connector to 443 port

```xml
<Connector port="80" maxHttpHeaderSize="8192" 
    maxThreads="500" minSpareThreads="25" maxSpareThreads="75" 
    enableLookups="false"
    redirectPort="443" acceptCount="100" 
    connectionTimeout="20000" disableUploadTimeout="true" />
```

# modify SSL HTTP/1.1 Connector from 8443 to 443 port
In the server.xml file you will see a section defining the Tomcat connector for Port 8443. 

```xml
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true"
    maxThreads="150" scheme="https" secure="true"
    clientAuth="false" sslProtocol="TLS"
    keystoreFile="/usr/local/tomcat7/server.keystore"
    keystorePass="Envisi0n"/>
```

Add a copy of the connector definition for Port 8443 to the file and simply change the number 8443 in your copy to 443. 
```xml
<Connector port="443" protocol="HTTP/1.1" SSLEnabled="true"
    maxThreads="150" scheme="https" secure="true"
    clientAuth="false" sslProtocol="TLS"
    redirectPort="8443"
    keystoreFile="/usr/local/tomcat7/server.keystore"
    keystorePass="Envisi0n"/>
```
To disable the standard SSL port in the Apache Web server so that Tomcat can handle the connection, edit the httpd.conf file in the Apache conf directory and remove or comment out the lines that enable SSL in the Apache Web server. dis will be an actual SSL Port 443 definition block or an include statement that calls in another ssl.conf file. After changing the Apache Web server configuration and restarting the Web server, restart Tomcat. You should then be able to connect via https directly to Tomcat.



# modify AJP 1.3 Connector to other port

```xml
<Connector port="8009" 
enableLookups="false" redirectPort="443" protocol="AJP/1.3" />
```

Restart tomcat.


# Reference Links:

* [Changing SSL port from 8443 to 443](https://www.jamf.com/jamf-nation/discussions/7210/changing-ssl-port-from-8443-to-443)
* [A Simple Step-By-Step Guide To Apache Tomcat SSL Configuration](https://www.mulesoft.com/tcat/tomcat-ssl)
* [Tomcat from 8443 to 443](https://stackoverflow.com/questions/25743718/tomcat-from-8443-to-443)