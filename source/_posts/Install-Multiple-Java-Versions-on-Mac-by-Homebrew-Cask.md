---
title: Install Multiple Java Versions on Mac by Homebrew Cask
catalog: true
date: 2021-06-06 16:33:20
subtitle: 多个Java版本切换和安装 jenv
header-img:
tags:
- MAC
- Command line
- Java
categories:
- TECH
- Tools
- Environment setup
---

# 安装[Homebrew Cask](https://github.com/Homebrew/homebrew-cask)

## [brew install 和 brew cask install 的区别](https://zhuanlan.zhihu.com/p/138059447)

## [homebrew](https://brew.sh/) 官网

Install [Homebrew Cask](https://github.com/Homebrew/homebrew-cask) first if you haven’t:

```bash
brew update
# 老版本 brew tap caskroom/cask
# 会报错：
# Error: caskroom/cask was moved. Tap homebrew/cask instead.
# 2021 新版本：
brew tap homebrew/cask 
# 老版本： brew install brew-cask
brew install homebrew/cask
```

安装brew-cask-completion：

```bash
brew install brew-cask-completion
```

But before doing that, let’s check if we already have JDK 7 installed by Homebrew Cask:

```bash
# 老版本 brew tap caskroom/versions
# Error: caskroom/versions was moved. Tap homebrew/cask-versions instead.
brew tap homebrew/cask-versions
# 老版本：brew cask info java7
brew info --cask java7
```

## [How to Use Homebrew Cask](https://github.com/Homebrew/homebrew-cask/blob/master/USAGE.md)

# 安装Java

## 安装最新版本Java

Otherwise, install Latest Version of Java Using Brew:

```bash
# 老版本 brew cask install java
# 会报错：
# Error: Unknown command: cask
brew install --cask java
```

## 安装指定版本Java

### [New]安装openjdk11 or openjdk17

[Homebrew 安装openjdk11](https://formulae.brew.sh/formula/openjdk@11)
MACOS 升级M1芯片后，最好更新下jdk版本，运行效率更高。
另外因为`CVE-2022-21476 vulnerability resolution` (aka Java upgrade to jdk-11.0.15+10) ，openjdk11最好更新到`11.0.15+10`.

1. Install

```bash
$ brew install openjdk@11

==> openjdk@11
For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk

openjdk@11 is keg-only, which means it was not symlinked into /opt/homebrew,
because this is an alternate version of another formula.

If you need to have openjdk@11 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openjdk@11/bin:$PATH"' >> ~/.zshrc

For compilers to find openjdk@11 you may need to set:
  export CPPFLAGS="-I/opt/homebrew/opt/openjdk@11/include"
```

```bash
brew install openjdk@17

==> Pouring openjdk@17--17.0.16.arm64_sequoia.bottle.tar.gz
==> Caveats
For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /opt/homebrew/opt/openjdk@17/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-17.jdk

openjdk@17 is keg-only, which means it was not symlinked into /opt/homebrew,
because this is an alternate version of another formula.

If you need to have openjdk@17 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openjdk@17/bin:$PATH"' >> ~/.zshrc

For compilers to find openjdk@17 you may need to set:
  export CPPFLAGS="-I/opt/homebrew/opt/openjdk@17/include"
==> Summary
🍺  /opt/homebrew/Cellar/openjdk@17/17.0.16: 636 files, 305MB
==> Running `brew cleanup openjdk@17`...
Disable this behaviour by setting `HOMEBREW_NO_INSTALL_CLEANUP=1`.
Hide these hints with `HOMEBREW_NO_ENV_HINTS=1` (see `man brew`).
```

Add `export PATH="/opt/homebrew/opt/openjdk@17/bin:$PATH"` to ~/.zshrc

```bash
source ~/.zshrc

java -version  # 应显示 openjdk 17.x.x
    openjdk version "17.0.16" 2025-07-15
    OpenJDK Runtime Environment Homebrew (build 17.0.16+0)
    OpenJDK 64-Bit Server VM Homebrew (build 17.0.16+0, mixed mode, sharing)

javac -version # 应显示 javac 17.x.x[1,2](@ref)
    javac 17.0.16
```

2. Set jdk for jenv

```bash
$ where java
/opt/homebrew/opt/openjdk@17/bin/java
/Users/yuanli/.jenv/shims/java
/opt/homebrew/opt/openjdk@11/bin/java

$ jenv versions
openjdk64-11.0.11

$ jenv add /opt/homebrew/opt/openjdk@11
$ jenv add /opt/homebrew/opt/openjdk@17

$ jenv versions
* openjdk64-11.0.28 (set by /Users/yuanli/.jenv/version)
  openjdk64-17.0.16

$ jenv enable-plugin export

# set default jdk version
$ jenv global openjdk64-17.0.16

$ jenv versions
  openjdk64-11.0.28
* openjdk64-17.0.16 (set by /Users/yuanli/.jenv/version)
```

3. (Optional)删除旧的jdk

```bash
sudo rm -rf /Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home/bin/java

jenv remove openjdk64-11.0.11

jenv versions

```

1. Set jdk for IDE

#### ERROR in terminal

`~/.bash_profile` 或是`~/.zprofile` `~/.zshrc`里面配置了`JAVA_HOME`

```bash
 export JAVA_HOME="/opt/homebrew/opt/openjdk@17" 
```

- 报错：

```bash
ERROR: JAVA_HOME is set to an invalid directory: /opt/homebrew/opt/openjdk@11
```

- [解决方法1](https://stackoverflow.com/a/6588410)：

1. `JAVA_HOME` 修改为： `export JAVA_HOME="$(/usr/libexec/java_home)"`
2. Run `sudo ln -sfn /usr/local/opt/openjdk/libexec/openjdk.jdk`

推荐解决方法2： quite IDE

```bash
ps aux | grep gradle
yuanli           53967   0.3  0.0 408628368   1616 s004  S+    3:20PM   0:00.00 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn --exclude-dir=.idea --exclude-dir=.tox gradle
kill 53967
```

```bash
jenv enable-plugin export
jenv local openjdk64-17.0.16

echo $JAVA_HOME
```

### other

Install Specific Versions of Java (Java8, Java11, Java13)
To install previous or specific versions of JDKs, you can get them from AdoptOpenJDK:

```bash
brew tap adoptopenjdk/openjdk

brew install --cask adoptopenjdk8
brew install --cask adoptopenjdk11
brew install --cask adoptopenjdk13
```

# Java版本切换

Now it is time to install jEnv:

```bash
brew install jenv

To activate jenv, add the following to your shell profile e.g. ~/.profile, ~/.bash_profile
or ~/.zshrc:
  export PATH="$HOME/.jenv/bin:$PATH"
  eval "$(jenv init -)"
==> Summary
🍺  /opt/homebrew/Cellar/jenv/0.5.9: 91 files, 100.9KB
==> Running `brew cleanup jenv`...
Disable this behaviour by setting `HOMEBREW_NO_INSTALL_CLEANUP=1`.
Hide these hints with `HOMEBREW_NO_ENV_HINTS=1` (see `man brew`).
```

jEnv doesn’t install JDKs, so we have to tell jEnv where to look for them. Type these commands to register JDKs in jEnv (replace the minor and patch versions with yours):

```bash
$ where java
/usr/bin/java
/Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home/bin/java
/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home/bin/java
```

```bash
# 添加jdk变量到jenv，只有添加过jenv versions 才能显示出来
$ jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home
$ jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home
$ jenv add /usr
```

After that, run this command to list all registered JDKs:

```bash
$ jenv versions

openjdk64-1.8.0.292
openjdk64-11.0.11
```

```bash
# 移除jdk变量
jenv remove openjdk64-11.0.11
```

The version with an asterisk is the active version.
In my case, I need to keep JDK 7 as my default version, so I set the global version to 1.7:

```bash
jenv global oracle64-1.7.0.79
```

And in my project, I set the local JDK version to 1.8:

```bash
cd <my project>
jenv local oracle64-1.8.0.66
```

The above command will create a .java-version file at project root. Its content is the version I just picked for this project:

```bash
oracle64-1.8.0.66
```

## `jenv enable-plugin export`

用 jenv 管理 JDK 版本的小伙伴，可以通过这个命令让 `jenv` 在切版本的时候顺便把 `JAVA_HOME` 设置正确，运行一次即可。
`jenv enable-plugin export`

# Reference

- [Install Multiple Java Versions on Mac](http://davidcai.github.io/blog/posts/install-multiple-jdk-on-mac/)
- [Homebrew cask option not recognized?](https://stackoverflow.com/questions/30413621/homebrew-cask-option-not-recognized)
- [How to Use Brew to Install Java on Mac](https://devqa.io/brew-install-java/)
