---
title: '解决 No matching host key type found. Their offer ssh-rsa'
catalog: true
date: 2023-10-03 20:28:12
subtitle:
header-img:
tags:
---


# No matching host key type found. Their offer: ssh-rsa问题处理 - 知乎

[https://zhuanlan.zhihu.com/p/616716090](https://zhuanlan.zhihu.com/p/616716090)

## Mac 上iterm2 脚本连接堡垒机报错

![Mac 上iterm2 脚本连接堡垒机报错](https://pic2.zhimg.com/80/v2-93fa626b6fa7f63932f9ab61102856ad_1440w.webp)

```bash
(base)x xxx@xxxMacBook-ProD > /usr/local/bin > expect /usr/local/bin/login/login-jumper.exp
spawn ssh -p 2xxxxxx
Unable to negotiate with 106.75.36.157 port 22222: no matching host key type found. Their offer: ssh-rsa spawn_id: spawn id exp6 not open
    while executing
"interact"
    (file "/usr/local/bin/login/login-jumper.exp" line 29)
```

## 原因

openssh觉得ssh-rsa加密方式不安全, 直接从8.8开始默认不允许这种密钥用于登陆了

## 解决方案

### 方案1: 临时性方案（命令行增加参数 `-oHostKeyAlgorithms=+ssh-rsa`）

![命令行增加参数 `-oHostKeyAlgorithms=+ssh-rsa`](https://pic2.zhimg.com/80/v2-dd2b52f6308497be0c2ff14ae194d225_1440w.webp)

```bash
$ ssh -oHostkeyALgorithms=+ssh-rsa -p 22222 -l
The authenticity of host '[baolei.zen-game.com]:22222 ([106.75.36.157]:22222)' can't be established.
RSA key fingerprint is SHA256:2wywU82+91MJq5vxjwWWOIpTNdVal2GYAOi35/FWm4.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:16: [zengame.uhasadmin.com]: 22222
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added "[baolei.zen-game.com]:22222 (RSA) to the list of known hosts.
Password authentication (mars.cai@baolei.zen-game.com) Password:
Welcome to SSHD

请选择多因子认证方式：
[1] 短信验证码
[2] 手机令牌OTP
[x] English
[e] 退出
```

连接成功

### 方案2:持久化方案（配置文件持久化）

输入`sudo nano ~/.ssh/config`，然后在出现提示时，输入您的管理密码

![输入您的管理密码](https://pic1.zhimg.com/80/v2-9f68694841e5892aae8a4c58811ae4cc_1440w.webp)

```bash
Host baolie .xxxxxx
HostKeyAlgorithms +ssh-rsa
```

输入上面内容，将需要连接的服务器IP加入到host，可以用 * 对所有主机生效

```
Host *

PubkeyAcceptedKeyTypes +ssh-rsa

HostKeyAlgorithms +ssh-rsa
```

第一行说明对所有主机生效, 第二行是将ssh-rsa加会允许使用的范围, 第三行是指定所有主机使用的都是ssh-rsa算法的key

连接测试成功，可以像往常一样通过SSH连接到服务器。
