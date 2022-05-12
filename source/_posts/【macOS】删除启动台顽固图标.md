---
title: 【macOS】删除启动台顽固图标
catalog: true
date: 2022-05-12 16:22:53
subtitle: Delete icon from MAC launchpad
header-img:
tags:
- MAC
categories:
- TECH
- Tools
---

有些已经卸载的application在MAC launchpad (苹果启动台)无法删除：

## 解决

通过命令行删除图标，分步骤：

```bash
# 1 进入到/private/var/folders目录
cd /private/var/folders
# 2 搜索com.apple.dock.launchpad/db
cd $(sudo find . -name "com.apple.dock.launchpad")/db
# 3 删除启动台图标
sqlite3 db "delete from apps where title='要删除的application名称';"
# 4 关闭重启Dock
killall Dock
```

例子，我要删除Alfred 4，那么第3步骤的时候把`title`改成`'Alfred 4'`就可以了。

```bash
# 例如我要删除Alfred 4
sqlite3 db "delete from apps where title='Alfred 4';"&&killall Dock

```

命令合并起来就是：

```bash
cd /private/var/folders  && cd $(sudo find . -name "com.apple.dock.launchpad")/db &&  sqlite3 db "delete from apps where title='要删除的application名称';"&&killall Dock
```

## 参考链接

- [【macOS】删除启动台顽固图标与卸载残留](https://www.bilibili.com/video/BV1Cu411o7Zm/?p=2&spm_id_from=pageDriver)