---
title: Install Multiple Java Versions on Mac by Homebrew Cask
catalog: true
date: 2021-06-06 16:33:20
subtitle: 多个Java版本切换和安装
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

### [New]安装openjdk11

[Homebrew 安装openjdk11](https://formulae.brew.sh/formula/openjdk@11)
MACOS 升级M1芯片后，最好更新下jdk版本，运行效率更高。
另外因为`CVE-2022-21476 vulnerability resolution` (aka Java upgrade to jdk-11.0.15+10) ，openjdk11最好更新到`11.0.15+10`.

1. Install

```bash
$ brew install openjdk@11

For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk

openjdk@11 is keg-only, which means it was not symlinked into /opt/homebrew,
because this is an alternate version of another formula.

If you need to have openjdk@11 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openjdk@11/bin:$PATH"' >> ~/.zshrc

For compilers to find openjdk@11 you may need to set:
  export CPPFLAGS="-I/opt/homebrew/opt/openjdk@11/include"
```

2. Set jdk for jenv

```bash
$ where java
/opt/homebrew/opt/openjdk@11/bin/java
/Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home

$ jenv versions
openjdk64-11.0.11

$ jenv add /opt/homebrew/opt/openjdk@11

$ jenv versions
* openjdk64-11.0.11 (set by /Users/yuanli/.jenv/version)
openjdk64-11.0.15

# set default jdk version
$ jenv global openjdk64-11.0.15

$ jenv versions
openjdk64-11.0.11
* openjdk64-11.0.15 (set by /Users/yuanli/.jenv/version)
```

3. (Optional)删除旧的jdk

```bash
$ sudo rm -rf /Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home/bin/java

$ jenv remove openjdk64-11.0.11

$ jenv versions
openjdk64-11.0.15
```

4. Set jdk for IDE

### other

Install Specific Versions of Java (Java8, Java11, Java13)
To install previous or specific versions of JDKs, you can get them from AdoptOpenJDK:

```bash
$ brew tap adoptopenjdk/openjdk

$ brew install --cask adoptopenjdk8
$ brew install --cask adoptopenjdk11
$ brew install --cask adoptopenjdk13
```

# Java版本切换

Now it is time to install jEnv:

```bash
brew install jenv
```

Add the following lines to ~/.bash_profile. This will initialize jEnv.

```bash
# Init jenv
if which jenv > /dev/null; then eval "$(jenv init -)"; fi
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


# Reference

- [Install Multiple Java Versions on Mac](http://davidcai.github.io/blog/posts/install-multiple-jdk-on-mac/)
- [Homebrew cask option not recognized?](https://stackoverflow.com/questions/30413621/homebrew-cask-option-not-recognized)
- [How to Use Brew to Install Java on Mac](https://devqa.io/brew-install-java/)
