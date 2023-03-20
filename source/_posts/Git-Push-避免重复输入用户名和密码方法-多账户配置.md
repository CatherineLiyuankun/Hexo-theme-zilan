---
title: Git Push 避免重复输入用户名和密码方法 - 多账户配置
catalog: true
date: 2021-06-01 14:55:28
subtitle:
header-img:
tags:
- git
categories:
- TECH
- Tools
- Environment setup
---


# Git Push 避免用户名和密码方法

在大家使用github的过程中，一定会碰到这样一种情况，就是每次要push 和pull时总是要输入github的账号和密码，这样不仅浪费了大量的时间且降低了工作效率。在此背景下，本文在网上找了两种方法来避免这种状况，这些成果也是先人提出来的，在此只是做个总结。

## 1 方法一 .git-credentials

### 1.1 创建文件存储GIT用户名和密码

在%HOME%目录中创建文件名为.git-credentials的文件。
<!-- 文件保存在 OneDrive/LYKMACSetting/_Users_liyuankun/.git-credentials -->

%HOME%目录:

- Windows：一般为`C:\users\Administrator`，也可以是你自己创建的系统用户名目录，反正都在C:\users\中。
- Mac：/Users/YourUserName

```bash
cd ~
touch .git-credentials
vim .git-credentials
```

```bash
# 输入 https://{username}:{password}@github.com
https://{CatherineLiyuankun}:{xxxxxxxxx}@github.com
https://{yuanli}:{xxxxxxx}@github.yourcompanydomain.com
```

### 1.2 添加Git Config 内容

进入终端， 输入如下命令：

```bash
git config --global credential.helper store
```

执行完后查看%HOME%目录下的.gitconfig文件，会多了一项：

```bash
[credential]
helper = store
```

重启终端会发现git push时不用再输入用户名和密码。

## 2 方法二 环境变量

### 2.1 添加环境变量

添加一个HOME环境变量，变量名:HOME,变量值：%USERPROFILE%

### 2.2 创建git用户名和密码存储文件

进入%HOME%目录，新建一个名为"_netrc"的文件，文件中内容格式如下：

```bash
machine {git account name}.github.comlogin your-usernmaepassword your-password
```

重新打开终端，无需再输入用户名和密码
<!-- [user]
        name = Li,Yuankun
        email = yuanli@microstrategy.com -->

## 3 开启两步验证"Two-factor authentication"的github账号

前面用方法一之后， 重启终端， 重新`git push`, 跟据提示输入用户名和密码，结果报错：

```bash
Username for 'https://github.com': CatherineLiyuankun
Password for 'https://CatherineLiyuankun@github.com':
remote: Invalid username or password.
fatal: Authentication failed for 'https://github.com/CatherineLiyuankun/Todo-List-mojo.git/'
```

查了下原因，是因为我github账号 开启过两步验证，所以简单说就是不要输入`password` 而是要输入`personal access token`。
可以通过： [https://github.com/settings/tokens](https://github.com/settings/tokens) 查看你账号已有的personal access token。
如果没有可以新建一个`personal access token`，并保存下来。

 <!-- my own githut : token: "mac-MS"  -->

> It turns out that I need to log in using my username, but instead of using the normal GitHub account password, I should use a personal access token that can be created here.
>
> Because I am use GitHub feature named "Two-factor authentication" (It isn't a standard Git's feature, it's added feature by GitHub.com). After turn on the feature, I must create "Personal Access Tokens"

> **Reference**
>
> When you'll be asked for a personal access token as a password
After 2FA is enabled there are a couple of scenarios where you need to enter a personal access tokeninstead of a 2FA code and your GitHub password.

> **Through the command line**
>
> You must create a personal access token to use as a password when authenticating to GitHub on the command line using HTTPS URLs.
For example, when you access a repository using Git on the command line using commands like git clone, git fetch, git pull or git push with HTTPS URLs, you must provide your GitHub username and your personal access token when prompted for a username and password. The command line prompt won't specify that you should enter your personal access token when it asks for your password.

> **2FA and Subversion (svn command line, tortoise svn, etc)**
>
> When you access a repository via Subversion, you must provide a personal access token instead of entering your password.

## Git Credential Manager

[Caching your GitHub credentials in Git](https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git#git-credential-manager)

## 附录：配置git账户命令

``` bash
# 配置git账户
git config --list #查看当前配置
git config --list --local #查看当前仓库配置
git config --list --global #查看全局配置

# 配置全局账户（配置文件位于 ~/.gitconfig中）
git config --global user.name "your_name" # 如果是提到github上，your_name最好是你的github账户的名字
git config --global user.email "your_email@example.com" # 如果是提到github上，your_email@example.com最好是你的github账户的邮箱

# 配置本地仓库账户 (配置文件位于当前仓库目录的.git/config中）
git config --local user.name "your_name_in_company" # 如果是提到github上，your_name最好是你的github账户的名字
git config --local user.email "your_company_email@example.com" # 如果是提到github上，your_email@example.com最好是你的github账户的邮箱

```
