---
title: Install node.js and nvm
catalog: true
date: 2022-04-05 19:16:29
subtitle:
header-img:
tags:
- Command line
- node.js
categories:
- TECH
- node.js
---

## Node.js 版本介绍

## 通过`nvm`安装Node.js

安装 Node.js 的最佳方式是使用 nvm（`Node Version Manager`）。

### 安装`nvm`

cURL:

```bash
curl https://raw.github.com/creationix/nvm/master/install.sh | sh
```

Wget:

```bash
wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
```

或者您也可以下载 安装程序 来安装。

```bash
brew install nvm
```

### command not found: nvm

```bash
nvm
zsh: command not found: nvm
```

#### 解决方法1

There might be some problems installing nvm in new mac, caused by the shell is not bash by default, check if it is bash with command

```bash
echo $0
```

§ if it is not run command

```bash
chsh -s /bin/bash
```

And then reopen the terminal

#### 解决方法2

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

### `nvm`安装 Node.js

1. Install Node.js

安装完成后，重启终端并执行下列命令即可安装 Node.js。

```bash
nvm install stable
```

```bash
nvm install v10.15.0
```

2. Upgrade(<https://codeforgeek.com/update-node-using-npm/>)

```bash
sudo npm install -g n
npm -v
sudo n 10.15.0
```
