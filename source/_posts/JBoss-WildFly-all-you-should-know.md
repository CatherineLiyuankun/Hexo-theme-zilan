---
title: JBoss/WildFly all you should know
catalog: true
date: 2021-12-15 17:14:45
subtitle:
header-img:
tags: 
- WebContainer
- JBoss
categories:
- TECH
- BackEnd
- Java
---

## JBoss EAP Vs JBoss AS Vs Wildfly

> JBoss EAP is the JBoss Enterprise Application Platform that is a subscription based JavaEE application server; this is a Red Hat product; whereas Wildfly is the community product.

作为JBoss的新手，会发现很多不同的术语-JBoss EAP，JBoss Server，Wildfly，Jboss Web，以及许多不是最新的或针对较旧版本的文档。

`JBoss AS` (JBoss Application Server) 是开源社区版本，发布比较频繁。最新版本是7.1.1，2012年3月发布的，已经不再维护。官方推荐升级到WildFly或者JBoss EAP。所以从JBoss AS 7.1.1之后分出了两个方向，分别是WildFly和JBoss EAP。
网址：<https://jbossas.jboss.org/downloads>
> JBoss AS 7，前后发布了 7.0.0, 7.0.1, 7.0.2, 7.1.0, 7.1.1, 7.1.2, 7.1.3, 7.2.0，其中 7.1.1 比较经典，7.2.0 是 JBoss EAP 6.1 的基础，但7.1.2, 7.1.3, 7.2.0 只是源代码打了 Tag，并没提供开放下载。这个社区项目最终将成为JBoss EAP。

`WildFly`只是`JBoss AS`的新名称，从 8 开始，新的 JBoss AS 正式有一个名字，叫 `WildFly`. RedHat公司称，新名称WildFly反映了服务器“非常灵活、轻量、不羁、自由”的特性。WildFly 8，WildFly 9，WildFly 10以及可能的其他WildFly版本都是通往最终称为JBoss EAP 7的里程碑, 它们都实现了Java EE 7。尽管它们是该路线上的里程碑并且不受支持，但某些发行版实际上相当稳定并且可以投入生产(但由于不支持，因此后果自负)。

> 改名后的首个版本为WildFly 8，将接棒JBoss AS 7。RedHat公司表示，新版本不仅是名称上的变化，还带来了如下改进：
>
> - 启动超快
> - 模块化设计
> - 非常轻量，内存占用非常少
> - 更优雅的配置、管理方式
> - 严格遵守Java EE7和OSGi规范

`JBoss EAP`(JBoss Enterprise Application Platform)在开源版本上构建的企业版本，目前Redhat 已经将 JBoss EAP 放在 JBoss.org 开放下载，开发人无需注册 Redhat （之前是必须有 Redhat.com 账号才能下载 JBoss EAP）。是Red Hat生产和支持的Java EE应用程序服务器的名称。

`JBoss Web`是Red Hat在JBoss EAP 6及更早版本中使用的基于Tomcat的Servlet容器的名称。从EAP 7开始(因此已经在WildFly 8,9,10中使用)，它将被称为`Undertow`的新Servlet容器/ http引擎取代。

## JBoss和Tomcat区别

- Tomcat 是 JSP/Servlet 容器

- JBoss 是 JEE 容器，JEE 包括JSP/Servlet，JMS， EJB，JAX-WS，JAX-RS，CDI等等
  - JBoss是一个管理EJB的容器和服务器，但JBoss核心服务不包括支持servlet/JSP的WEB容器，一般与Tomcat或Jetty绑定使用。servlet容器还是tomcat，所以JBoss是基于tomcat的。
  - JBoss无最大访问限制、可伸缩性。

## JBoss 下载部署

### JBoss 下载

[JBOSS EAP](https://developers.redhat.com/products/eap/download/)
[WildFly](https://www.wildfly.org/downloads/) JBoss AS 从版本 8.0 开始改名为 WildFly
[JBoss AS](https://jbossas.jboss.org/downloads)

### JBoss 部署

[JBOSS EAP 7.2 官方文档](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.2/html-single/configuration_guide/index)

[JBOSS EAP实战(1)](https://blog.csdn.net/lifetragedy/article/details/51371794)
[Jboss eap7.1 配置部署入门](https://www.jianshu.com/p/4baaf549436b)

## JBoss EAP的详细介绍（目录结构等）

目录 | 功能
---------|----------
 appclient/ | 包含应用程序客户容器的配置细节。
 bin/ | 包含 Red Hat 企业版 Linux 和微软 Windows 上 JBoss EAP 的启动脚本。
 docs/ | 许可证文件、schema 和示例。
 domain/ | 配置文件、部署内容和 JBoss EAP 6 以受管域运行时使用的可写入区域。
 modules/| 当有服务请求时 JBoss EAP 6 动态加载的模块。
 standalone/ | 配置文件、部署内容和 JBoss EAP 6 以独立服务器运行时使用的可写入区域。
 welcome-content/ | 包含默认安装里 8080 端口上的 Welcome 应用程序使用的内容。
 jboss-modules.jar | 加载模块的引导机制。

### domain/ 里的目录

名称 | 目的
---------|----------
configuration/ | 用于受管域的配置文件。这些文件是通过管理控制台和 CLI 进行修改的，不能直接进行编辑。
data/ | 关于已部署服务的信息。服务是用管理控制台或管理 CLI，而不是通过部署扫描器来部署的。因此，请不要手动在这个目录里放入文件。
log/ | 包含运行在本地实例上的主机和进程控制器的运行时日志文件。
servers/ | 包含某个域里的每个服务器实例的 data/、log/ 和 tmp/ 目录，其中包含的数据和顶层的 domain/
tmp/ | 包含临时数据，如针对受管域检验本地用户的管理 CLI 使用的共享密钥机制相关的文件。

### standalone/ 里的目录

名称 | 目的
---------|----------
configuration/ | 用于独立服务器的配置文件。这些文件是通过管理控制台和 CLI 进行修改的，不能直接进行编辑。
deployments/ | 关于已部署服务的信息。独立服务器包含一个部署扫描器，您可以在这个目录里放入要部署的归档文件。然而，我们推荐的方法是用管理控制台或管理 CLI 来管理部署。
lib/ | 附属于独立服务器模式的外部库。默认为空。
tmp/ | 包含临时数据，如针对服务器检验本地用户的管理 CLI 使用的共享密钥机制相关的文件。

### JBoss EAP 的功能

功能 | 描述
符合 Java EE 7 规范 | 通过 Java Enterprise Edition 7 full 和 web profile 认证。
受管域 | 集中管理多个服务器实例和物理主机，而独立服务器只允许运行单个服务器实例。可以按服务器组来管理配置、部署、套接字绑定、模块、扩展和系统属性。集中并简化应用程序安全性（包括安全域）管理。
管理控制台和管理 CLI | 新的域或独立服务器管理界面。管理 CLI 还包括批处理模式，可以编写脚本并自动执行管理任务。不建议直接编辑 JBoss EAP XML 配置文件。
简化的目录结构 | 模块目录包含所有应用服务器模块。域和独立目录分别包含用于域和独立部署的构件与配置文件。
模块化类加载机制 | 模块可以按需加载和卸载。这样可提高性能、实现更好的安全性并缩短启动和重启时间。
简化数据源管理 | 数据库驱动程序可像其他服务一样进行部署。另外，可以使用管理控制台和管理 CLI 来创建和管理数据源。

#### 子系统

许多对部署到 JBoss EAP 的应用程序开放的 API 和功能组成子系统。管理员可根据应用程序的目标，配置这些子系统来提供不同的特性。例如，如果应用程序需要数据库，则可在 datasources 子系统中配置数据源，在应用程序部署到 JBoss EAP 服务器或域之后，就可以访问该数据源。

#### 高可用性

JBoss EAP 中的高可用性 (HA) 是指多个 JBoss EAP 实例一起协同运行，使应用程序能更好地抵抗流量、服务器负载和服务器故障等方面的波动。HA 结合了可扩展性、负载均衡和容错性等概念。

#### 操作模式

除了向应用程序提供相关功能和 API 之外，JBoss EAP 还具备强大的管理功能。JBoss EAP 采用不同的操作模式启动，可以分别提供不同的管理功能。JBoss EAP 提供独立服务器操作模式用于管理分散的实例，提供受管域操作模式用于从单个控制点管理一组实例。

# 参考文章

- [初识JBoss EAP](https://blog.csdn.net/zmh458/article/details/79405871)
