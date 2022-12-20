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

# Vim基本操作

参考文章：
- https://killercoda.com/vim 在线课程，直接操作，互动好，强推！
- [史上最全Vim快捷键键位图（入门到进阶）](https://www.runoob.com/w3cnote/all-vim-cheatsheat.html)

## 最常用的操作

Command | 功能 | Mode
---------|----------|---------
`:u0` | reset first to undo all changes
 `u` | undo | normal mode
 | w             | move forward one word (next alphanumeric word)                |
| 5w            | move forward five words                                       |
| b             | move backward one word (previous alphanumeric word)           |
| 5b            | move backward five
 `shift+6 (^)`  | 移动到行头 | C2
 `shift+4 ($)` | 移动到行尾 | C3
`数字+shift+g` | 移动到目标行，数字为行号
`:30`  | normal mode | Type `:30` to jump to line 30
gg | 到文件头部
G | 到文件尾部
dd | 删除当前行
`[n]d` + `Enter` | 删除n+1行，`2d`然后`Enter`, 删除当前行在内之后的3行。
`[n]dd` + `Enter` | Cut n行，`2d`然后`Enter`, 删除当前行在内之后的2行。
yy or Y | 复制整行文本。
3yy | 复制3整行文本。
| `yw`    | Copy to the start of next word         |
p | 在光标之后粘贴。
P | 在光标之前粘贴。

## Mode

| Mode   | Description      |
| ------ | ------------------ |
| Normal | Default mode for navigation and manipulation of text and it can always be activated by pressing `Esc`                    |
| Insert | Used for inserting/manipulating the text by using all keyboard keys. Not any Normal mode commands is active in this mode |
| Visual | Used for navigation and manipulation of text selections. Allows the use of most Normal mode commands on selected text    |

![mode transfer](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b386e6926dad4a8aa52e77ee9bd98ebb~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

## Insert mode


| Command | Description          | Mode
| ------- | ---------------- |---
i | 进入insert-mode
| `o`     | Insert new line **below** the current line | 进入insert-mode     |
| `O`     | Insert new line **above** the current line | 进入insert-mode      |
| `a`     | Append **after cursor** | 进入insert-mode                   |
| `A`     | Append at **end of line** | 进入insert-mode
| `s`     | Delete the character cursor is **currently on** | 进入insert-mode
| `C`     | Delete all **after cursor position** | 进入insert-mode

## 普通模式

Press Keyboard | Mode | 作用
---------|----------|---------
Esc | 返回normal mode | normal mode is default mode
`:x` | command-mode | save and quit
`:wq` | command-mode | same as `:x`
`:q` | command-mode | quit
`:q!` | command-mode | force quit
`:set number` | command-mode | to show the line numbers
`:30`  | normal mode | Type `:30` to jump to line 30 You can move to a line by just entering the line number in normal mode
`:goto 700` | normal mode | jump directly to a character in a file. Type `:goto` 700 to jump to 第700个character

### search

Press Keyboard | Mode | 作用
---------|----------|---------
`/` | search forward |  type `/search string` and press `enter`. Press `n` to jump to the next occurrence or `N` to jump to the previous occurrence
`/\<searchword\>` |  search forward | search the whole word，here is "is". 例如文件里"list is"的`list`不会match，只有`is`会被搜索到。
`/searchword`| |Vim allows us to start a search for the current word that the cursor is pointing. 搜索光标所在的单词。Type `/li` and press `Enter` Now, press `*` (asterisk) to search the entire word which is line in our case. You can also press `#` (hash) to search backwards
`?` | search backward |
`:s/old/new` | 用new替换当前行第一个old。
`:s/old/new/i` | 忽略大小写，Ignore Case。用new替换当前行第一个old。
`:s/old/new/g` | 用new替换当前行所有的old。
`:%s/old/new/g` | 用new替换文件中所有的old。

#### Search Ignore Case

By default search is case-insensitive. It is possible to ignore case in a search by adding \c to the end of your search string

Type `/` to enable search mode and type `this`

It won't return any results

Type `/` again and type `this\c` this time and notice that search finds string `This` which has a capital letter

You can also ignore case indefinitely for the current session

Type `:set ignorecase` or `:set ic`

To revert it back, Type `:set noignorecase` or `:set noic`

To make it default for vim, you need to add it to `~/.vimrc` file

Press `Esc` and type `:q!` to quit without saving

### navigate

| navigate in a file Shortcut Key  | Function           |
| ------------- | --------------------------------- |
| enter `]]` or `G` | To get to the last line
| enter `[[` or `gg` | To get to the first line
| $             | moves the cursor to the end of the line                       |
| ^             | moves the cursor to the first non-empty character of the line |
| w             | move forward one word (next alphanumeric word)                |
| W             | move forward one word (delimited by a white space)            |
| 5w            | move forward five words                                       |
| b             | move backward one word (previous alphanumeric word)           |
| B             | move backward one word (delimited by a white space)           |
| 5b            | move backward five words                                      |
| Ctrl + f      | moves the cursor one page down                                |
| Ctrl + b      | moves the cursor one page up                                  |
| h             | moves the cursor one character to the left                    |
| j or Ctrl + J | moves the cursor down one line                                |
| k or Ctrl + P | moves the cursor up one line                                  |
| l             | moves the cursor one character to the right                   |
| 0             | moves the cursor to the beginning of the line                 |

### Delete

Type 3d and press Enter to delete the first 4 lines. Notice that deleting is a 0 indexed operation with d command so try with 1d and notice that it will remove 2 lines below

Type D to remove the content of the line but not the line itself

#### Delete all lines in Vim

Type `gg` to get to first line
Type `dG` to clear the file completely


| Command          | Description        |
| ---------------- | ---------------------------- |
dd | 删除当前行
`[n]d` + `Enter` | 删除n+1行，`2d`然后`Enter`, 删除当前行在内之后的3行。deleting is a 0 indexed operation with d command so try with 1d and notice that it will remove 2 lines below
| `d<left-arrow>`  | Delete current and left character                 |
| `d<right-arrow>` | Delete current and right character                |
| `d<up-arrow>`    | Delete current and upper line                     |
| `d<down-arrow>`  | Delete current and bottom line                    |
| `d$`             | Delete from current position to end of line       |
| `d^`             | Delete from current backward to first character   |
| `dO`             | Delete from current backward to beginning of line |
| `dw`             | Delete current to end of current word             |
| `db`             | Delete current to beginning of current word       |

### Copy, Cut & Paste

ress Esc and type yy to copy the line (y is short for yank)

Type :2 to jump to line 2 and type p to paste the content to line 3

Repeat the operation by pressing dd to cut a line and p to paste the content
 

Type :u0 to undo all changes since opening to reset

Type :4 and get to line 4 and type 3yy to copy the current and next 2 lines

Type gg to get to the top and type P to paste these 3 lines before the cursor

Replace 3yy with 3dd to cut instead of copy and reply the operation if you wish

| Command | Description                            |
| ------- | -------------------------------------- |
| `y$`    | Copy all from current to end of line   |
| `y^`    | Copy all from current to start of line |
| `yw`    | Copy to the start of next word         |
| `yiw`   | Copy the current word                  |

## Advanced

### Comment out multiple lines

You'll often need to comment/uncomment multiple lines in a config file. You can perform this operation conveniently in Visual mode
Type `gg` to get to top and press `Shift + V` to activate Visual mode in block mode and notice that all text in the current line is selected

Type `2j` or use `down-arrow` key to select the first 3 lines

Type `:s/^/#` to replace the first character with `#`

### Sorting

Make a reset first to undo all changes by typing `:u0`

Make sure you are on top or type `gg` to get to the beginning of file

Press `Shift + V` to activate Visual mode in block mode

Press `G` to select all text

Type `:sort ui` and notice that the text is sorted
## other

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