---
title: JBoss/WildFly all you should know
catalog: true
date: 2021-12-15 17:14:45
subtitle: JBoss/WildFly 常见概念/版本/下载/部署总结
header-img:
tags: 
- WebContainer
- JBoss
categories:
- TECH
- BackEnd
- Java
---

# [Web-containers-web容器总结](../Web-containers-web容器总结.html)

# JBoss 基本术语/概念

## JBoss EAP Vs JBoss AS Vs Wildfly

> JBoss EAP is the JBoss Enterprise Application Platform that is a subscription based JavaEE application server; this is a Red Hat product; whereas Wildfly is the community product.

作为JBoss的新手，会发现很多不同的术语-JBoss EAP，JBoss Server，Wildfly，Jboss Web，以及许多不是最新的或针对较旧版本的文档。按时间线来看的话：

`JBoss AS` (JBoss Application Server) 是开源社区早期版本，发布比较频繁。内部封装的容器是基于Tomcat的升级版。最新版本是7.1.1，2012年3月发布的，已经不再维护。官方推荐升级到WildFly或者JBoss EAP。所以从JBoss AS 7.1.1之后分出了两个方向，分别是WildFly和JBoss EAP。
网址：<https://jbossas.jboss.org/downloads>
> JBoss AS 7，前后发布了 7.0.0, 7.0.1, 7.0.2, 7.1.0, 7.1.1, 7.1.2, 7.1.3, 7.2.0，其中 7.1.1 比较经典，7.2.0 是 JBoss EAP.1 的基础，但7.1.2, 7.1.3, 7.2.0 只是源代码打了 Tag，并没提供开放下载。这个社区项目最终将成为JBoss EAP。

`WildFly`只是`JBoss AS`的新名称，从 8 开始，新的 JBoss AS 正式有一个名字，叫 `WildFly`. 内部封装的容器是Undertow。RedHat公司称，新名称WildFly反映了服务器“非常灵活、轻量、不羁、自由”的特性。WildFly 8，WildFly 9，WildFly 10以及可能的其他WildFly版本都是通往最终称为JBoss EAP 7的里程碑, 它们都实现了Java EE 7。尽管它们是该路线上的里程碑并且不受支持，但某些发行版实际上相当稳定并且可以投入生产(但由于不支持，因此后果自负)。

> 改名后的首个版本为WildFly 8，将接棒JBoss AS 7。RedHat公司表示，新版本不仅是名称上的变化，还带来了如下改进：
>
> - 启动超快
> - 模块化设计
> - 非常轻量，内存占用非常少
> - 更优雅的配置、管理方式
> - 严格遵守Java EE7和OSGi规范

`JBoss EAP`(JBoss Enterprise Application Platform)在开源版本上构建的企业版本，会将社区版中验证过的，成熟的技术引入该版本，支持周期长。6的版本以Jboss AS7为基础；7的版本以Wildfly为基础。目前Redhat 已经将 JBoss EAP 放在 JBoss.org 开放下载，开发人无需注册 Redhat （之前是必须有 Redhat.com 账号才能下载 JBoss EAP）。是Red Hat生产和支持的Java EE应用程序服务器的名称。

`JBoss Web`是Red Hat在JBoss EAP及更早版本中使用的基于Tomcat的Servlet容器的名称。从EAP 7开始(因此已经在WildFly 8,9,10中使用)，它将被称为`Undertow`的新Servlet容器/ http引擎取代。

`Undertow` Jboss自主研发的Servlet容器。

## JBoss和Tomcat区别

- Tomcat 是 JSP/Servlet 容器

- JBoss 是 JEE 容器，JEE 包括JSP/Servlet，JMS， EJB，JAX-WS，JAX-RS，CDI等等
  - JBoss是一个管理EJB的容器和服务器，但JBoss核心服务不包括支持servlet/JSP的WEB容器，一般与Tomcat或Jetty绑定使用。servlet容器还是tomcat，所以JBoss是基于tomcat的。从EAP 7开始(因此已经在WildFly 8,9,10中使用)，tomcat被称为`Undertow`的新Servlet容器/ http引擎取代。
  - JBoss无最大访问限制、可伸缩性。

# JBoss 下载配置

## JBoss 下载

[JBOSS EAP developers](https://developers.redhat.com/products/eap/download/)
[JBOSS EAP](https://access.redhat.com/jbossnetwork/restricted/listSoftware.html?product=appplatform&downloadType=distributions)
[WildFly](https://www.wildfly.org/downloads/) JBoss AS 从版本 8.0 开始改名为 WildFly
[JBoss AS](https://jbossas.jboss.org/downloads)

## JBoss 官方文档

这里只列出部分常用配置文档：

[JBOSS EAP 官方文档目录](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4)

- [JBOSS EAP 官方文档-Getting Started Guide](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html/getting_started_guide/index)
  - [JBoss EAP 官方文档-1.1. Downloading and installing JBoss EAP](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html/getting_started_guide/administering_jboss_eap#assembly-download-and-install-jboss-eap_default)
  - [JBoss EAP 官方文档-1.2. Starting and stopping JBoss EAP](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html/getting_started_guide/administering_jboss_eap#assembly-start-stop-jboss-eap_default)
  - [JBoss EAP 官方文档-1.3 JBoss EAP Management](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html/getting_started_guide/administering_jboss_eap#jboss_eap_management)
  - [JBoss EAP 官方文档-1.4 Network and port configuration JBoss EAP](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html/getting_started_guide/administering_jboss_eap#assembly-network-port-configurations_default)
- [JBOSS EAP 官方文档-INSTALLATION GUIDE](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html-single/installation_guide/index)
- [JBOSS EAP 官方文档-Configuration Guide](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html-single/configuration_guide/index)
  - [JBOSS EAP 官方文档-Deploying Applications](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.2/html/configuration_guide/deploying_applications)

## JBoss 常用配置

[JBoss EAP 官方文档-1.3.3 Configuration Files](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html/getting_started_guide/administering_jboss_eap#configuration_files)

目录 | 功能
---------|----------
 EAP_HOME/bin/init.d/jboss-eap-rhel.sh | startup script 启动脚本
 EAP_HOME/bin/init.d/jboss-eap.conf | configuration file 配置文件, 最少配置下`JBOSS_HOME`和`JBOSS_USER`。 1 默认使用默认配置文件 `standalone.xml`启动 a standalone JBoss EAP server。2 If you want the service to start JBoss EAP as a managed domain, add `JBOSS_MODE=domain` to jboss-eap.conf. To specify custom [domain configuration files](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.2/html-single/installation_guide/index#:~:text=To%20specify%20custom-,domain%20configuration%20files,-%2C%20add%20JBOSS_DOMAIN_CONFIG%3DDOMAIN_CONFIG_FILE), add `JBOSS_DOMAIN_CONFIG=DOMAIN_CONFIG_FILE.xml` and `JBOSS_HOST_CONFIG=HOST_CONFIG_FILE.xml`. By default, JBoss EAP uses `domain.xml` and `host.xml` as the domain configuration files.
 EAP_HOME/bin/standalone.sh |启动server脚本， standalone mode（单机模式）。 `standalone.bat` for windows users. 默认配置文件 `EAP_HOME/standalone/configuration/standalone.xml`， 也可以指定读取其他配置文件，命令是`./standalone.sh --server-config=standalone-custom.xml`。或者使用备份历史文件：`$ EAP_HOME/bin/standalone.sh --server-config=standalone_xml_history/snapshot/20151022-133109702standalone.xml`
 EAP_HOME/bin/domain.sh |启动server脚本， domain mode（集群模式）. `domain.bat` for windows users. 默认配置文件  `EAP_HOME/domain/configuration/domain.xml` and `EAP_HOME/domain/configuration/host.xml`
 EAP_HOME/bin/jboss-cli.sh | 命令行管理工具, 通过命令行实现部署卸载应用、配置系统设置和执行管理任务的功能。使用该工具修改系统配置时，最终也会作用到standalone.xml中。虽然官方文档不建议直接改xml而是推荐CLI，但我更喜欢直接改。 The management command-line interface (CLI) is a command-line administration tool for JBoss EAP.
 EAP_HOME/bin/jboss-cli.sh --connect command=:shutdown | stop server脚本. 1 `EAP_HOME/bin/jboss-cli.sh --connect` 2 `shutdown`
 EAP_HOME/bin/add-user.sh | Adding a Management User， For Windows Server, use the `EAP_HOME\bin\add-user.bat` script. `a` to add a management user, `b` adds a user to the ApplicationRealm, which is used for applications and provides no particular permissions.
 EAP_HOME/bin/standalone.conf | Jboss启动的配置，在文件中加入 `JAVA_HOME="/path/jdk"`，可以指定使用的jdk，而不必依赖于系统默认的java环境变量。在文件中加入 `LANG=Zh_CN.GB18030`，可以设定语言环境为中文. 修改`JAVA_OPTS`，可以设置JVM的启动参数.
 <http://localhost:9990/console/index.html> | Management Console，管理控制台。是jboss提供的web管理系统，所有的操作均可通过jboss-cli实现。默认用户名密码admin/admin, 可以通过 `EAP_HOME/bin/add-user.sh` 选择`a` management user, 进行添加或修改。
`EAP_HOME/standalone/configuration/standalone.xml` | standalone mode（单机模式）的默认配置文件。It contains all information about the server, including subsystems, networking, deployments, socket bindings, and other configurable details. It does not provide the subsystems necessary for messaging or high availability.
`EAP_HOME/domain/configuration/domain.xml` | domain mode（集群模式）默认配置文件，Only the domain master reads this file. This file contains the configurations for all of the profiles (default, ha, full, full-ha, load-balancer).
`EAP_HOME/domain/configuration/host.xml` | This file includes configuration details specific to a physical host in a managed domain, such as network interfaces, socket bindings, the name of the host, and other host-specific details. The host.xml file includes all of the features of both host-master.xml and host-slave.xml, which are described below.也可以指定读取其他配置文件，命令是`$ EAP_HOME/bin/domain.sh --host-config=host-master.xml`

## JBoss EAP 网络和端口配置

[JBoss EAP 官方文档-1.4 Network and port configuration JBoss EAP](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html/getting_started_guide/administering_jboss_eap#assembly-network-port-configurations_default)

## JBoss EAP的详细介绍（目录结构等）

目录 | 功能
---------|----------
 appclient/ | 包含应用程序客户容器的配置细节。
 bin/ | 包含 Red Hat 企业版 Linux 和微软 Windows 上 JBoss EAP 的启动脚本。
 docs/ | 许可证文件、schema 和示例。
 domain/ | 配置文件、部署内容和 JBoss EAP 以受管域运行时使用的可写入区域。
 modules/| 当有服务请求时 JBoss EAP 动态加载的模块。custom modules自定义的modules可以放在这里。
 standalone/ | 配置文件、部署内容和 JBoss EAP 以独立服务器运行时使用的可写入区域。
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

# Web Application的部署

[JBOSS EAP 官方文档-Deploying Applications](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.2/html/configuration_guide/deploying_applications)
官方文档中有6种方法，这里只列出常用的方法，可根据生产/开发环境来选择合适的方式。

> For administrators, the `management console` and the `management CLI` offer ideal graphical and command-line interfaces to manage application deployment in a production environment.

对于管理员, `management console` 和 `management CLI` 提供理想的图形和命令行界面来管理生产环境中的应用程序部署.

> For developers, the range of application deployment testing options include a configurable file system `deployment scanner`, the `HTTP API`, an `IDE` such as Red Hat CodeReady Studio, and `Maven`.

对于开发人员，应用程序部署测试选项的范围包括可配置文件系统`deployment scanner`、`HTTP API`、`IDE`（例如 Red Hat CodeReady Studio）和`Maven`。


部署方式 | Management CLI | Management Console | Deployment Scanner | Exploded | HTTP API | Maven
---------|----------|---------|----------|---------|----------|---------
 环境 | 生产环境(推荐) | 生产环境 | 开发环境 | 开发环境 | 开发环境 | 开发环境
 需要上传文件到deployments文件夹下？ | No | No | YES | 根据部署方式

## 使用Management CLI部署【官方推荐：生产环境】

[JBOSS EAP 官方文档-Deploying Applications](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.2/html/configuration_guide/deploying_applications#deploying_apps_using_cli)

<!-- 增加属性scan-enabled="false" -->
此模式是官方推荐的生产环境部署应用方式，无需将应用上传至deployments文件夹下。首先保证test-application.war在服务器上，假设其路径为/path/to/test-application.war。

1. 启动服务器，并使用`./jboss-cli.sh --connect`命令进入命令行管理界面。
2. 执行命令`deployment deploy-file /path/to/test-application.war`部署应用。
3. 取消部署时，在命令行管理界面执行 `deployment undeploy test-application.war`。
应用的数据会在`EAP_HOME/standalone/data/content`下，并且standalone.xml最下方会出现deployments标签，显示已经部署的应用。

- Disable某个application：
Disable 不会把部署内容移除，只是暂时不启动。

```bash
deployment disable test-application.war
```

```bash
deployment disable-all
```

- Enable某个application：
  
```bash
deployment enable test-application.war
```

```bash
deployment enable-all
```

- 列出deploy信息
  
```bash
deployment info
```

## 使用Management Console部署【生产环境】

Management Console，管理控制台。是jboss提供的web管理系统，所有的操作均可通过jboss-cli实现。默认用户名密码admin/admin, 可以通过 `EAP_HOME/bin/add-user.sh` 选择`a` management user, 进行添加或修改。
[<http://localhost:9990/console/index.html>](http://localhost:9990/console/index.html)

### 选择Deployments Tab

![选择Deployments Tab](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/JBoss-WildFly-all-you-should-know/console.png)

### 点击+，可以选择

![选择Deployments Tab](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/JBoss-WildFly-all-you-should-know/console-deployment1.png)

- Upload a deployment

  Upload an application that will be copied to the server’s content repository and managed by JBoss EAP.

- Adding an unmanaged deployment

  Specify the location of a deployment. This deployment will not be copied to the server’s content repository and will not be managed by JBoss EAP.

- Creating an empty deployment

  Create an empty, exploded deployment. You can add files to the deployment after it has been created.

### 选中application，可以选择

![选择Deployments Tab](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/JBoss-WildFly-all-you-should-know/console-deployment2.png)

- Undeploy an Application
  Select the deployment and choose the `Remove` option to undeploy the application. This undeploys the deployment and removes it from the content repository.

- Disable an Application
  Select the deployment and choose the `Disable` option to disable the application. This undeploys the deployment, but does not remove it from the content repository.

- Replace an Application
  Select the deployment and choose the `Replace` option. Select the new version of the deployment, which must have the same name as the original, and click Finish. This undeploys and removes the original version of the deployment, and then deploys the new version.

## 使用Deployment Scanner部署【适合开发环境】

### Deploy an Application

在默认配置下，将war包拷贝至`EAP_HOME/standalone/deployments/`，服务器会在启动时，每5秒间隔检查deployments下的文件变化，部署应用。
此外，Deployment Scanner不应与其他部署方法结合使用。
> Deployment Scanner仅在 JBoss EAP 作为standalone服务器运行时可用。

```bash
cp /path/to/test-application.war EAP_HOME/standalone/deployments/
```

如果启用了自动部署，则会自动选取、部署此文件，并创建`.dodeploy`标记文件。
如果未启用自动部署，则需要手动添加`.dodeploy` 标记文件以触发部署。
JBOSS在启动时会把这个文件名自动改成`test-application.war.deploying`。
如果布署成功，该文件名会被自动改名成：`test-application.war.deployed`
如果布署失败，该文件名会被自动改名成：`test-application.war.failed`

```bash
touch EAP_HOME/standalone/deployments/test-application.war.dodeploy
```

### UnDeploy

删除`.dodeploy` 标记文件。如果启用自动部署，删除`.war`文件也会触发undeploy。

### ReDeploy

手动添加 `.dodeploy` 标记文件, 或者把之前的标记文件从`.deployed`或者`.failed`重命名为`.dodeploy`。

```bash
touch EAP_HOME/standalone/deployments/test-application.war.dodeploy
```


## 解压式部署【适合开发环境】

解压式部署比war包部署的好处是，允许更改解压的应用程序的内容，而无需部署应用程序的新版本。
在 JBoss EAP 7.1 之前，只能通过操作文件系统上的文件来管理解压部署。从 JBoss EAP 7.1 开始，可以使用管理界面management console管理解压式部署。

### 手动部署

在 JBoss EAP 7.1 之前，只能通过操作文件系统上的文件来管理解压部署。和Deployment Scanner部署比较相像， 唯一区别是需要手动解压war文件，并重命名。

1. 解压test-application.war包到test-application文件夹，重命名test-application文件夹为`test-application.war`
2. 拷贝解压好的war包拷贝至`EAP_HOME/standalone/deployments/`。

```bash
cp /path/to/test-application.war EAP_HOME/standalone/deployments/
```

3. 创建`.dodeploy`标记文件。 如果未启用自动部署，则需要手动添加`.dodeploy` 标记文件以触发部署。

```bash
touch EAP_HOME/standalone/deployments/test-application.war.dodeploy
```
4. UnDeploy和ReDeploy的方法也和Deployment Scanner部署一样。

### management console部署

从 JBoss EAP 7.1 开始，可以使用管理界面management console管理解压式部署。
>对部署中的静态文件（例如 JavaScript 和 CSS 文件）的更新会立即生效。 对其他文件（例如 Java 类）的更改可能需要重新部署应用程序才能使更改生效。

1. 选择Deployments Tab, 点击+, 选择`Creating an empty deployment`
2. 填写文件夹路径`/path/to/test-application.war`

### Management CLI部署

#### 创建空的部署：

```bash
/deployment=DEPLOYMENT_NAME.war:add(content=[{empty=true}])
```

#### Explode an Existing Archive Deployment

```bash
/deployment=ARCHIVE_DEPLOYMENT_NAME.ear:explode
```

# 参考文章

- [初识JBoss EAP](https://blog.csdn.net/zmh458/article/details/79405871)
- [JBOSS EAP实战(1)](https://blog.csdn.net/lifetragedy/article/details/51371794)
- [Jboss eap7.1 配置部署入门](https://www.jianshu.com/p/4baaf549436b)
