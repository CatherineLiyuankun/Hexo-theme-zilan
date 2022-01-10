---
title: System-V 与 SystemD 区别
catalog: true
date: 2022-01-10 21:31:58
subtitle:
header-img:
tags:
- Command line
- TODO
categories:
- TECH
- Linux/bash
---




> One of the most fundamental distinctions in modern Linux systems is whether they use SystemV or Systemd. Here are the main differences between the two.
> 
> 1. SystemV is older, and goes all the way back to original Unix.
> 2. SystemD is the new system that many distros are moving to.
> 3. SystemD was designed to provide faster booting, better dependency management, and much more.
> 4. SystemD handles startup processes through .service files.
> 5. SystemV handles startup processes through shell scripts in /etc/init*.
> 
> Indicators
> 
> - If you’re starting and stopping things using `systemctl restart sshd`, etc, you’re on a SystemD system.
> - If you’re starting and stopping things using `/etc/init.d/sshd start`, etc, you’re on a SystemV system.
> 
> Which distros use which?
> 
> Many older versions of SystemD distros were SystemV.
> Here’s an incomplete but hopefully useful breakdown of which distros are on which system.
> 
> `Systemd`: Amazon Linux, Red Hat Enterprise, CentOS, Fedora, Debian/Ubuntu/Mint
> 
> Related
> an ics/scada primer
> `SystemV`: Gentoo, Alpine, Slackware, Linux from Scratch
> 
> Notes
> There are other startup systems as well, such as Upstart and BSD.



## 参考链接

- [The Difference Between System V and SystemD](https://danielmiessler.com/study/the-difference-between-system-v-and-systemd/)
- [system V与systemd](https://blog.csdn.net/qinhan728/article/details/48792691)
- [systemd、upstart和system V](https://www.cnblogs.com/baiyw/p/3504419.html)
