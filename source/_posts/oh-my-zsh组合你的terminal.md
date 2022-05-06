---
title: iterm2+oh-my-zsh组合你的terminal
date: 2020-05-24 12:26:42
subtitle: 效率提升奥利给
tags:
- Command line
categories:
- TECH
- Tools
- Environment setup
---

# [oh-my-zsh](http://ohmyz.sh)到底是个啥呢？

其实很早就装了[oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh)，但是没好好研究过好用的插件。趁此机会就全面总结下好了，省的我下次又忘记了。

> Oh My Zsh is an open source, community-driven framework for managing your zsh configuration.

简单说oh-my-zsh是基于zsh的管理配置框架。只是一个对zsh命令行环境的配置包装框架，但它不提供命令行窗口，更不是一个独立的APP。所以前提是先安装好zsh。

## 为什么要用Zsh？

（在[“利用Oh-My-Zsh打造你的超级终端”](https://blog.csdn.net/czg13548930186/article/details/72858289)第一部分的基础上修改。）
> 【兼容bash】原来爱用bash的童鞋切换过来毫无压力。
>
> 【强大的历史纪录功能】在用方向上键⬆查找历史命令时，zsh支持限制查找。比如输入git然后再按方向上键⬆,则只会查找用过的git命令。
>
> 【多个终端会话共享历史记录】经常有多个窗口，tab，tmux的多个session，panel。这些命令历史不能共享实在是很糟糕的回忆。
但是有了zsh之后，这些确实成了回忆了,所有的命令历史都可以共享。
>
> 【智能拼写纠正】输入gtep mactalk * -R，系统会提示：zsh: correct 'gtep' to 'grep' [nyae]?比妹纸贴心吧，她们向来都是让你猜的……
>
> 【各种补全】路径补全、命令补全，命令参数补全，插件内容补全等等。触发补全只需要按一下或两下tab键，补全项可以使用ctrl+n/p/f/b上下左右切换。
> 比如你想杀掉java的进程，只需要输入kill java + tab键，如果只有一个java进程，zsh 会自动替换为进程的 pid，如果有多个则会出现选择项供你选择。ssh+空格+两个tab键，zsh会列出所有访问过的主机和用户名进行补全
>
> 【不再需要输入cd命令跳转目录】 直接输入.. 或 … ，或目录名都可以跳转，不再需要输入cd命令了。
>
> 【通配符搜索】 ls -l **/*.sh，可以递归显示当前目录下的 shell 文件，文件少时可以代替find，文件太多还是用find。
>
> 输入 d，即可列出你在这个会话里访问的目录列表，输入列表前的序号，即可直接跳转。
>
> 【丰富的插件】安装了autojump插件之后，zsh 会自动记录你访问过的目录，通过 j + 目录名 可以直接进行目录跳转，而且目录名支持模糊匹配和自动补全，例如你访问过hadoop-1.0.0目录，输入j hado 即可正确跳转。j –stat 可以看你的历史路径库。

# oh-my-zsh 安装

## 1 [安装zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)

### 判断zsh是否已经安装

```bash
zsh --version
```

期望版本 zsh 5.4.2 或者更高。没有安装的话，按[官网步骤安装zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)就好了。

### 安装zsh

```bash
# Linux
sudo yum install zsh    (Fedora和RedHat以及SUSE中)或
sudo apt-get install zsh    (Debian系列，Ubuntu )

# macOS 系统自带了zsh, 一般不是最新版，如果需要最新版可通过Homebrew来安装(确认安装了Homebrew)
brew install zsh zsh-completions

# 或者也可以使用MacPorts(包管理工具)
sudo port install zsh zsh-completions

```

### 设置Zsh 作为默认shell

打开一个新的terminal来确认，设置Zsh 作为默认shell：

```bash
echo $SHELL
# 期望结果: /usr/bin/zsh or similar
# 如果shell列表中没有zsh或者你没有使用chsh权限的时候，不起作用
[sudo] chsh -s $(which zsh)  #或 chsh -s /bin/zsh
```

## 2 安装oh-my-zsh

Oh My Zsh 的安装方式简单，可以通过curl或wget的方式。

### curl 方式

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### wget方式

```bash
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

```

### git方式

```bash
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
```

### oh-my-zsh目录结构

进入~/.oh-my-zsh目录后，看看该目录的结构

```bash
$ ls ~/.oh-my-zsh
cache  custom  lib  log  MIT-LICENSE.txt  oh-my-zsh.sh  plugins  README.markdown  templates  themes  tools
```

>lib 提供了核心功能的脚本库
tools 提供安装、升级等功能的快捷工具
plugins 自带插件的存在放位置
templates 自带模板的存在放位置
themes  自带主题文件的存在放位置
custom 个性化配置目录，自安装的插件和主题可放这里

# oh-my-zsh 主题配置

## 默认主题

打开配置文件~/.zshrc

```bash
vi ~/.zshrc
```

找到`ZSH_THEME="robbyrussel"` 系统默认主题robbyrussel。

![默认主题robbyrussel](https://cloud.githubusercontent.com/assets/2618447/6316876/710cbb8c-ba03-11e4-90b3-0315d72f270c.jpg)

Oh My Zsh默认自带了一些主题，存放在~/.oh-my-zsh/themes目录中。我们可以查看这些主题，[官网也列出了许多主题的图片](https://github.com/ohmyzsh/ohmyzsh/wiki/themes), 方便我们挑选。

```bash
ls ~/.oh-my-zsh/themes
```

想用什么主题，我们只要修改配置`ZSH_THEME`。
然后保存这个文件文件，再打开一个新的命令行窗口即可看到效果了。我们还可以将主题设置为随机，这样在我们每次打开命令行窗口的时候，都会随机在已经安装的主题中选择一个。

```bash
ZSH_THEME="random"
```

我们如果觉得当前的主题比较喜欢，可以直接使用 echo 命令输出当前主题的名称

```bash
echo $ZSH_THEME
```

然后再将他设置到配置文件配置文件~/.zshrc中即可。

## 官方推荐主题agnoster

![agnoster](https://cloud.githubusercontent.com/assets/2618447/6316862/70f58fb6-ba03-11e4-82c9-c083bf9a6574.png)

为啥这个单拎出来说呢，因为需要额外安装[Powerline Fonts字体](https://github.com/powerline/fonts) (或[Cascadia Code PL /Cascadia Mono PL字体](https://github.com/microsoft/cascadia-code))和修改iTerm设置。

否则就会长这个样子：

![缺少字体](https://hustyichi.github.io/img/in-post/oh-my-zsh/first.jpg)

解决方法：

1. [下载Powerline字体库](https://github.com/powerline/fonts), 或者使用[Cascadia Code PL /Cascadia Mono PL字体](https://github.com/microsoft/cascadia-code)
2. 进入目录，执行install.sh脚本
3. iTerm -> Preferences -> Profiles -> Text -> Font 修改字体

### 修改配置文件~/.zshrc

```bash
ZSH_THEME="agnoster"
```

### 安装[Powerline Fonts字体](https://github.com/powerline/fonts)

#### 通过命令安装字体

```bash
# clone
$ git clone https://github.com/powerline/fonts.git --depth=1

# install
$ cd fonts
$ ./install.sh
cp: directory /Users/yuanli/Library/Fonts does not exist
Powerline fonts installed to /Users/yuanli/Library/Fonts

# 如果~/Library/Fonts 文件夹不存在，则创建文件夹后再次执行
$ ./install.sh
# ~/Library/Fonts里面就有需要的字体

# clean-up a bit
cd ..
rm -rf fonts
```

#### 通过font book安装字体

参考链接： <https://www.lifewire.com/how-to-manually-install-fonts-on-mac-2260815>

1. 打开Mac自带应用： Font Book

2. Select `File` and choose `Add Fonts` in the drop-down menu.

3. 选择刚刚在~/Library/Fonts下安装好的所有字体
4. Before you use the font, validate it to be sure it is safe to use. Select the font and choose `Validate Font` in the File menu to generate a Font Validation window.

这时候发现还是不生效。iTerm2需要额外配置，需要在终端中Regular font 和 the Non-ASCII Font选中刚刚安装的字体

### 修改iTerm2设置

#### 多设备共享iTerm2设置

iTerm2 --> Preferences --> General --> Preferences Tab

勾选 `Load preferences from a custom folder or URL`，并选择配置文件，这里我是用oneDrive共享过来的。
![修改iTerm2设置字体](https://github.com/CatherineLiyuankun/PictureBed/raw/218eec4defecbfe94b81086b7dfa7b4c099b9746/blog/post/oh-my-zsh%E7%BB%84%E5%90%88%E4%BD%A0%E7%9A%84terminal/iTerm2%E9%85%8D%E7%BD%AE%E5%85%B1%E4%BA%AB.png)

#### iTerm2设置主题

iTerm2需要额外配置，需要在终端中Regular font 和 the Non-ASCII Font选中刚刚安装的字体，点击iTerms的菜单"iTerm > Preferences > Profiles > Text"，进行配置（[git issue](https://github.com/powerline/fonts/issues/44)）。

##### 字体方案一【不管用】

![修改iTerm2设置](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/oh-my-zsh%E7%BB%84%E5%90%88%E4%BD%A0%E7%9A%84terminal/iTerm2%E8%AE%BE%E7%BD%AE.png)

按说这回就能正常显示主题agnoster了，但还是不行。

##### 字体方案二【管用】

后来在git issue上面查了半天，找到了[解决办法](https://github.com/ohmyzsh/ohmyzsh/issues/2869)。

iTerm2设置中不仅要修改Non-ASCII Font，还要修改字体。
这里我修改成：
![修改iTerm2设置字体](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/oh-my-zsh%E7%BB%84%E5%90%88%E4%BD%A0%E7%9A%84terminal/iTerm2%E8%AE%BE%E7%BD%AE2.png)

##### 字体方案三【管用】

看别人的经验，还可以把iTerm 2的设置里的Profile中的Text 选项卡中里的Regular Font和Non-ASCII Font的字体都设置成 Powerline的字体
`12pt Meslo LG S DZ Regular for Powerline`

或者:
![或者](https://cloud.githubusercontent.com/assets/1128227/9950693/c834c0ec-5dc5-11e5-92c1-a75d80f3d783.png)

##### 字体方案四【管用，正在使用】

如果之前安装的是[Cascadia Code PL /Cascadia Mono PL字体](https://github.com/microsoft/cascadia-code)，设置为：

- Font：Cascadia Code PL            Regular 12
- Non-ASCII Font：Cascadia Code PL  Regular 12

#### iTerm2配色方案

我的iTerm2配色跟agnoster不同，也需要修改。
下载[solarized](https://github.com/altercation/solarized#click-here-to-download-latest-version)。

进入刚刚下载的工程的solarized/iterm2-colors-solarized 下双击 Solarized Dark.itermcolors 和 Solarized Light.itermcolors 两个文件就可以把配置文件导入到 iTerm2 里

通过load presets选择刚刚安装的配色主题即可
![修改iTerm2设置字体](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/oh-my-zsh%E7%BB%84%E5%90%88%E4%BD%A0%E7%9A%84terminal/iTerm2%E8%AE%BE%E7%BD%AE%E9%85%8D%E8%89%B23.png
)

### VS Code 设置

但后来我发现，在VS Code的控制台中仍然有乱码。
原因是VS Code的字体设置有限制，只能设置monospace样式的字体，我找到了这篇文章
作者用的是Linux，跟Mac在目录结构上有些差异，我参照了前面提到的install.sh脚本中的信息，修改了一些地方，以下是Mac上的操作步骤：

- 从这个[链接](https://github.com/abertsch/Menlo-for-Powerline)下载字体文件
- sudo mv "Menlo for Powerline.ttf" ~/Library/Fonts
- VS Code -> Terminal Font Family 设置字体为 Menlo for Powerline

## [修改主题-怎样不显示主机名](https://github.com/agnoster/agnoster-zsh-theme/issues/39#issuecomment-307338817)

有的主机名很长，我不需要常常看到。我喜欢这个主题，但是主题里面带有主机名怎么办？

### 方法一 只修改改某一主题

比如我不想让ys主题显示主机名,编辑 ~/.oh-my-zsh/themes/ys.zsh-theme，最后面改成这样。**记得把#去掉**。

```bash
# PROMPT="
# %{$terminfo[bold]$fg[blue]%}#%{$reset_color%} \
# %(#,%{$bg[yellow]%}%{$fg[black]%}%n%{$reset_color%},%{$fg[cyan]%}%n) \
# %{$fg[white]%}in \
# %{$terminfo[bold]$fg[yellow]%}%~%{$reset_color%}\
# ${hg_info}\
# ${git_info}\
#  \
# %{$fg[white]%}[%*] $exit_code
# %{$terminfo[bold]$fg[red]%}$ %{$reset_color%}"
```

### 方法二 作用于所有主题

打开.zshrc 在底部粘贴， **记得把#去掉**:

```bash
# prompt_context() {
#  if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
#    prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"
#  fi
# }
```

这样就只显示用户名了. 如果你连用户名也不想显示，只需要注释掉这一行： `prompt_segment black default...`。

[其他修改主题的方法](https://github.com/ohmyzsh/ohmyzsh/wiki/themes)。

## 其他主题

如果这些默认主题还不能满足你的需要，我们还可以到这里找到更多的主题

> <https://github.com/robbyrussell/oh-my-zsh/wiki/Themes>
<https://github.com/robbyrussell/oh-my-zsh/wiki/External-themes>
<https://github.com/unixorn/awesome-zsh-plugins#themes>

# oh-my-zsh 插件推荐

## 默认插件

Oh My Zsh 默认自带了一些默认插件，存放在~/.oh-my-zsh/plugins目录中。可以查看：

```bash
ls ~/.oh-my-zsh/plugins
```

## 插件介绍

### [zsh-history-substring-search](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins/history-substring-search)

### [autojump](https://github.com/wting/autojump)

功能：实现目录间快速跳转，想去哪个目录直接 j + 目录名，不用在频繁的 cd 了！

```bash
# 这个命令就能找到近期 clone 了哪些库，省却了写一堆代码的功夫。
history | grep "git clone"
```

autojump 就是通过记录你在 history 中的行为把你访问过的文件夹路径都 cache 下来，当你输入路径名的时候会模糊匹配你之前cd过的目录路径，配合后面的自动提示插件，非常好用！！！

```bash
# 先cd到一些目录
cd ~/lyk/production
cd ~/lyk/src/react
# j快速切换到 ~/lyk/production目录下
j production
# jo快速在finder里打开文件夹 ~/lyk/production
jo production
```

### [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

日常用的命令会高亮显示，命令错误显示红色。
![zsh-syntax-highlighting例子](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/oh-my-zsh%E7%BB%84%E5%90%88%E4%BD%A0%E7%9A%84terminal/zsh-syntax-highlighting.png)

### [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

如图所示，输入命令时可提示自动补全（灰色部分），然后按键盘 → （！！！！上下左右的右键，不是tab键）即可补全。

<a href="https://asciinema.org/a/37390" target="_blank"><img src="https://asciinema.org/a/37390.svg" /></a>

更多插件可参考：

> <https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins>
<https://github.com/unixorn/awesome-zsh-plugins>
<https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins-Overview>

## 插件安装

安装zsh-history-substring-search、autojump、zsh-autosuggestions、zsh-syntax-highlighting插件:

```bash
# 安装zsh-history-substring-search
 git clone https://github.com/zsh-users/zsh-history-substring-search $ZSH_CUSTOM/plugins/zsh-history-substring-search
```

```bash
# 安装autojump
brew install autojump
```

```bash
# 安装zsh-autosuggestions
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

```bash
# 安装zsh-syntax-highlighting
git clone git://github.com/zsh-users/zsh-syntax-highlighting $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```

别忘了在~/.zshrc找到`plugins=`

```bash
vi ~/.zshrc
```

添加你想使用的插件。
注意不同插件间用空格，不要加逗号。

```bash
plugins=(
  git
  autojump
  zsh-autosuggestions
  zsh-syntax-highlighting
  zsh-history-substring-search
)
```

最后保存执行:

```bash
source ~/.zshrc
```

## 插件使用

[git plugin 命令](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git/)

# 其他技巧

## 给history命令增加时间

.zshrc中加入以下行

```bash
vim ~/.zshrc
HIST_STAMPS="yyyy-mm-dd"
source ~/.zshrc
```

如果没用oh my zsh的话可用如下alias

```bash
alias history='fc -il 1'
```

## 更新oh-my-zsh

设置自动更新oh-my-zsh

默认情况下，当oh-my-zsh有更新时，都会给你提示。如果希望让oh-my-zsh自动更新，在~/.zshrc 中添加下面这句

```bash
DISABLE_UPDATE_PROMPT=true
```

要手动更新，可以执行

```bash
upgrade_oh_my_zsh
```

## 卸载oh my zsh

直接在终端中，运行`uninstall_oh_my_zsh`既可以卸载。

# 借鉴文章

有点懒，把这几篇写的好的部分和官网结合在一起了。

- [oh-my-zsh让终端好用到飞起~](https://juejin.im/post/5d773da76fb9a06aff5e9a99)
- [利用Oh-My-Zsh打造你的超级终端](https://blog.csdn.net/czg13548930186/article/details/72858289)
- [Oh my zsh 配置与插件](https://hustyichi.github.io/2018/09/19/oh-my-zsh/)
- [Oh my zsh官网](http://ohmyz.sh)
