---
title: Docker
catalog: true
date: 2021-12-22 22:10:03
subtitle:
header-img:
tags: 
- Cloud
- container
categories:
- TECH
- container
- Docker
---


# Docker 基本概念

镜像（`Image`）：Docker 镜像理解为一个包含了必要的操作系统（通常只有OS文件系统和文件系统对象）。是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。镜像不包含任何动态数据，其内容在构建之后也不会被改变。镜像由一些松耦合的只读镜像层组成。多个镜像间可以并且确实会共享镜像层（节约空间提升性能）。

容器（`Container`）：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的`类` 和 `实例` 一样，镜像是静态的定义，容器是镜像运行时的实体， 一个镜像可以运行为多个容器。容器可以被创建、启动、停止、删除、暂停等。可以停止某个容器的运行，并从中创建新的镜像。镜像可以理解为一种构建时（build-time）结构，容器为运行时（run-time）结构。一旦容器从镜像启动后，二者变成了相互依赖的关系，并且在镜像上启动的容器全部停止之前，镜像是无法被删除的。

仓库（`Repository`）：镜像仓库（Image Registry）类似Git的远程仓库，集中存放镜像文件。Docker客户端的镜像仓库服务可配置，默认使用的镜像仓库是Docker Hub. 镜像仓库服务： 镜像仓库 = 1: N 镜像仓库: 镜像 = 1：N。`Docker Hub`分为`官方仓库（Official Repository）`和`非官方仓库（Unofficial Repository）`.

- `官方仓库（Official Repository）`: 镜像由官方审查过，及时更新，高质量，安全，完善文档，最佳实践。
- `非官方仓库（Unofficial Repository）`：非官方，不保证上述特性。

三者关系：
![三者关系](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Docker/docker1.png)

## 容器Vs虚拟机

容器优势：

- `OS Tax/VM Tas`: 虚拟机操作系统OS本身有额外开销。
- 容器启动快： 容器不是完整操作系统，容器内部不需要内核，也就没有定位、解压以及初始化的过程。

虚拟化：

- 硬件虚拟化（`Hardware Virtualization`）: Hypervisor将硬件物理资源划分为虚拟资源。
- 操作系统虚拟化（`Hardware Virtualization`）: 容器将系统资源划分为虚拟资源。

## 容器（`Container`）

### 容器随着运行应用的退出而终止

- `docker container run -it ubuntu /bin/bash` Linux容器在Bash Shell退出后终止.
- `docker container run -it microsoft- /powershell:nanoserver pwsh.exe` Windows容器在PowerShell进程退出后终止.

杀死容器中的主进程，容器也会被杀死：

```bash
$ docker container run -it ubuntu:latest /bin/bash
# 查看容器内进程
root@3027eb644874:/# ps -elf
# 退出容器
  # Ctrl + PQ 退出容器时保持容器运行
  # 从这个 stdin 中 exit()，会导致容器的停止
Ctrl + PQ

$ docker exec -it 3027eb644874 bash
root@3027eb644874:/#
# docker exec创建了新的Bash进程并且连接到容器，所以现在输入exit()并不会导致容器种植，因为原Bash进程还在运行中
```

### 重启策略

`--restart [重启策略]`: 设置重启策略，例如`docker container run -it  --restart always ubuntu:latest /bin/bash`

重启策略 | always | unless-stopped | on-failed
---------|----------|---------|---------
策略  | if not 容器被明确停止（例如`docker container stop`）， 重启处于停止状态的容器 | if not 容器被明确停止（例如`docker container stop`）， 重启处于停止状态的容器 | if 退出容器&&返回值!=0， 重启容器
daemon/Docker重启时  | 停止的容器也被重启 | 停止的容器不！！！重启 | stopped的容器也被重启

```bash
# 无重启策略
$ docker container run -it  ubuntu:latest /bin/bash
root@733b80d556f7:/# exit
exit
# 退出进程时，容器终止
 ✘ $ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

```bash
# 重启策略： always
$ docker container run -it  --restart always ubuntu:latest /bin/bash
root@b077521d228e:/# exit
exit
# 退出进程时，容器终止，又自动重启（STATUS 启动时间 UP 7 seconds < CREATED 创建时间13 seconds ago）
$ docker container ls
CONTAINER ID   IMAGE           COMMAND       CREATED          STATUS         PORTS     NAMES
b077521d228e   ubuntu:latest   "/bin/bash"   13 seconds ago   Up 7 seconds             wonderful_yalow
# 主动stop后，不自动重启
$ docker container stop b077521d228e
b077521d228e
 $ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
# 重启Docker，容器重启
$ systemctl restart docker
$ docker container ls
CONTAINER ID   IMAGE           COMMAND       CREATED          STATUS         PORTS     NAMES
807b900b28f9   ubuntu:latest   "/bin/bash"   12 seconds ago   Up 3 seconds             epic_noether
```

```bash
# 重启策略： always 和 unless-stopped
$ docker container run -d --name always \
  --restart always \
  ubuntu:latest /bin/bash
$ docker container run -d --name unless-stopped \
  --restart unless-stopped \
  ubuntu:latest /bin/bash

$ docker container ls
CONTAINER ID   IMAGE           COMMAND       CREATED          STATUS         PORTS     NAMES
807b900b28f9   ubuntu:latest   "/bin/bash"   12 seconds ago   Up 3 seconds             always
9afe62536be6   ubuntu:latest   "/bin/bash"   12 seconds ago   Up 17 seconds            unless-stopped

# 主动stop后，不自动重启
$ docker container stop always unless-stopped
b077521d228e
 $ docker container ls -a
CONTAINER ID   IMAGE           COMMAND       CREATED          STATUS                   PORTS     NAMES
807b900b28f9   ubuntu:latest   "/bin/bash"   12 seconds ago   Exited (137) 3 seconds ago         always
9afe62536be6   ubuntu:latest   "/bin/bash"   12 seconds ago   Exited (137) 3 seconds ago         unless-stopped

# 重启Docker，always容器重启
$ systemctl restart docker
$ docker container ls -a
CONTAINER ID   IMAGE           COMMAND       CREATED          STATUS                   PORTS     NAMES
807b900b28f9   ubuntu:latest   "/bin/bash"   12 seconds ago   Exited (137) 2 minutes ago         always
9afe62536be6   ubuntu:latest   "/bin/bash"   12 seconds ago   Up 17 seconds                      unless-stopped
```

### Docker 端口

Docker默认非TLS网络端口为2375，默认TLS网络端口为2376。

### Docker 持久化

stop 或 pause容器并不会导致容器销毁，或者内部存储的数据丢失。

## 镜像（`Image`）

`悬虚镜像`: Repository:Tag 为<none>:<none>. 因为构建了一个新的镜像，为该新镜像打了一个已经存在的Tag，Docker发现已经有镜像包含相同的Tag，会移除旧镜像上面的Tag，将Tag标在新镜像上， 旧镜像就成了悬虚镜像。

## 相关资料

`Moby`: [Docker开源项目](https://github.com/moby)，2017年正式命名为Moby(白鲸)， Github上的docker/docker库转移到[moby/moby](https://github.com/moby)。Apache协议2.0， Golang编写。
`Docker引擎`: `企业版（Enterprise Edition, EE）`， `社区版（Community Edition, CE）`， 每季度 企业版EE和社区版 CE都会发布一个稳定版本。 CE社区版又分为`稳定版（stable）` `抢先版（Edge）`，抢先版（Edge）每月发布。
`版本号`： 从2017年第一季度开始，YY.MM-xx格式， 例如18.06.0-ce（18年6月社区版）
`开放容器计划（The Open Container Initiative， OCI）`： 对容器基础架构中的基础组件进行标准化的管理委员会（在Linux基金会支持下运作）。 OCI已发布规范：`镜像规范`(类比铁轨尺寸)， `运行时规范`(类比相关属性).

# Docker安装

 方式 | Docker for Windows(DfW) | Docker for Mac(DfM) | Linux | Windows Server2016
---------|----------|---------|----------|---------
 类别 | 桌面安装 | 桌面安装 | 服务器安装 | 服务器安装
 要求 | 1 64位 2 Windows10 3 启用Hyper-v和容器特性 | MAC | Linux | Windows Server2016
 生产环境 | No，社区CE版本应用 | No，社区CE版本应用 | CE或EE |
 版本 | 稳定版（stable） 抢先版（Edge） |  |  |
 运行内核 | 默认Hyper-v虚拟机中的轻量级Linux，可切换为Native Windows 原生内核 | 轻量级Linux VM | Linux | Windows

Docker for Mac(DfM) 是一个流畅，简单并且稳定版的boot2docker.

# Docker 常用命令

![Docker 常用命令](https://ask.qcloudimg.com/http-save/yehe-7565276/6lldlbgfhn.png?imageView2/2/w/1620)

## 服务

### 查看Docker系统信息（信息比`docker version`更多）

```bash
docker system info
```

### 查看Docker版本信息，包含Client和Server信息

如果Server中包含错误码，表示

1. 或者当前用户没有权限访问。 解决方法： 确认用户是否属于本地Docker UNIX组，若不是，`usermod -aG docker <user>`来添加，退出并重新登录Shell
2. Docker daemon可能没有运行。 解决方法：检查Docker daemon状态 `service docker status`

```bash
$ docker version
Client:
 Cloud integration: v1.0.22
 Version:           20.10.11
 API version:       1.41
 Go version:        go1.16.10
 Git commit:        dea9396
 Built:             Thu Nov 18 00:36:09 2021
 OS/Arch:           darwin/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.11
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.9
  Git commit:       847da18
  Built:            Thu Nov 18 00:35:39 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.12
  GitCommit:        7b11cfaabd73bb80907dd23182b9347b4245eb5d
 runc:
  Version:          1.0.2
  GitCommit:        v1.0.2-0-g52b36a2
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

#### 查看docker简要信息

```bash
$ docker -v
Docker version 20.10.11, build dea9396
```

```bash
docker --version
```

### 检查Docker daemon状态

```bash
# 使用System V在Linux系统中执行命令
$ service docker status
docker start/running, process 29393
```

```bash
# 使用SystemD 在Linux系统中执行命令
$ systemctl is-active docker
active
```

```bash
# 在Windows Server 2016 的PowerShell窗口中执行命令
> Get-Service docker
Status    Name     DisplayName
------    ----     -----------
Running   Docker   docker
```

### 启动Docker服务

```bash
# 使用SystemD 在Linux系统中执行命令
systemctl start docker
```

```bash
# 使用System V在Linux系统中执行命令
service docker start
```

### 重启Docker服务

```bash
# 使用SystemD 在Linux系统中执行命令
systemctl restart docker
```

```bash
# 使用System V在Linux系统中执行命令
service docker restart
```

### 关闭docker服务

```bash
# 使用SystemD 在Linux系统中执行命令
systemctl stop docker
```

```bash
# 使用System V在Linux系统中执行命令
service docker stop
```

### 设置开机启动

```bash
# 使用SystemD 在Linux系统中执行命令
systemctl enable docker
```

## 镜像

### 镜像仓库

Docker Hub 等镜像仓库上有大量的高质量的镜像可以用，可以从仓库获取镜像。

- 检索镜像
  - `docker search 关键字` 搜索NAME字段含有关键字符串的仓库
    - `docker search 关键字 --filter "is-official=true"` 过滤是否是官方镜像
    - `docker search 关键字 --filter "is-automated=true"`过滤是否是自动创建的镜像
    - `docker search 关键字 --limit 行数` 默认只返回25行结果，--limit 可设置返回行数，最多为100行
- 拉取镜像
  - `docker image pull <option> <DockerHub用户名组织名/repository>:<tag>`
    - 从官方Ubuntu库 拉取 标签为latest的镜像 `docker image pull ubuntu:latest`
    - 默认标签为latest `docker image pull ubuntu`
    - 注意！！！latest不一定代表是最新镜像
    - 多个镜像可有相同tag
    - 从官方Mongo库 拉取 标签为3.3.11的镜像`docker image pull mongo:3.3.11`
    - 从Docker Hub 账号nigelpoulton为命名空间的tu-demon库下拉取v2标签的镜像`docker image pull nigelpoulton/tu-demo:v2`
    - 从第三方镜像仓库服务获取，需在前面加上第三方镜像仓库服务DNS名称 例如Google容器镜像仓库（GCR） `docker image pull gcr.io/nigelpoulton/tu-demo:v2`
  - `docker image pull -a <DockerHub用户名组织名/repository>` `-a` 拉取全部镜像
  - `docker image pull <repository><Digest>``docker image pull ubuntu@sha256:c0537...7cj32rg42454` 通过镜像摘要Digest 拉取镜像，镜像摘要Digest是基于内容散列值（Content Hash），可区分出两个tag相同的镜像

### 镜像管理

- 列出镜像
  - `docker image ls`
    - `docker image ls -q` 获取全部镜像ID
    - `docker image ls --filter` 过滤
      - dangling: true(返回悬虚镜像) false (返回非悬虚镜像) `docker image ls --filter dangling=true`
      - before: 镜像名/ID 返回指定镜像之前被创建的全部镜像
      - since: 与before类似，返回指定镜像之后被创建的全部镜像
      - label: 根据标注（lable）的名称或者值，对镜像进行过滤。`docker image ls`输出中不显示lable
      - reference：`docker image ls --filter reference="*:latest"`
    - `docker image ls --format` 通过Go模板对输出内容格式化

      ```bash
      # 只返回镜像的Size属性
      docker image ls --format "{{.Size}}"
      ```

      ```bash
      # 只返回镜像的Repository: Tag: Size属性
      docker image ls --format "{{.Repository}}: {{.Tag}}: {{.Size}}"
      ```

    - `docker image ls --digest <image-name or image-id>` 显示镜像摘要（Image Digest，镜像内容散列值）
  - `docker images`

- 查看镜像分层，启动时默认应用
  - `docker image inspect <image-name or image-id>`
  
- 移除全部的`悬虚镜像`
  - `docker image prune`

- 删除镜像
  - 删除指定镜像`docker image rm <image-name or image-id>`
  - 删除本地所有镜像`docker image rm $(docker image ls -q) -f`

- 导出镜像
  - 将镜像保存为归档文件
  - docker save
- 导入镜像
  - docker load

## Dockerfile构建镜像

`容器化（Containerizing）`也叫`Docker化(Dockerizing)`： 将应用整合到容器中并运行起来的过程。
容器化过程：

1. 编写应用代码
2. 创建Dockerfile，其中包含当前应用描述、依赖以及如何运行这个应用。
3. 对Dockerfile执行`docker image build`命令
4. 等待Docker将应用程序构建到Docker镜像中。

### Dockerfile

`Dockerfile` 是一个文本格式的配置文件，用户可以使用 Dockerfile 来快速创建自定义的镜像。
`Dockerfile` 由一行行行命令语句组成，并且支持以＃开头的注释行.除注释行，每一行都是一条`指令（Instruction）`.
指令不区分大小写，通常采用大写。
`构建上下文（Build Context）`: 包含应用文件的目录。
通常将Dockerfile放在构建上下文的根目录下。

- Dockerfile常见指令
下面是Dockerfile中一些常见的指令：

  - `FROM`：指定`基础镜像（Base Image）`

  - `RUN`：执行命令

  - `COPY`：复制文件

  - `ADD`：更高级的复制文件

  - `CMD`：容器启动命令

  - `ENV`：设置环境变量

  - `EXPOSE`：暴露端口

其它的指令还有`ENTRYPOINT`、`ARG`、`VOLUME`、`WORKDIR`、`USER`、`HEALTHCHECK`、`ONBUILD`、`LABEL`等等。

以下是一个Dockerfile实例：

```bash
FROM java:8
LABEL maintainer="yuanli@gmail.com"
MAINTAINER "jinshw"<jinshw@qq.com>
ADD mapcharts-0.0.1-SNAPSHOT.jar mapcharts.jar
EXPOSE 8080
CMD java -jar mapcharts.jar
```

```Dockerfile
# 1 apine作为基础镜像， 是镜像的第一个镜像层layer
FROM apine
# 2 维护者为yuanli@gmail.com
LABEL maintainer="yuanli@gmail.com"
# 3 安装Node.js 和NPM，新建镜像层2
RUN apk add --update nodejs nodejs-npm
# 4 将应用代码拷贝到当前镜像中，新建镜像层3
COPY . /src
# 5 设置工作目录
WORKDIR /src
# 6 npm install会根据package.json文件用npm安装应用的依赖包，新建镜像层4
RUN npm install
# 7 应用需要通过TCP端口8080对外提供web服务
EXPOSE 8080
# 8 指定镜像的入口程序 
ENTRYPOINT ["node", "./app.js"]
```

#### 如何区分命令是否会新建镜像层？

- if 向镜像中添加新的文件或程序，then 新建镜像层。例如例子中的1，3，4，6
- if 只是告诉Docker如何完成构建或如何运行应用程序，then 增加镜像的元数据。例如例子中的2，5，7，8

### 构建命令

#### 镜像构建`docker image build`

镜像构建(在Dockerfile目录下运行)
`docker image build -t test:latest .`

- `.`表示使用当前目录作为构建上下文
- `--no-cache=true` 强制忽略缓存，不使用缓存构建镜像
- `--squash` 创建一个合并镜像

构建过程：

1. 运行临时容器  `---> Running in e60ddca785f`
2. 在该容器中运行Dockerfile中的指令
3. 将指令运行结果保存为一个新的镜像层 `---> cldddca785f`
4. 删除临时容器 `Removing intermediate container`

#### 查看构建镜像过程中执行的指令`docker image history`

`docker image history test:latest`

- 每行都对应Dockerfile中的一条指令
- SIZE列数值不为零的指令，表示新建镜像层

### 生产环境中的多阶段构建

Docker镜像应尽量小， 对生产环境来说，缩小到仅包含运行应用所必须的内容即可。

#### Docker镜像如何尽量小？

1. Dockerfile的写法： 每个RUN指令会新增一个镜像层，通过使用&&连接多个命令以及使用反斜杠（\）换行的方法，将多个命令煲仔一个RUN指令字中。
2. 利用构建缓存：

- 一旦有指令在缓存中未命中，后续整个构建过程将不再使用缓存。所以编写Dockerfile时，将容易放生变化的指令放在Dockerfile文件靠后的位置执行。
  - `docker image build`参数 `--no-cache=true` 强制忽略缓存，不使用缓存构建镜像
- `COPY``ADD`指令会检查复制到镜像中的内容自上一次构建之后是否发生了变化。`COPY . /src` 指令没有变化，但被复制的内容发生变化了。Docker会计算每个被复制文件的Checksum值，并与缓存镜像层中同一个文件的checksum对比，如果不匹配，则认为缓存无效并构建新的镜像层。

3. 合并镜像

镜像层数过多时，可以合并镜像。如果新建了一个镜像，想把它作为其他镜像的基础镜像时，这个基础镜像最后被合并为一层。
缺点： 合并的镜像无法共享镜像层，存储空间低效利用。而且push和pull操作的镜像体积更大。
`docker image build`参数 `--squash` 创建一个合并镜像

4. 使用no-install-recommends（Linux）

构建Linux镜像时，若使用APT包管理器，在执行`apt-get install`时增加`no-install-recommends`参数。确保APT只安装核心依赖，而不是推荐和建议的包， 减少不必要包的下载数量。

5. 不要安装MSI包（Windows）

构建Windows镜像时，尽量避免使用MSI包管理器。其对空间利用率不高，会大幅增加镜像体积。

#### 构建清理？

构建镜像过程中拉取的构建工具在构建完成后没有清理，就会留在镜像中移交至生产环境。

- 方法一：`建造者模式（Builder Pattern）`： 两个Dockerfile, 开发环境Dockerfile.dev(构建一个镜像并创建容器)， 生产环境Dockerfile.prod(从刚才创建的容器中将应用程序的部分复制过来). 需要编写额外的脚本才能串联起来。

- 方法二（更好，建议使用）：`多阶段构建(Multi-Stage Build)`： 一个Dockerfile， 包含多个`FROM`指令。每个`FROM`指令都是一个新的`构建阶段（Build Stage）`, 并且可以方便地复制之前构建阶段的构件。
  
## 容器

### 容器生命周期

- 查看容器

```bash
# 列出本机运行的容器
$ docker ps
$ docker container ls

# 列出本机所有的容器（包括停止和运行）
$ docker ps -a
$ docker container ls -a
```

- 启动：启动容器有两种方式，一种是基于镜像新建一个容器并启动，另外一个是将在终止状态（stopped）的容器重新启动。

```bash
# 新建并启动
$ docker container run <option> <image-name or image-id>:<tag> <app>

# 例子 -it 将Shell切换到容器终端
$ docker container run -it ubuntu:latest /bin/bash
root@3027eb644874:/#
# 3027eb644874是容器唯一ID的前12个字符

# 指定name为lyk 和 port映射为 host-port:container-port 8080:8080
$ docker container run -it --name lyk --publish 8080:8080 ubuntu:latest
```

`--restart always`: 设置重启策略，例如`docker container run -it  --restart always ubuntu:latest /bin/bash`

```bash
# 启动已终止容器
docker start <container-id or container-name>
```

- 退出容器
  - Ctrl + PQ 退出容器时保持容器运行
  - 从这个 stdin 中 exit，会导致容器的停止

- 进入容器
进入容器有两种方式：

```bash
# 如果从这个 stdin 中 exit，会导致容器的停止
docker attach <container-id or container-name>

# 交互式进入运行中的容器
docker exec <option> <container-name or container-ID> <command/app>
docker exec -it 4dbcc6555bc6 bash
```

进入容器通常使用第二种方式，`docker exec`后面跟的常见参数如下：
`－d, --detach` 在容器中后台执行命令；
`－i, --interactive=true I false` ：打开标准输入接受用户输入命令

- 暂停容器
  `docker container pause <container-id or container-name>`

- 停止容器

```bash
# 停止运行的容器
# 给容器进程发送SIGTTERM信号
docker stop <container-id or container-name>

# 杀死容器进程
docker  kill <container-id or container-name>
```

- 删除容器
  - `docker container rm <container-id or container-name>` 删除容器前，最好先`docker stop`容器，给容器中运行的应用/进程一个停止运行并清理残留数据的机会。# 给容器进程发送SIGKILL信号
  - `docker container rm $(docker container ls -aq) -f`。删除所有运行中的容器.
    - `-f`: force 强制执行， 运行状态的容器也会被删除。

- 重启容器
  - `docker restart <container-id or container-name>`

- 查看容器配置细节和运行时信息
  - `docker container inspect <container-name or container-id>`

### 导出和导入

- 导出容器

```bash
# 导出一个已经创建的容器到一个文件
docker export <container-id or container-name>
```

- 导入容器

```bash
# 导出的容器快照文件可以再导入为镜像
docker import <路径>
```

### 其它

- 查看日志

```bash
# 导出的容器快照文件可以再导入为镜像
docker logs <container-id or container-name>
```

这个命令有以下常用参数

```bash
 -f : 跟踪日志输出

--since :显示某个开始时间的所有日志

-t : 显示时间戳

--tail :仅列出最新N条容器日志
```

- 复制文件

```bash
# 从主机复制到容器
sudo docker cp host_path containerID:container_path 
# 从容器复制到主机
sudo docker cp containerID:container_path host_path
```

## 参数（Options）

### `docker container run` Options

`--help` 输出帮助信息，例如`docker run --help`
`－d, --detach` 在容器中后台执行命令；
`－i, --interactive` ：打开标准输入接受用户输入命令（Keep STDIN open even if not attached）
`-t, --tty`           Allocate a pseudo-TTY
`--restart always`: 设置重启策略，例如`docker container run -it --restart always ubuntu:latest /bin/bash`
`--name`: 设置容器名称
`-p, --publish`: 端口映射  主机端口：容器端口`docker container run -it --name lyk --publish 8080:8080 ubuntu:latest`

### `docker container rm` Options

`-f`: force 强制执行， 运行状态的容器也会被删除。

### `docker` Options

      --config string      Location of client config files (default "/Users/liyuankun/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var
                           and default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/Users/liyuankun/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/Users/liyuankun/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/Users/liyuankun/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            输出版本信息（Print version information and quit）

# 参考文章

- [一张脑图整理Docker常用命令](https://cloud.tencent.com/developer/article/1772136)
- 《深入浅出Docker》书
- [System-V 与 SystemD 区别](../System-V-与-SystemD-区别.html)
- [Docker概述-状态转换，命令](https://www.codenong.com/bc35c4295aaef7fb6b8c/)
