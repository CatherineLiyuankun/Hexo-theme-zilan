---
title: Install/Upgrade node.js
catalog: true
date: 2022-04-05 19:16:29
subtitle: By n, nvm, brew
header-img:
tags:
- Command line
- node.js
categories:
- TECH
- node.js
---

## Node.js 版本介绍

[Node.js官网下载](https://nodejs.org/en/)的时候会看到`LTS`和`Current`两个版本可以选项：

- `Current`：一个新版本会先进入`Current`版本，将持续六个月的时间。
  - 只有我们非生产环境需要尝试新版本的一些特性时，才会选择。
- `LTS（Long Term Support）`： “长期维护版”，通常生产环境为了保证稳定性，选择这个版本。 它分为两个阶段：
  - `Active LTS`： 正积极维护和升级的版本，持续18个月，到期后进入`Maintenance LTS`
  - `Maintenance LTS`： 维护的LTS版本，持续18个月，到期后进入`EOL`版本
  - `EOL（End of life）`，正式退出历史舞台。

> 主版本的 Node.js 进入`Current`版本将持续六个月的时间，在此期间库作者可以对其进行支持。 六个月之后，奇数版本（诸如 9、11 等）将变为不支持状态，只有偶数版本（诸如 10、12 等）变成 活跃 `LTS` 状态，并且准备投入使用。 `LTS` 发布版的状态是“长期维护版”，这意味着重大的 Bug 将在后续的 30 个月内持续得到不断地修复。 上线应该仅使用 活跃 `LTS` 或者是 维护 `LTS` 版。

根据官网的描述，我们可以看出`Current`和`LTS`是随着时间相互转变的。

- `Current`偶数版 6 months ---> `Active LTS` 18 months ---> `Maintenance LTS` 18 months  ---> `EOL`
- `Current`奇数版 6 months ---> `unsupported`

![Long Term Support (LTS) schedule](https://raw.githubusercontent.com/nodejs/Release/master/schedule.svg?sanitize=true)

### node.js 相关链接

- [Node.js Chagelog](https://github.com/nodejs/node/blob/master/doc/changelogs/CHANGELOG_V16.md#16.14.2)
- [Node.js News](https://nodejs.org/tr/blog/)
- [Long Term Support (LTS) schedule](https://nodejs.org/en/about/releases/)

## Node.js 安装方法

`node -v` 先查看是否安装node.js 和安装的版本。

## 通过`nvm`安装Node.js

安装 Node.js 的最佳方式是使用 nvm（`Node Version Manager`）。

- [nvm](https://nodejs.org/zh-cn/download/package-manager/#nvm)适用OS: Mac/Linux
- [nvm-windows](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fcoreybutler%2Fnvm-windows%2Freleases)则是其在windows平台的一个替代方案，两者有联系，但是各自独立的项目。
  - [Install NodeJS on Windows](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-windows)

### 安装`nvm`

可以下载 安装程序 来安装。

```bash
brew install nvm
```

cURL:

```bash
curl https://raw.github.com/creationix/nvm/master/install.sh | sh
```

或者Wget:

```bash
wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
```

### 配置nvm

安装完成后，根据安装完的提示不要忘记
1. 创建nvm 工作路径： `mkdir ~/.nv`
2. 配置nvm的路径到~/.profile or ~/.zshrc， 然后`source ~/.zshrc`

```bash
You should create NVM's working directory if it doesn't exist:
  mkdir ~/.nvm

Add the following to your shell profile e.g. ~/.profile or ~/.zshrc:
  export NVM_DIR="$HOME/.nvm"
  [ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \. "/opt/homebrew/opt/nvm/nvm.sh"  # This loads nvm
  [ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion

You can set $NVM_DIR to any location, but leaving it unchanged from
/opt/homebrew/Cellar/nvm/0.40.3 will destroy any nvm-installed Node installations
upon upgrade/reinstall.
```

重启终端并执行下列命令即可安装 Node.js。

### 安装问题1：command not found: nvm

```bash
nvm
zsh: command not found: nvm
```

#### 解决方法1

忘记配置nvm

如果用的是`zsh`, 而不是`bash`. 将`.bashrc`中关于`nvm`的配置copy到`.zshrc`里边。
将`.bashrc`中的copy到`~.zshrc`下就可以啦。

```bash
export NVM_DIR="/usr/local/Cellar/nvm/0.38.0"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" #This loads nvm bash_completion
```

然后再

```bash
source ~/.zshrc
```

#### 解决方法2

There might be some problems installing nvm in new mac, caused by the shell is not bash by default, check if it is bash with command

```bash
echo $0
```

§ if it is not run command

```bash
chsh -s /bin/bash
```

And then reopen the terminal



### `nvm`安装 Node.js

1. Install Node.js

    ```bash
    # 列出远程服务器上所有的可用版本
    nvm ls-remote

    ...
       v16.12.0
       v16.13.0   (LTS: Gallium)
       v16.13.1   (LTS: Gallium)
       v16.13.2   (LTS: Gallium)
       v16.14.0   (LTS: Gallium)
       v16.14.1   (LTS: Gallium)
       v16.14.2   (LTS: Gallium)
    -> v16.15.0   (Latest LTS: Gallium)
        v17.0.0
    ...
    ```

    ```bash
    # 安装latest available version
    nvm install node

    # 安装最新的LTS版本
    nvm install --lts

    # 安装16.14.x 中最高（最新）的版本
    nvm install 16.14

    # 安装指定版本
    nvm install 10.15.0
    ```

### `nvm` 切换版本

```bash
# 使用latest available version
nvm use node

# 安装stable版本
nvm install stable

# 使用最新的LTS版本
nvm use --lts

# 安装16.14.x 中最高（最新）的版本
nvm install 16.14

# 安装指定版本
nvm install 10.15.0
```

### `nvm`列出已安装版本

```bash
nvm list
       v10.15.3
       v12.22.9
       v14.19.1
       v16.14.2
->     v16.15.0
default -> v10.15.3
iojs -> N/A (default)
unstable -> N/A (default)
node -> stable (-> v16.15.0) (default)
stable -> 16.15 (-> v16.15.0) (default)
lts/* -> lts/gallium (-> v16.15.0)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.24.1 (-> N/A)
lts/erbium -> v12.22.12 (-> N/A)
lts/fermium -> v14.19.2 (-> N/A)
lts/gallium -> v16.15.0
```

### `nvm` 设置default版本

```bash
# Set default node version as 8.1.0
  nvm alias default 8.1.0      
# Always default to the latest available node version on a shell         
  nvm alias default node                
```

### `nvm` 其他命令

```bash
# Run app.js using node 6.10.3
  nvm run 6.10.3 app.js
# Run `node app.js` with the PATH pointing to node 4.8.3
  nvm exec 4.8.3 node app.js
# 卸载指定版本 Uninstall a version
  nvm uninstall <version>
```

## Node.js 升级

### 安装node.js 新版本

- via npm

```bash
npm cache clean -f
npm install -g n
n 16.15.0
```

- via nvm

```bash
nvm install v16.15.0
nvm use v16.15.0
```

- via [brew](https://formulae.brew.sh/formula/node@16)

```bash
brew install node@16
```

### Remove node_modules folder (optional)

### Reinstall the dependencies

by `yarn install` or `npm install`

## 参考文章

- [Node.js怎么选版本？](https://juejin.cn/post/7001401390983544840)
- [使用 nvm 管理不同版本的 node 与 npm](https://www.runoob.com/w3cnote/nvm-manager-node-versions.html)
- [How to switch Node.js versions with NVM](https://blog.logrocket.com/how-switch-node-js-versions-nvm/)

- [Install NodeJS on Windows](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-windows)
- [How to Update Node to Any Version Using Npm](https://codeforgeek.com/update-node-using-npm/)
- [How to Update Node.js to Latest Version {Linux, Windows, and macOS}](https://phoenixnap.com/kb/update-node-js-version)
- [Upgrading Node.js to latest version](https://stackoverflow.com/questions/10075990/upgrading-node-js-to-latest-version)
