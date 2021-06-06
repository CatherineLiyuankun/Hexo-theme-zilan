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
```

```bash
$ jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home
```

After that, run this command to list all registered JDKs:

```bash
jenv versions
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
