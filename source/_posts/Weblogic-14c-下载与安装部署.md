---
title: Weblogic 14c 下载与安装部署
catalog: true
date: 2021-07-26 15:39:56
subtitle:
tags: WebContainer
categories:
- TECH
- BackEnd
- Java
---

# Preface
 [官方安装文档](https://docs.oracle.com/en/middleware/fusion-middleware/weblogic-server/index.html)

## step 1 确保已正确安装JDK

JDK安装：  [Install Multiple Java Versions on Mac by Homebrew Cask](../Install-Multiple-Java-Versions-on-Mac-by-Homebrew-Cask.html)
> Verify that a certified JDK already exists on your system; the installer requires a certified JDK. See [Oracle Fusion Middleware Supported System Configurations](https://docs.oracle.com/pls/topic/lookup?ctx=en/middleware/standalone/weblogic-server/14.1.1.0/wlsig&id=fmwsysreq). To download the JDK, see [About JDK Requirements for an Oracle Fusion Middleware Installation](https://docs.oracle.com/pls/topic/lookup?ctx=en/middleware/standalone/weblogic-server/14.1.1.0/wlsig&id=ASINS-GUID-8AA3A3BA-27F0-43B8-8F62-1B2DC8C5DBB1).

```bash
java -version
```

## step 2 下载安装

 [官方下载地址1](https://www.oracle.com/middleware/technologies/fusionmiddleware-downloads.html)
 [官方下载地址2](https://www.oracle.com/middleware/technologies/weblogic-server-installers-downloads.html)

选择 “Generic Installer”，下载`fmw_14.1.1.0.0_wls_lite_Disk1_1of1.zip`.

解压`fmw_14.1.1.0.0_wls_lite_Disk1_1of1.zip`文件，得到安装包`fmw_14.1.1.0.0_wls_lite_generic.jar`文件。

安装：
```bash
java -jar fmw_14.1.1.0.0_wls_lite_generic.jar
```

## step 3 部署配置

出现图形化安装界面，大多数都选择默认。

创建管理账户和域：
![创建管理账户和域](https://img-blog.csdnimg.cn/20200415100633131.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzM4MTEyNDc1,size_16,color_FFFFFF,t_70)

域创建结束后就可以启动weblogic了。

## step 4 启动/关闭weblogic

### start 关闭weblogic

Window 系统则使用./startWebLogic.cmd
```bash
cd <weblogicFoder>/user_projects/domains/base_domain
./startWebLogic.sh
```

浏览器登陆[http://localhost:7001/console/](http://localhost:7001/console/)进入weblogic控制台。

### stop 关闭weblogic

> [Shutting Down Instances of WebLogic Server](https://docs.oracle.com/en/middleware/standalone/weblogic-server/14.1.1.0/start/overview.html#GUID-9AD29794-B51A-4DFC-9DBD-6D1EAD9AECFE)

Window 系统则使用./stopWebLogic.cmd

```bash
cd <weblogicFoder>/user_projects/domains/base_domain/bin
./stopWebLogic.sh
```

## 配置文件
```bash
cd <weblogicFoder>/user_projects/domains/base_domain/config
vim config.xml
```



## 参考文章
- [WebLogic使用总结(一)——WebLogic安装](https://www.cnblogs.com/xdp-gacl/p/4140683.html)
- [Weblogic运维使用手册](https://cloud.tencent.com/developer/article/1501376)

