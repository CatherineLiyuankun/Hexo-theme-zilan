---
title: Vim操作&配置
catalog: true
date: 2022-11-08 23:16:39
subtitle:
header-img:
tags:
- Command line
categories:
- TECH
- Linux/bash
---

## Vim基本操作

参考文章：
- [史上最全Vim快捷键键位图（入门到进阶）](https://www.runoob.com/w3cnote/all-vim-cheatsheat.html)


最有用的操作：

### 普通模式

Comand | 功能 | Mode
---------|----------|---------
 `u` | undo | C1
 `shift+6 (^)`  | 移动到行头 | C2
 `shift+4 ($)` | 移动到行尾 | C3
`数字+shift+g` | 移动到目标行，数字为行号
gg | 到文件头部
G | 到文件尾部
dd | 删除当前行
yy or Y | 复制整行文本。
p | 在光标之后粘贴。
P | 在光标之前粘贴。

光标移动：
+或Enter: 把光标移至下一行第一个非空白字符。
-: 把光标移至上一行第一个非空白字符。
w: 前移一个单词，光标停在下一个单词开头；
W: 移动下一个单词开头，但忽略一些标点；
e: 前移一个单词，光标停在下一个单词末尾；
E: 移动到下一个单词末尾，如果词尾有标点，则移动到标点；
b: 后移一个单词，光标停在上一个单词开头；
B: 移动到上一个单词开头，忽略一些标点；


剪切和复制

[n]x: 剪切光标右边n个字符，相当于d[n]l。
[n]X: 剪切光标左边n个字符，相当于d[n]h。
y: 复制在可视模式下选中的文本。
yy or Y: 复制整行文本。
y[n]w: 复制一(n)个词。
y[n]l: 复制光标右边1(n)个字符。
y[n]h: 复制光标左边1(n)个字符。
y$: 从光标当前位置复制到行尾。
y0: 从光标当前位置复制到行首。
:m,ny<cr> 复制m行到n行的内容。
y1G或ygg: 复制光标以上的所有行。
yG: 复制光标以下的所有行。
d: 删除（剪切）在可视模式下选中的文本。
d$ or D: 删除（剪切）当前位置到行尾的内容。
d[n]w: 删除（剪切）1(n)个单词
d[n]l: 删除（剪切）光标右边1(n)个字符。
d[n]h: 删除（剪切）光标左边1(n)个字符。
d0: 删除（剪切）当前位置到行首的内容
p: 在光标之后粘贴。
P: 在光标之前粘贴。

查找和替换

/something: 在后面的文本中查找something。
?something: 在前面的文本中查找something。
n: 向后查找下一个。
N: 向前查找下一个。
:s/old/new - 用new替换当前行第一个old。
:s/old/new/g - 用new替换当前行所有的old。
:%s/old/new/g - 用new替换文件中所有的old。


## [Vim配置入门](https://www.ruanyifeng.com/blog/2018/09/vimrc.html)

## 参考文章

- [Vim 配置入门 - 阮一峰](https://www.ruanyifeng.com/blog/2018/09/vimrc.html)
- [Linux 基础篇-VIM编辑器](https://juejin.cn/post/7155688792093884423)