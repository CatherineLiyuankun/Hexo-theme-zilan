---
title: nano编辑器使用&快捷键-Linux
catalog: true
date: 2022-12-25 12:45:33
subtitle:
header-img:
tags:
- Command line
categories:
- TECH
- Linux/bash
---

# 使用nano编辑器

```bash
# 编辑1.yaml文件，如果1.yaml文件不存在则新建
nano 1.yaml
# 粘贴+编辑

# 保存 control + o
# 退出 control + x
```

## nano快捷键

nano中被称为"快捷方式"，例如保存，退出，对齐等。最常见的功能在屏幕底部列出，但还有许多其他功能。

<!-- 请注意，nano不使用快捷键中的<kbd>Shift</kbd>键。 所有快捷方式均使用小写字母和未修改的数字键，因此<kbd>Ctrl</kbd> + <kbd>G</kbd>不是<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>G</kbd>。 -->

- 光标控制
  - 移动光标：使用用方向键移动。
  - 选择文字：按住鼠标左键拖动
  - ^A        move to the beginning of the current line.
    ^E        move to the End of the current line.

- 复制、剪贴和粘贴
  <!-- - 复制一整行：<kbd>option</kbd> + <kbd>6</kbd> -->
  - 复制和粘贴快捷键<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>c</kbd> and <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>v</kbd>
  - 剪切一整行<kbd>control</kbd>  + <kbd>K</kbd>
  - 在当前光标处插入上次剪切的内容<kbd>control</kbd>  + <kbd>U</kbd>

- 选中：<kbd>control</kbd>  + <kbd>U</kbd>
  - 如果需要复制／剪贴多行或者一行中的一部分，先将光标移动到需要复制／剪贴的文本的开头，按<kbd>control</kbd>  + <kbd>6</kbd>（或者<kbd>option</kbd> + <kbd>A</kbd>）做标记，然后移动光标到 待复制／剪贴的文本末尾。
  - 这时选定的文本会反白，用<kbd>option</kbd> + <kbd>6</kbd>来复制，<kbd>control</kbd>  + <kbd>K</kbd> 来剪贴。若在选择文本过程中要取消，只需要再按一次<kbd>control</kbd>  + <kbd>6</kbd>。

- 保存
  - 使用<kbd>control</kbd> + <kbd>O</kbd>来保存所做的修改

- 退出
  - 按<kbd>control</kbd> + <kbd>X</kbd> 
  - 如果你修改了文件，下面会询问你是否需要保存修改。
    - 输入<kbd>Y</kbd>确认保存，输入<kbd>N</kbd>不保存，按<kbd>control</kbd>  + <kbd>U</kbd>取消返回。
    - 如果输入了<kbd>Y</kbd>，下一步会让你输入想要保存的文件名。
      - 如果不需要修改文件名直接回车就行；若想要保存成别的名字（也就是另存为）则输入新名称然后回车。这个时候也可用<kbd>control</kbd>  + <kbd>U</kbd>来取消返回。
- Undo
  - <kbd>Meta</kbd> + <kbd>u</kbd>
  - 考试环境 + MAC OS 上的<kbd>Meta</kbd>实测是<kbd>Esc</kbd>
- Redo
  - <kbd>Meta</kbd> + <kbd>e</kbd>
- 搜索
  - 按<kbd>control</kbd>  + <kbd>W</kbd>，然后输入你要搜索的关键字，回车确定。这将会定位到第一个匹配的文本，接着可以用<kbd>option</kbd> + <kbd>W</kbd>来定位到下一个匹配的文本。

- 翻页
  - <kbd>control</kbd>  + <kbd>Y</kbd>到上一页 <kbd>control</kbd>  + <kbd>V</kbd>到下一页

>       ^G (F1)   Display this help text.
        ^F        move Forward a character.
        ^B        move Backward a character.
        ^P        move to the Previous line.
        ^N        move to the Next line.
        ^A        move to the beginning of the current line.
        ^E        move to the End of the current line.
        ^V (F8)   move forward a page of text.
        ^Y (F7)   move backward a page of text.

        ^W (F6)   Search for (where is) text, neglecting case.
        ^L        Refresh the display.

        ^D        Delete the character at the cursor position.
        ^^        Mark cursor position as beginning of selected text.
                  Note: Setting mark when already set unselects text.
        ^K (F9)   Cut selected text (displayed in inverse characters).
                  Note: The selected text's boundary on the cursor side
                        ends at the left edge of the cursor.  So, with
                        selected text to the left of the cursor, the
                        character under the cursor is not selected.
        ^U (F10)  Uncut (paste) last cut text inserting it at the
                  current cursor position.
        ^I        Insert a tab at the current cursor position.

        ^J (F4)   Format (justify) the current paragraph.
                  Note: paragraphs delimited by blank lines or indentation.
        ^T (F12)  To invoke the spelling checker
        ^C (F11)  Report current cursor position

        ^R (F5)   Insert an external file at the current cursor position.
        ^O (F3)   Output the current buffer to a file, saving it.
        ^X (F2)   Exit pico, saving buffer.