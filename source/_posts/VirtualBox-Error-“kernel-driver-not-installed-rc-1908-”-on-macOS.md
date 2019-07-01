---
title: VirtualBox Error “kernel driver not installed (rc=-1908)” on macOS
catalog: true
date: 2019-07-01 14:48:47
subtitle:
header-img:
tags:
- VirtualBox
categories:
- TECH
- Tools
---

I installed VirtualBox on Macbook Pro to run a new imported VM. Here is what I got when trying to start one:

![Error1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/VirtualBox-Error-%E2%80%9Ckernel-driver-not-installed-rc-1908-%E2%80%9D-on-macOS/Vitualbox%20error1.png)

![Error2](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/VirtualBox-Error-%E2%80%9Ckernel-driver-not-installed-rc-1908-%E2%80%9D-on-macOS/Vitualbox%20error2.png)

The error message is quite vague. It says On Linux, open returned ENOENT. What about on macOS? It turns out that I have to explicitly allow VirtualBox in the macOS system preference.

Go to System Preferences / Security & Privacy.

![Scurity](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/VirtualBox-Error-%E2%80%9Ckernel-driver-not-installed-rc-1908-%E2%80%9D-on-macOS/Scurity.png)

Click “Allow” in the window below.

![Scurity Allow](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/VirtualBox-Error-%E2%80%9Ckernel-driver-not-installed-rc-1908-%E2%80%9D-on-macOS/Allow.jpeg)

Now VirtualBox no longer complains about kernel driver.


Update: some people don’t see this button. According to a comment from Albert Wolszon:

> This Allow button section shows up only after first 30 minutes after the installation of VirtualBox. If you have this error and don’t see the button, uninstall VirtualBox, remove its belongings (there are usually some files left) and install it once again, then check this button again.
Thanks for the comments!

#The reference Links:
[Solving VirtualBox “kernel driver not installed (rc=-1908)” Error on macOS](https://medium.com/@Aenon/mac-virtualbox-kernel-driver-error-df39e7e10cd8)

