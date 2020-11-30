---
layout: 
title: MacOS 10.14.6 Karabiner-Elements不生效
date: 2020-07-29 05:14:01
tags:
---

参考[Does not work on MacOS Catalina #1867](https://github.com/pqrs-org/Karabiner-Elements/issues/1867)

For some reason the permission prompt is not showing up for me when I open Karabiner-EventViewer. And EventViewer says "EventViewer failed to observe keyboard devices". So I cannot find out a way to use
saagarjha's method as stated above.

1. add karabiner_grabber and karabiner_observer to “Security & Privacy > Privacy > Accessibility” apps.
2. And after sudo killall-ing both processes, Karabiner-Elements is working for me again.

```shell
$ sudo killall karabiner_grabber
$ sudo killall karabiner_observer
```

In order to fix the F-key/media playback buttons, I needed to add the following entries to the Security & Privacy > Privacy > Input Monitoring list:

/Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_grabber
/Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_observer