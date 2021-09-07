---
title: 改变echo的颜色-change the output color of echo in Linux
catalog: true
date: 2021-09-07 18:14:48
subtitle: command line 改色
header-img:
tags:
- Command line
categories:
- TECH
- Linux/bash
---


```bash
GREEN='\033[0;32m'
Yellow='\033[0;33m'
echo "${GREEN}"
echo "green string"
echo "${Yellow}"
echo "yellow string"
```

希望的输出：
"green string" 应该是绿色的
"yellow string" 应该是黄色的

实际输出：

```bash
\033[0;32m
green string
\033[0;33m
yellow string
```

> if you are using the echo command, be sure to use the -e flag to allow backslash escapes.
> 所以我们应该把`echo "${GREEN}"` 改成 `echo -e "${GREEN}"`

```bash
GREEN='\033[0;32m'
Yellow='\033[0;33m'
echo -e "${GREEN}"
echo "green string"
echo -e "${Yellow}"
echo "yellow string"
```

实际输出：

```bash
green string
yellow string
```

`green string` 是绿色的
`yellow string` 是黄色的

## 参考链接

- [How to change the output color of echo in Linux](https://stackoverflow.com/questions/5947742/how-to-change-the-output-color-of-echo-in-linux)
- [Git shell coloring](https://gist.github.com/vratiu/9780109)
