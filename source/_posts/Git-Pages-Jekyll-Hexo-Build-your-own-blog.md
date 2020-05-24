---
title: Git Pages + Jekyll/Hexo Build your own blog
catalog: true
date: 2018-10-09 11:10:48
subtitle: 构建个人博客-你想知道的都在这里了
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/hexotheme/hexo-cover.png"
tags:
- Hexo
- Blog
categories:
- TECH
- Hexo
---
# Hexo 博客主题

[Hexo博客自建主题hexo-theme-zilan](../hexo-theme-zilan.html)

# 1 Github Pages

比较懒，默认都是用过gitbhub的啦

安装 Git
>Windows：下载并安装 git.
Mac：使用 Homebrew, MacPorts ：brew install git;或下载 安装程序 安装。
Linux (Ubuntu, Debian)：sudo apt-get install git-core
Linux (Fedora, Red Hat, CentOS)：sudo yum install git-core
Windows 用户
由于众所周知的原因，从上面的链接下载git for windows最好挂上一个代理，否则下载速度十分缓慢。也可以参考这个页面，收录了存储于百度云的下载地址。

>Mac 用户
您在编译时可能会遇到问题，请先到 App Store 安装 Xcode，Xcode 完成后，启动并进入 Preferences -> Download -> Command Line Tools -> Install 安装命令行工具。

---

>Windows 用户
由于众所周知的原因，从上面的链接下载git for windows最好挂上一个代理，否则下载速度十分缓慢。也可以参考[这个页面](https://github.com/waylau/git-for-win)，收录了存储于百度云的下载地址。

## step1 创建一个库 Create a repository
在[GitHub](https://github.com/) 页面[创建一个库](https://github.com/new) 命名规则是：username.github.io（username是Github用户名）。

例如我的就是CatherineLiyuankun.github.io，我已经建过这个库了，所以报错说库已经存在。
![setp1-1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/setp1-1.png)

## step2 clone 库
![setp2.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/setp2.png)
## step3 创建index.html
![setp3-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/setp3-1.png)
## step4 git push 
![setp4-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/setp4-1.png)
## step5 访问页面  
我的对应页面就是： https://catherineliyuankun.github.io/

![setp5-1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/setp5-1..png)
上面照着pages页面的步骤做就行，重点在下面

------

# 2 Jekyll or Hexo ?

弄到这里，我就犹疑了，查了查有用Jekyll 也有用 Hexo。这两个静态页面生成器（Static Website Generation）到底有什么区别，各自优缺有是什么呢？

| Tables | Jekyll | Hexo | 
| ------- |:-------------:| -----:| 
| 依赖 | ruby  gem （gem依赖也许会带来不兼容问题 **弱点**） | nodejs| 
|  | *brew install ruby*| *brew install node*|
| 安装 | *gem install jekyll*| ***npm install hexo-cli -g***|
| 生成静态站点的速度 | 随着网站内容增加越来越慢  **最大弱点**| 相当快 **优点**| 
| 与git Pages关系 | 背后运行引擎，支持html/md格式（把原文上传github， 可以直接生成博客，也可以用在线编辑器处理，但只能用[Github-safe plugins](https://help.github.com/articles/adding-jekyll-plugins-to-a-github-pages-site/)）**优点**| 无直接关系（本地生成 html 再上传），部署简单：deploy to Github pages or any other host with one deploy command | 
| 格式 | html/md | md | 
| 是否需本地环境 | 不需 | 需要 | 
| 编辑 | 不支持在titles或者YAML使用变量，许多插件过时了 **弱点** ；不buid-in支持livereload；不buid-in支持post pagination as of Jekyll 3 |大量可用的[免费插件](https://hexo.io/plugins/)  **优点**| 
| 模板 | copy Jekyll创始人的[示例库](https://github.com/mojombo/tpw)，以及其他用Jekyll搭建的[blog](https://github.com/jekyll/jekyll/wiki/Sites) | 大量可用的[免费开源主题](https://hexo.io/themes/) 中国社区很活跃 **优点**| 
| 迁移 | 依靠[Jekyll importers](https://import.jekyllrb.com/docs/home/)可从其他平台迁移博客（例如WordPress）**优点**| https://hexo.io/zh-cn/docs/migration | 
| 开源 | 免费开源 | 免费开源 | 
| category 分类 | 需要自己写标签语言遍历然后在创建各个分类的主页，再设置页面css，或者用ruby写插件 | 文章前使用“category: 分类名”，自动右边生成，包括分类主页，默认样式 | 
| 教程难度 | 相对更难 | 更简洁 | 
| 上手难度 | 相对更难 | 更简单 | 

------

# 3 Jekyll

官网： https://jekyllrb.com/docs/quickstart/
中文版官网：https://www.jekyll.com.cn/docs/quickstart/

## step 0 前提安装有ruby

 - 如果你是Mac用户，你就需要安装 Xcode 和 Command-Line Tools了。下载方式 Preferences →
   Downloads → Components。如果安装过Xcode和 Command-Line Tools，那就已经有ruby了。
   
 - 在 Windows 下使用 Jekyll 你可以使用 Jekyll running on Windows, 但是官方文档并不建议你在 Windows 平台上安装 Jekyll。

安装 ruby

Mac

```
brew install ruby
```

Linux

```
sudo apt-get intall ruby 
```

我已经安装有了。
检查下版本：
```bash
ruby -v
```

## step1 安装Jekyll
开始正题
```bash
~ gem install jekyll
```
## step2 建my-awesome-site

```bash
~ jekyll new my-awesome-site
```
手动把my-awesome-site目录下的所有内容复制到自己的git库中，我的是~/MyOwnGit/CatherineLiyuankun.github.io 或者是命令行复制
```bash
cd my-awesome-site
cp -R * /Users/liyuankun/MyOwnGit/CatherineLiyuankun.github.io/
```
## step3 启动Jekyll环境
```bash
➜  CatherineLiyuankun.github.io git:(master) ✗ jekyll serve
```

## step4 访问页面

通过http://localhost:4000 ，访问页面。


## step5 Jekyll博客模板

Jekyll创始人的[示例库](https://github.com/mojombo/tpw)，以及其他用Jekyll搭建的[blog](https://github.com/jekyll/jekyll/wiki/Sites)。

-----

# 4 Hexo
官网主题(模板)： https://hexo.io/themes/
中文版官网：https://hexo.io/zh-cn/docs/
## step 0 前提安装有Node.js

如果您的电脑中尚未安装所需要的程序，请根据以下安装指示完成安装。
安装 Node.js 的最佳方式是使用 nvm。

cURL:
```bash
$ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
```
Wget:
```bash
$ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
```
安装完成后，重启终端并执行下列命令即可安装 Node.js。
```bash
$ nvm install stable
```
或者您也可以下载 安装程序 来安装。

>Windows 用户
对于windows用户来说，建议使用安装程序进行安装。安装时，请勾选Add to PATH选项。
另外，您也可以使用Git Bash，这是git for windows自带的一组程序，提供了Linux风格的shell，在该环境下，您可以直接用上面提到的命令来安装Node.js。打开它的方法很简单，在任意位置单击右键，选择“Git Bash Here”即可。由于Hexo的很多操作都涉及到命令行，您可以考虑始终使用Git Bash来进行操作。

## step1 安装 Hexo
开始正题,所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。
```bash
$ npm install -g hexo-cli
```

## step2 init Hexo

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中(我新建了文件夹hexofolder)新建所需要的文件。
```bash
$ hexo init hexofolder
$ cd hexofolder
$ npm install
```
新建完成后，指定文件夹的目录如下：
```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```
_config.yml
网站的 配置 信息，您可以在此[配置大部分的参数](https://hexo.io/zh-cn/docs/configuration)。

package.json
应用程序的信息。EJS, Stylus 和 Markdown renderer 已默认安装，您可以自由移除。(具体看官方文档，这里就不赘述了)

scaffolds
模版 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。

Hexo的模板是指在新建的markdown文件中默认填充的内容。例如，如果您修改scaffold/post.md中的Front-matter内容，那么每次新建一篇文章时都会包含这个修改。

source
资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。

themes
主题 文件夹。Hexo 会根据主题来生成静态页面。

## step3 Hexo 命令

在<folder>文件夹下就可以执行
```
$ hexo g #hexo generate 生成
$ hexo s #启动本地web服务器
```
这时，通过http://localhost:4000 ，访问页面。就可以看到，hexo默认带的主题landscap的效果。

> Hexo[常用的几个命令](https://hexo.io/zh-cn/docs/commands)：
hexo generate (hexo g) 生成静态文件，会在当前目录下生成一个新的叫做public的文件夹
hexo server (hexo s) 启动本地web服务，用于博客的预览
hexo deploy (hexo d) 部署播客到远端（比如github, heroku等平台）
另外还有其他几个常用命令：
```
$ hexo new "postName" #新建文章
$ hexo new page "pageName" #新建页面
```
常用简写
```
$ hexo n == hexo new
$ hexo g == hexo generate
$ hexo s == hexo server
$ hexo d == hexo deploy
```
常用组合
```
$ hexo d -g #生成部署
$ hexo s -g #生成预览
```
## step4 添加其他主题
官网主题(模板)： https://hexo.io/themes/，在上面选择自己喜欢的模板，进入它对应的git页面，获得clone的链接。

这里以我改的主题Hexo-theme-zilan为例进行说明， 我这个主题增加了。

### 安装主题
```
$ hexo clean
$ cd hexofolder/themes
$ git clone https://github.com/CatherineLiyuankun/Hexo-theme-zilan.git
```
可以看到themes文件夹下多了一个文件夹Hexo-theme-zilan。

### 启用主题
修改Hexo目录下的_config.yml配置文件中的theme属性，将其设置为Hexo-theme-zilan。

###更新主题
```
$ cd themes/Hexo-theme-zilan
$ git pull
$ hexo g # 生成
$ hexo s # 启动本地web服务器
```
现在打开http://localhost:4000/ ，会看到我们已经应用了一个新的主题。

## step5 部署到git pages

这一步恐怕是最关键的一步了，让我们把在本地web环境下预览到的博客部署到github上，然后就可以直接通过http://CatherineLiyuankun.github.io/访问了。

首先需要明白所谓部署到github的原理。

之前步骤中在Github上创建的那个特别的repo（CatherineLiyuankun.github.io）一个最大的特点就是其master中的html静态文件，可以通过链接http://CatherineLiyuankun.github.io来直接访问。
Hexo -g 会生成一个静态网站（第一次会生成一个public目录），这个静态文件可以直接访问。
需要将hexo生成的静态网站，提交(git commit)到github上。
明白了原理，怎么做自然就清晰了。

使用hexo deploy部署
hexo deploy可以部署到很多平台，具体可以参考这个链接. 如果部署到github，需要在配置文件_config.xml中作如下修改：
```xml
deploy:
  type: git
  repo: git@github.com/CatherineLiyuankun.github.io
  branch: master
```
注意部署到git需要提前安装一个扩展：
```
$ npm install hexo-deployer-git --save
```
然后在命令行中执行
```
hexo d
```
即可完成部署。

去自己的git pages看下部署的成果吧！https://catherineliyuankun.github.io/


## step5 添加分类

### 添加分类页
新建一个页面，命名为 categories 。命令如下：
```
hexo new page categories
```
编辑刚新建的页面/source/categories/index.md，将页面的类型设置为 categories ，主题将自动为这个页面显示所有分类。
```md
title: 分类
date: 2018-8-22 12:39:04
type: "categories"
---
```
注意：如果有启用多说 或者 Disqus 评论，默认页面也会带有评论。需要关闭的话，请添加字段 comments 并将值设置为 false，如：
```
title: 分类
date: 2018-8-22 12:39:04
type: "categories"
comments: false
---
```
在菜单中添加链接。编辑主题的 _config.yml ，将 menu 中的 categories: /categories 注释去掉，如下:
```
menu:
  home: /
  categories: /categories
  archives: /archives
  tags: /tags
```
 
但是这样部署之后，在分类页面还是看不到任何分类的，同时官方的next教程中并没有写。
其实为文章添加分类关联的教程已经在hexo教程给出了。。
下面仅仅做个简单的介绍，全面的教程参照[hexo官方教程](https://hexo.io/zh-cn/docs/front-matter.html#%E5%88%86%E7%B1%BB%E5%92%8C%E6%A0%87%E7%AD%BE)

文章内添加分类：
```
---
title: Installing MySQL on Mac
catalog: true
date: 2018-09-29 14:23:53
subtitle: "zsh: command not found"
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Installing-MySQL-on-Mac/mysql-header.png"
tags:
- MySQL
categories:
- TECH
- Database
---
```

###添加文章分类关联
hexo中有Front-matter这个概念，是文件最上方以 — 分隔的区域，用于指定个别文件的变量。举个栗子，在hexo new post article时会生成article.md文件，文件生成好的文章属性。
```markdown
---
title: hexo next 为文章添加分类
date: 2018-8-22 18:12:43
tags:
---
```
在其中添加categories属性，再部署之后就可以在分类页看到分类了

```markdown
---
title: hexo next 为文章添加分类
date: 2018-8-22 18:12:43
tags:
categories: 
- Frontend
--- 
```
## step5+ 分类显示页面
参考[hughshen的文章](https://github.com/hughshen/blog/blob/c3390a5a99cfcf398a012a9cf742b7f41b49d345/app/posts/1437904915000-hexo-modify-theme.md)

我的Commit代码1：[\[categories\] page and category page work](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/5005553605b5b2c1a2077d5b025b2e387d93a030) 

Commit 代码2：[重构archive，category, tags ](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/2183339d41a39eb4c88847f953d08f6a8df72909)
Commit 代码3：[重构archive，category, tags2 ](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/84b8445e9e682c1ef284dc4a17938a16da977f89)

├── archive.ejs //文章归档，包括单个分类与单个标签，调用 _partial/archive.ejs
├── categories.ejs  //显示所有分类的布局，
├── category.ejs  //单个分类显示的布局，调用 _partial/archive.ejs
├── tags.ejs  //显示所有显示的布局，调用 _partial/archive.ejs, 调用_partial/tags.ejs

## step6 多级分类显示
利用系统的[list_categories(\[categories\], \[options\])](https://hexo.io/zh-cn/docs/helpers.html#list-categories)辅助函数生成分类列表;

<%- list_categories([options]) %>
| 参数 |	描述 |	默认值 |
|--|--|--|
|orderby|	分类排列方式|	name|
|order	|分类排列顺序。1, asc 升序；-1, desc 降序。|	1|
|show_count	|显示每个分类的文章总数|	true|
|style	|分类列表的显示方式。使用 list 以无序列表（unordered list）方式显示。|	list|
|separator	|分类间的分隔符号。只有在 style 不是 list 时有用。|	,|
|depth	|要显示的分类层级。0 显示所有层级的分类；-1 和 0 很类似，但是显示不分层级；1 只显示第一层的分类。|	0|
|class	|分类列表的 class 名称。	|category|
|transform	|改变分类名称显示方法的函数	|  |


具体代码见Commit: [\[categories\]\[sidebar\]Make categories display as hierarchical structure in sidebar](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/e7a7cd1843986f6cc4ac124184d3d0021d93aafe)
## step6+ 分类页面显示不同背景图片
```ejs
<!-- /Hexo-theme-zilan/themes/zilan/layout/_partial/header.ejs -->
<!-- Post Header -->
<style type="text/css">
    header.intro-header{
        <% if (is_home()) { %>
            background-image: url('<%= config.root + config["header-img"] %>'); 
            /*config*/
        <%} else if (is_post()){%>
            background-image: url('<%= page["header-img"] %>');
            /*post*/
        <%} else if (is_category()){%>
            background-image: url('<%= config.root + "img/header_img/category-bg.jpg" %>');
            /*category*/
        <%} else {%>
            background-image: url('<%= config.root + page["header-img"] %>');
            /*page*/
        <%} %>
    }
    <% if (config.signature) {%>
    #signature{
        background-image: url('<%= config.root + config["signature-img"] %>');
    }
    <%}%>

    <% if (config["header-cover-color"]) {%>
    #header-cover{
        background-color: <%= config["header-cover-color"] %>;
    }
    <%}%>
</style>
```

具体代码见Commit: [\[category\]\[header\]background img for url http://liyuankun.top/categories/xxxxx/](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/25b40c9d72c1eb0d62f97c376b6366d942eda12f) 

参考文章： [Hexo 魔改： 为 Next 主题 Header 栏设置可变化的背景图片](https://blog.chonghan.me/Hexo/Hexo-change-header-background-image/)


## step7 添加widget
看我的commit：[侧边栏 添加微信二维码widget](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/f799a1a0457d6c88bcd47a2502aecdbd2f4efd40)

## step8 模板
在layout布局文件夹中, 可以看到有的主题布局文件是.ejs 结尾，有的是.swig结尾，其实是使用的模板不同。
用于存放主题的模板文件，决定了网站内容的呈现方式，Hexo 内建 Swig 模板引擎，您可以另外安装插件来获得 EJS、Haml 或 Jade 支持，Hexo 根据模板文件的扩展名来决定所使用的模板引擎。
对于下载的[jade的模板](https://github.com/hexojs/hexo-renderer-jade)，需要在安装插件。终端下输入
```
npm install hexo-renderer-jade --save
```

对于下载的[Ejs的模板](https://github.com/hexojs/hexo-renderer-ejs)，需要在安装插件。终端下输入：
```
 npm install hexo-renderer-ejs --save
```
对于下载的[Haml的模板](https://github.com/hexojs/hexo-renderer-haml)，需要在安装插件。终端下输入：
```
 $ npm install hexo-renderer-haml --save
```

## step9 支持markdown数学公式
> 原生hexo并不支持数学公式，需要安装插件 mathJax。mathJax 是一款运行于浏览器中的开源数学符号渲染引擎，使用 mathJax 可以方便的在浏览器中嵌入数学公式。mathJax 使用网络字体产生高质量的排版，因此可适应各种分辨率，它的显示是基于文本的而非图片，因此显示效果更好。这些公式可以被搜索引擎使用，因此公式里的符号一样可以被搜索引擎检索到。

### step9.1 在hexo目录(我的是Hexo-theme-zilan)下安装：
```bash
$ npm install hexo-math --save
```

### step9.2 方法一配置hexo-math
代码可以参考我的commit：[支持markdown数学公式](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/71e6f7a23dbbb4056303c6374214077491f0f183)。

#### step9.2.1 在站点配置文件_config.yml 中添加：
 (我的是Hexo-theme-zilan/_config.yml)
```yml
math:
  engine: 'mathjax' # or 'katex'
  mathjax:
    # src: custom_mathjax_source
    config:
      # MathJax config
```

#### step9.2.2 在 zilan 主题配置文件_config.yml 中添加:
并将 mathJax.enable 设为 true.
(我的是Hexo-theme-zilan/themes/zilan/_config.yml) 
```yml
# MathJax Support
mathjax:
  enable: true
  per_page: false
  cdn: //cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML
```

#### step9.2.3 mathjax.ejs
在Hexo-theme-zilan/themes/zilan/layout/_third-party/添加 mathjax.ejs
mathjax.ejs
```ejs
<% if(theme.mathjax.enable) { %> 
  <% if (!theme.mathjax.per_page || (page.total || page.mathjax)) { %> 
    <script type="text/x-mathjax-config">
      MathJax.Hub.Config({
        tex2jax: {
          inlineMath: [ ['$','$'], ["\\(","\\)"]  ],
          processEscapes: true,
          skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
        }
      });
    </script>

    <script type="text/x-mathjax-config">
      MathJax.Hub.Queue(function() {
        var all = MathJax.Hub.getAllJax(), i;
        for (i=0; i < all.length; i += 1) {
          all[i].SourceElement().parentNode.className += ' has-jax';
        }
      });
    </script>
    <script type="text/javascript" src="<%= theme.mathjax.cdn%>"></script>
  <% } %>
<% } %>
```

#### step9.2.4 mathjax.ejs配置
添加到Hexo-theme-zilan/themes/zilan/layout/layout.ejs中：
```ejs
  <!-- Markdown math -->
  <% include ./_third-party/mathjax.ejs %>
```

### step9.2 方法二 直接添加hexo-math(不推荐)
建议用方法一，方便灵活配置。
添加到Hexo-theme-zilan/themes/zilan/layout/layout.ejs中：
```html
<script type="text/javascript"
   src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```

-----

## step10 Hexo博客中插入音乐和视频

[Hexo博客中插入音乐和视频](../Hexo博客中插入音乐和视频.html)

## step11 Hexo插入相对路径

[Hexo博客中插入相对路径](../hexo-reference%20path%20for%20link%20to%20another%20blog%20post.html)

# 5 博客配置

## 5.1 绑定域名
### step1 买域名
可以在[阿里云](https://wanwang.aliyun.com/domain/?spm=5176.8006371.1007.dnetcndomain.q1ys4x)购买的域名。我这个 liyuankun.top 的域名第一年才只要1元([新用户特惠](https://wanwang.aliyun.com/domain/1yuan?spm=5176.8112568.483655.12.3c8f9ed5abPlyL))~ 我又续了9年，共10年才145元。

域名尽量选择短一点比较好记住，中文域名比如 博客.top ,GitHub Pages 无法处理中文域名，会导致你的域名在你的主页上不能使用。

常见国际域名后缀：.com，.net，.top，tech，.ink，.info，.win等
常见国内域名后缀：.cn,   .com.cn,  .cx,  .cc,  .xin等

### step2 修改CNAME
如果你不想用http://username.github.com/jekyll_demo/这个域名，可以换成自己的域名。

具体方法是在repo的根目录下面，新建一个名为CNAME的文本文件（注意一定是大写的！！！），里面写入你要绑定的域名，比如liyuankun.top或者xxx.example.com。
或者是在github 你的pages库：CatherineLiyuankun.github.io 的Setting 选项里，设置Custom domain：liyuankun.top。就会自动新建一个名为CNAME的文本文件，里面写入你填写的域名：liyuankun.top。
![5_1-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5_1-1.png)
![5_1-2](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5_1-2.png)

### step3 域名解析
在你的域名注册提供商那里配置DNS解析，获取[GitHub的IP地址](https://help.github.com/articles/setting-up-an-apex-domain/), 或者直接ping CatherineLiyuankun.github.io, 得到IP。
```bash
$ ping CatherineLiyuankun.github.io
PING catherineliyuankun.github.io (185.199.109.153): 56 data bytes
64 bytes from 185.199.109.153: icmp_seq=0 ttl=47 time=459.228 ms
```
如果绑定的是顶级域名，则DNS要新建一条A记录，指向185.199.109.153，主机记录为 www,代表可以解析 www.liyuankun.top的域名。

另一个为 @, 代表 liyuankun.top，记录值就是我们博客的IP地址，刚才ping出的地址 185.199.109.153
（如果绑定的是二级域名，则DNS要新建一条CNAME记录，指向CatherineLiyuankun.github.com）

此外，别忘了将_config.yml文件中的baseurl改成根目录"/"。

![5_1-step3.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5_1-step3.png)

### step4 域名备案
>购买好域名后我就可以直接使用它吗？
如果只是用作pages博客的域名，前面三步骤就可以使用了。
如果需要绑定七牛云或者其他用途，则需要域名备案。域名只有经过备案审核后才能使用，审核必须有相应的主机，光有域名不行。

>那我该如何备案呢？
#### 1通过全国公安机关互联网安全管理服务平台 备案
[如何进行公安网备案？](https://developer.qiniu.com/af/kb/3987/how-to-make-website-and-inquires-the-police-put-on-record-information)
#### 2通过阿里云 备案
> 1. 在阿里云登录后进入[备案系统](https://beian.aliyun.com/)，申请备案。
>  2. 按表单要求填写真实的备案信息，然后点击提交。此操作需要证件照（身份证或其他有效证件）的正反面照片。按表单要求填写真实的备案信息，然后点击提交。此操作需要证件照（身份证或其他有效证件）的正反面照片。
 > 3. 提交申请后过一天或两天，阿里云工作人员会给你打电话，验证你的姓名和身份证后四位等信息就算是初审通过了。
 > 4. 接下来你需要再次登录备案系统，申请幕布拍照，然后点击指定链接，网购价值15元的幕布，以此为背景拍照再上传到备案系统。
>  5. 工作人员会对照片进行审核，照片审核通过后他们会把你的备案信息提交给省通信管理局审核，通信管理局一般会审核11—20天，审核通过后会发短信和邮件通知你。


## 5.2 网站统计

### 5.2.1 [sitemap](https://github.com/hexojs/hexo-generator-sitemap)

hexo所在文件夹下，命令行安装sitemap:
```bash
$ npm install hexo-generator-sitemap --save
$ npm install hexo-generator-baidu-sitemap --save
```

在_config.yml里添加：
```yml
#sitemap
sitemap:
  path: sitemap.xml

baidusitemap:
  path: baidusitemap.xml

```

如果你已经配置了自己的域名，在_config.yml里修改url为自己的域名，例如我的http://liyuankun.top/。
```yml
url: http://liyuankun.top
```

生成sitemap.xml 和 baidusitemap.xml 文件：
```bash
$ hexo g
$ hexo d
```

配完之后，就可以访问http://liyuankun.top/sitemap.xml和http://liyuankun.top/baidusitemap.xml，发现文件已经成功生成了.


老版本的Google Search Console 在抓取--》 robots.txt测试工具 可以 测试robots.txt。 新版本中好像找不到了。。。后来找到了，robots.txt [测试工具链接](https://support.google.com/webmasters/answer/6062598)在此。
百度也有[robots.txt工具](https://ziyuan.baidu.com/robots/index?site=http://liyuankun.top/)。

借助 robots.txt 测试工具，您可以检查 robots.txt 文件是否可以阻止 Google 网页抓取工具访问您网站上的特定网址。例如，您可以使用此工具来测试 Googlebot-Image 抓取工具能否抓取您想阻止 Google 图片搜索访问的图片网址。

在your-hexo-site\source中新建文件robots.txt,内容可以参照:

```text
# hexo robots.txt
User-agent: *
Allow: /
Allow: /archives/
Allow: /categories/
Allow: /tags/
Allow: /about-me/
Disallow: /vendors/
Disallow: /js/
Disallow: /css/
Disallow: /fonts/
Disallow: /vendors/
Disallow: /fancybox/
Sitemap: http://liyuankun.top/sitemap.xml
Sitemap: http://liyuankun.top/baidusitemap.xml
```


### 5.2.2 [Google Search Console](https://search.google.com/search-console/about)

![5_2-2GoogleSearchConsole-1welcom](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5_2-2GoogleSearchConsole-1welcom.png)

然后选择验证方式：
![5_2-2GoogleSearchConsole-2verify](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5_2-2GoogleSearchConsole-2verify.png)

我选择的验证方式是HTML标记（HTML Tag）,
![5_2-2GoogleSearchConsole-2verifyHtmlTag](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5_2-2GoogleSearchConsole-2verifyHtmlTag.png)

把复制的"<meta ...>"部分粘贴到 your hexo folder/themes/zilan/layout/_partial/head.ejs
```html
<head>
    <!-- other tag -->
    <meta name="google-site-verification" content="4aJ9pFEKjOcI9zlltw5NYLKMsnk_Ygy49okv3PcTknw" />
    <!-- other tag -->
</head>
```

提交sitemap
![5_2-2GoogleSearchConsole-3sitemap](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5_2-2GoogleSearchConsole-3sitemap.png)

### 5.2.3 Baidu sitemap
[百度搜索引擎提交入口](https://ziyuan.baidu.com/site/#/)
![5.2.3Baidu1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5.2.3Baidu1.png)
百度搜索有三种验证方式，我选择Html标签验证，把复制的"<meta ...>"部分粘贴到 your hexo folder/themes/zilan/layout/_partial/head.ejs：
```html
<head>
    <!-- other tag -->
    <meta name="baidu-site-verification" content="JFD0vIDsbS" />
    <!-- other tag -->
</head>
```
验证成功后，查看[站点信息](https://ziyuan.baidu.com/dashboard/index?site=http://liyuankun.top/)

百度的sitemap提交需要邀请才可以，并没有对所有网站开放，网站高一点等级才会在你后台开放提交sitemap的入口。

[robots.txt工具](https://ziyuan.baidu.com/robots/index?site=http://liyuankun.top/)可以告诉百度您网站的哪些页面可以被抓取，哪些页面不可以被抓取。
![5.2.3Baidu2Robots](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5.2.3Baidu2Robots.png)

### 5.2.4 Analytics
集成了 [Baidu Analytics](https://marketingplatform.google.com/about/) 和 [Google Analytics](https://marketingplatform.google.com/about/)，到各个网站注册拿到track_id替换下面的就可以了

配置方法： https://www.jianshu.com/p/7e1166eb412a

```md
# Analytics settings
# Baidu Analytics
# ba_track_id: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
# Google Analytics
ga_track_id: 'UA-XXXXXXXX-X'          # Format: UA-xxxxxx-xx
ga_domain: yoursite
```

### 5.2.5 添加baidu站内搜索

添加[百度站内搜索](https://ziyuan.baidu.com/cse/wiki/introduce)，点击现在使用->新建搜索引擎->查看代码，将代码里的id值复制，打开_config.xml，添加配置。
```yml
baidu_search:     ## http://zn.baidu.com/
  enable: true
  id: "567867xxxxx1171234" ## for your baidu search id
  site: http://zhannei.baidu.com/cse/search ## your can change to your site instead of the default site
```

## 5.3 评论
### [Disqus](https://disqus.com/) 
博客中使用的是 [Disqus](https://disqus.com/) 评论系统，注册帐号后，按下面的步骤简单的配置即可：

> 一定一定要注意不是username!!!!!!!! 是shortname！！！！

刚开始被有些文章误导了，disqus_username: 填成username。造成评论一直无法显示!
> We were unable to load Disqus. If you are a moderator please see our troubleshooting guide.

什么是shortname?  https://help.disqus.com/installation/whats-a-shortname
去哪找shortname呢？
在https://disqus.com/admin/create/  点击setting。
没创建页面的先创建页面，输入网站名（就是根据这个生成Shortname的）lyk,
下一步选免费的，然后选应用，填网址https://catherineliyuankun.github.io/。成功！

> Shortname    Your website shortname is lyk-1

![5_3-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5_3-1.png)

这个 Shortname 就是我们 _config.yml 中 disqus_username
```yml
# Disqus settings
disqus_username: lyk-1
```

### Gitment


####**step 1 注册 OAuth Application**

 1. 登录 Github。 注册 https://github.com/settings/profile (左侧下方的 Developer
    settings->点击绿色 Register a new application)
 2. 填写：
```
Application name：Gitment
Homepage URL：https://catherineliyuankun.github.io/
Application description：Blog comment system
Authorization callback URL：https://catherineliyuankun.github.io/
```
点击 Register application后获取：
```
Client ID: xxxx
Client Secret: xxxxxxxxxx
```
3. 新建一个git 库存放 gitment-comments, Repository name 为 gitment-comments
地址：https://github.com/catherineliyuankun/gitment-comments
但是稍后填的是库名：gitment-comments，不是地址。


#### step 2 添加 Gitment 到博客
打开 __config.yml, 添加设置：
```yml
gitment:
  enable: true
  mint: true 		# RECOMMEND, A mint on Gitment, to support count, language and proxy_gateway
  count: true 		# Show comments count in post meta area
  lazy: false 		# Comments lazy loading with a button
  cleanly: false 	# Hide 'Powered by ...' on footer, and more
  language: 		# Force language, or auto switch by theme
  github_user: catherineliyuankun 	# 此处 - Your Github ID
  github_repo: gitment-comments # 此处注意 - The repo you use to store Gitment comments
  client_id: xxxxxxxxxxxxxxxxxx # 此处 - Github client id for the Gitment
  client_secret: xxxxxxxxxxxxx # 此处 - Github access secret token for the Gitment
  proxy_gateway: # Address of api proxy, See: https://github.com/aimingoo/intersect
  redirect_protocol: # Protocol of redirect_uri with force_redirect_protocol when mint enabled
```
添加gitment代码（页面，样式，script等）到主题：我的主题的[commit gitment代码](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/28458cf69588837448ab769f645eea3948a704fc)

部署:
```bash
hexo g -d
```
之后文章底部会出现 初始化本文的评论页，点击初始化。


## 5.4 二维码
添加微信二维码 commit 代码 ：[Add wechat QR code widget](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/f799a1a0457d6c88bcd47a2502aecdbd2f4efd40)


## 5.5 git fork me

获取[forlk me代码](https://blog.github.com/2008-12-19-github-ribbons/)，选择你喜欢的代码添加到hexo/themes/zilan/layout/layout.ejs的末尾即可，注意要将代码里的you改成你的Github账号名。

我的博客模板的[commit](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/15cced30f3d95e466cd5d10f8f3a462707c9d336)。

## 5.6 使用图床
### 七牛云
有很多推荐[七牛云](https://portal.qiniu.com/signup?code=3lbl5aqwrovv6), 具体方法可以看[这篇文章](https://www.jianshu.com/p/44d818f781a7).

用插件上传图片时报错：
>请求报文格式错误。(400：incorrect region, please use up-z2.qiniup.com)
我之前选的“华南”地区。伤心，查了查官网上传没有问题，可以自动切换上传区域。插件可能还没更新最新的sdk造成的。算了先用官网上传吧。

[存储区域和上传域名的对应关系](https://developer.qiniu.com/kodo/manual/1671/region-endpoint)：
[上传慢、上传失败等上传常见问题的处理方法](https://developer.qiniu.com/kodo/kb/3882/upload-problem-faq)

除了上传图片的基本功能，还可以[添加水印](https://developer.qiniu.com/dora/manual/1316/image-watermarking-processing-watermark)。[制作图片水印以及缩略图](https://blog.csdn.net/yongf2014/article/details/50016761)

但是现在七牛云的测试域名30天就会回收不能使用了，需要[绑定自己的域名](https://portal.qiniu.com/cdn/domain/create?ref=developer.qiniu.com)，但是自己的域名必须[公安网备案](https://developer.qiniu.com/af/kb/3987/how-to-make-website-and-inquires-the-police-put-on-record-information)才可以使用。备案审核必须有相应的主机，光有域名不行。也就是说你只买有域名，同时没有买过（或租）服务器是无法审核的。所以不想买主机的童鞋可以用下面👇的方法，或者换其他的图床。

### github 做图床

用github新建个库，[PictureBed](https://github.com/CatherineLiyuankun/PicturexxBed)专门放我的博客图好了。

> 注意! 一定要设置成Public的，不要设置成private私有的。
> 注意! 一定要设置成Public的，不要设置成private私有的。
> 注意! 一定要设置成Public的，不要设置成private私有的。
> 设置成私有后，图片链接会带有?token=AB6MExxxxxxxxI5K6XVVI4
> https://raw.githubusercontent.com/CatherineLiyuankun/PictureBed/master/blog/post/xxx.png?token=AB6MExxxxxxxxI5K6XVVI4 
> 过一段时间token会失效，获取图片就会返回404
> 设置成public,就可以继续用了

克隆到本地：
```bash
git clone https://github.com/CatherineLiyuankun/PicturexxBed.git
```
然后添加图片。
需要注意的是：到GitHub提取图片地址时，注意把blob改成 raw。
例如github中一张图片的地址是：https://github.com/CatherineLiyuankun/PictureBed/blob/master/blog/base/alipay.png

在博客中图片使用时的地址是：
https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/base/alipay.png

## 5.7 RSS订阅
我的[commit](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/28f6a36b995656795f1a1ffc844d74964875f872) 

### 安装插件
hexo博客有一个专门生成RSS xml文件的插件hexo-generator-feed。
安装：
```bash
$ npm install hexo-generator-feed --save
```
### 配置
_config.yml文件中添加如下内容
```yml
# Extensions
plugins:
    hexo-generator-feed
#Feed Atom
feed:
    type: atom
    path: atom.xml
    limit: 20
```

###生成RSS
```zsh
➜  Hexo-theme-zilan git:(master) ✗ hexo g
(node:88561) [DEP0061] DeprecationWarning: fs.SyncWriteStream is deprecated.
INFO  Start processing
INFO  Files loaded in 437 ms
INFO  Generated: category-sitemap.xml
INFO  Generated: sitemap.xsl
INFO  Generated: sitemap.xml
INFO  Generated: tags/index.html
INFO  Generated: about/index.html
INFO  Generated: archive/index.html
INFO  Generated: atom.xml     就是生成这个！
......
```

可以订阅了，把https://catherineliyuankun.github.io/atom.xml输入到邮箱的订阅地址就行了！


## 5.8 font awesome 图标
http://www.bootcss.com/p/font-awesome/

## 5.9 添加email to
[官网教程](https://hexo.io/zh-cn/docs/helpers#mail-to) 
```ejs
<%- mail_to('a@abc.com') %>
// <a href="mailto:a@abc.com" title="a@abc.com">a@abc.com</a>

<%- mail_to('a@abc.com', 'Email') %>
// <a href="mailto:a@abc.com" title="Email">Email</a>
```
我的[commit代码](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/246e4e2c3b93426bbbeef1e347067da4e01b947e)，还用到了font awesome 图标。

## 5.10 捐赠/赏
我的[commit代码](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/b080910aeea650d72ab4932fd2673f885c05b21c)
在_config.yml里添加属性来控制是否显示捐赠按钮：
```yml
# donate
donate: true
donate-alipay: img/alipay.png
donate-wechat: img/wechatpay.png
```
在zilan/layout/_partial下添加donate.ejs文件，用来放相应页面代码
```html
<!-- Donate -->
<% if(config['donate']) { %>
<div>
    <div class="donate-container" style="padding: 10px 0; margin: auto auto; width: 90%; text-align: center;">
        <div></div>
        <button id="rewardButton" disable="enable" onclick="var qr = document.getElementById('QR'); if (qr.style.display === 'none') {qr.style.display='block';} else {qr.style.display='none'}">
        <span>Donate</span>
        </button>
        <div id="QR" style="display: none;">
            <div id="wechat" style="display: inline-block">
                <img id="wechat_qr" src="<%= config['donate-wechat']%>" alt="WeChat Pay" style="width: 200px; height: 200px; text-align: center;">
            <!-- <p>Wechat</p> -->
            </div>
            <div id="alipay" style="display: inline-block">
                <img id="alipay_qr" src="<%= config['donate-alipay']%>" alt="Alipay" style="width: 200px; height: 200px; text-align: center;">
            <!-- <p>Alipay</p> -->
            </div>
        </div>
    </div>
</div>
<% } %>
```
在博客文章页面 themes/zilan/layout/post.ejs 里添加进捐献页面donate.ejs
```ejs
 <%- partial('_partial/donate') %>
```


## 5.11 利用 Fancybox 添加图片放大预览查看功能


基于donate功能，为二维码图片提供点击放大的功能。
我的[commit代码](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/40e5b397a9d9cf5eb657c55867cd8999da3874c2)

###在_config.yml里添加属性来控制是否使用fancybox按钮：
```yml
fancybox: true
```

###下载fancybox库
点击下载最新的 [fancybox 库](https://github.com/fancyapps/fancybox/releases/tag/v3.4.0)， 解压缩至 /theme/material/source/fancybox/ 目录下，这里贴出目录结构：

 ![5_11-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/5_11-1.png)

###在themes/zilan/source/js/下添加wrapImage.js, 用于在指定的 <img> 外裹一层 fancybox 所需要的属性
```javascript
  // Caption
  $('.donate-container').each(function(i){
    $(this).find('img').each(function(){
      if ($(this).parent().hasClass('fancybox')) return;
       var alt = this.alt;
       if (alt) $(this).after('<span class="caption">' + alt + '</span>');
       $(this).wrap('<a href="' + this.src + '" title="' + alt + '" class="fancybox"></a>');
    });
     $(this).find('.fancybox').each(function(){
      $(this).attr('rel', 'article' + i);
    });
  });
   if ($.fancybox){
    $('.fancybox').fancybox();
  } 
```

###在themes/zilan/layout/layout.ejs下添加fancybox script, css
```ejs
    <% if (theme.fancybox){ %>
        <%- css('/fancybox/jquery.fancybox') %>
        <%- js('/fancybox/jquery.fancybox.pack') %>
        <%- js('/js/wrapImage.js') %>
    <% } %>
```

成功！

## 5.12 Share 分享
用的第三方组件[need-more-share2](https://github.com/revir/need-more-share2)
另外可以参考主题next添加need-more-share2的[pull request](https://github.com/iissnan/hexo-theme-next/pull/1913/files)

fix bug: [微信分享图片无法loading出来](https://github.com/iissnan/hexo-theme-next/pull/1976)
source\lib\needsharebutton\needsharebutton.js

```javascript
var imgSrc = "https://api.qinco.me/api/qr?size=400&content=" + encodeURIComponent(myoptions.url);
```
改为
```javascript
var imgSrc = "http://tool.oschina.net/action/qrcode/generate?output=image/png&error=L&type=0&margin=2&size=4&data=" + encodeURIComponent(myoptions.url);

```

我的[commit](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/3c6ca2bdef522acbc1d57bb252868481f99620b3)

## 5.13 版权声明
以zilan 主题来举例，”your_theme“ is ”zilan“。
对应commit 代码： [\[copyright\]\[post\] add copyright](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/21b7d216e43e494c3757b6764198d214b021943f)

### 5.13.1 Html 内容
在your_theme\layout\_partial\post下面，创建一个名为copyright.ejs的文件，在里面填写

```
<! -- 添加版权信息 -->
<div class="article-footer-copyright">
  <div><b>本文标题: </b><a href="<%- config.root %><%- page.path %>" target="_blank" title="<%= page.title %>"><%= page.title %></a></div>
  <div><b>本文链接: </b><a href="<%- config.root %><%- page.path %>" target="_blank" title="<%= page.title %>"><%- config.url %>/<%- page.path %></a>.</div>
  <div>本文由<a href="<%= config.root %>index.html" target="_blank" title="<%= config.author %>"><%= config.author %></a>创作和发表,采用<b>BY</b>-<b>NC</b>-<b>SA</b>国际许可协议进行许可,转载请注明作者及出处。</div>
</div>
```
### 5.13.2 Html 内容添加到post文尾
在your_theme/layout/post.ejs 的<%- page.content %>后面添加
```
<%- partial('_partial/post/copyright') %>
```
### 5.13.3 修改样式css
在/zilan/source/css/下创建 copyright.styl，并在head.ejs里引用   <%- css('css/copyright')%>
```
div.article-footer-copyright {
    margin: 2em 0 0;
    padding: .5em 1em;
    border-left: 3px solid #0085a1;
    background-color: #f9f9f9;
    list-style: none;
}
```
## 5.14 代码块复制功能

参考文章： [Hexo博客中加入代码块复制功能](https://qiming.info/Hexo%E5%8D%9A%E5%AE%A2%E4%B8%AD%E5%8A%A0%E5%85%A5%E4%BB%A3%E7%A0%81%E5%9D%97%E5%A4%8D%E5%88%B6%E5%8A%9F%E8%83%BD/)

## 5.15 搜索功能

借鉴了hexo-theme-next的[local-search](http://theme-next.iissnan.com/third-party-services.html#local-search)，使用的[hexo-generator-searchdb](https://github.com/theme-next/hexo-generator-searchdb)。
GitHub commit： [Add local search function](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/6b672a20aa23101bf0b17f7d790c1f5ad8422843)。

### 5.15.1 install hexo-generator-searchdb
``` bash
$ npm install hexo-generator-searchdb --save
```

或者在Hexo-theme-zilan/package.json文件中增加：
``` json
  "dependencies": {
    "hexo-generator-searchdb": "^1.1.0",
  }
```
``` bash
$ npm install
```

### 5.15.2 修改_config.yml

/Hexo-theme-zilan/_config.yml中增加设置：
```yml
# Search hexo-generator-searchdb  https://github.com/theme-next/hexo-generator-search
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
  content: true
```

### 5.15.3 write a search view. 
This is the place for displaying a search form and search results ;

#### search icon 界面
nav bar上添加search icon，在“岚”后面。
![search icon 界面](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/sarch%20icon%20view.png)
点击触发search popup显示。themes/zilan/layout/_partial/nav.ejs 添加：
```javascript
<!-- Search -->
<% var hasSearch = theme.swiftype_key || theme.algolia_search.enable || theme.tinysou_Key || theme.local_search.enable; %>
<% if (hasSearch) {%>
    <li class="menu-item menu-item-search">
    <% if (theme.swiftype_key) { %>
        <a href="javascript:;" class="st-search-show-outputs">
    <% } else if (theme.local_search.enable || theme.algolia_search.enable) { %>
        <a href="javascript:;" class="popup-trigger">
    <% } %>
        <% if (theme.menu_icons.enable) { %>
            <i class="menu-item-icon fa fa-search fa-fw"></i> <br />
        <% } %>
    </a>
    </li>
<% } %>
```

#### search popup 界面
themes/zilan/layout/layout.ejs 文件中增加search popup 界面，用来输入search string和search 结果。
```javascript
    <!-- Search popup-->
    <% var hasSearch = theme.swiftype_key || theme.algolia_search.enable || theme.tinysou_Key || theme.local_search.enable; %>
    <% if (hasSearch) {%>
      <div class="site-search">
      <% include ./_partial/search.ejs %>
      </div>
    <% } %>
```
![search popup 界面](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/search%20popup%20view.png)


### 5.15.4 write a search script. 
This script tells the browser how to grab search data and filter out contents what we're searching;
添加文件：
[themes/zilan/layout/_third-party/search/localsearch.ejs](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/blob/master/themes/zilan/layout/_third-party/search/localsearch.ejs)
### 5.15.5 tell hexo to connect the above two part.
themes/zilan/layout/layout.ejs
```javascript
    <!-- Search -->
    <% include ./_third-party/search/index.ejs %>
```
另外修了3个bug：
1. Fix Bug: [ajax xml parser error](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/6b672a20aa23101bf0b17f7d790c1f5ad8422843#diff-6f479bf13d3e26f8efd29d7b534db439L53)
2. Fix Bug: [input is null, so add /zilan/layout/_partial/search/localsearch.ejs inside "site-search"](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/6b672a20aa23101bf0b17f7d790c1f5ad8422843#diff-6f479bf13d3e26f8efd29d7b534db439R307)
3. Fix Bug: [click close icon not work](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/6b672a20aa23101bf0b17f7d790c1f5ad8422843#diff-6f479bf13d3e26f8efd29d7b534db439R302)
------

# 6 优化
## 6.1 优化文章链接
Hexo默认的文章链接形式为 your domain/year/month/day/postTitle.
这就是四级url，造成url过长，对搜索引擎是十分不友好的，我们可以改成 domain/postTitle 的形式。
编辑站点_config.yml文件，修改其中的permalink字段改为 ”permalink: :title.html“:
```yml
# permalink: :year/:month/:day/:title/  原来permalink的值
permalink: :title.html  # 现在permalink的值
```

## 6.2 设置站点地图 sitemap
可以看本文的[sitemap部分](http://liyuankun.top/Git-Pages-Jekyll-Hexo-Build-your-own-blog.html#sitemap)。

## 6.3 设置关键字keywords
1. 添加博客网站关键字
_config.yml中找到设置Site的部分添加keyword：
```yml
# Site settings
SEOTitle: Yuankun | Zilan
description: ""
keyword: Tech blog, travel notes, 游记, React, Redux, javascript, Frontend, Machine Learning
```
2. 添加博客文章关键字
```yml
---
title: ###
date: ###
categories: ###
tags: ###
keywords: ###
description: ###
---
```
## 6.4 添加 “nofollow” 标签，优化SEO权重
 [“nofollow” 标签的前世今生](https://ahrefs.com/blog/zh/nofollow-links/)。
 > 简单理解，[Nofollow标签](https://www.batmanit.com/p/439.html)，它常用于A标签的一个属性值，主要表达不要向某个特定链接传递权重，有的时候写在Meta标签中，则表示不要爬行网页上所有的链接，主要的表现形式为:
 > ① `<a rel="nofollow" href="">不要跟随链接</a>  `
 > ② `<meta name="robots" content="nofollow"/>  `
所以页面中包含的不想影响SEO权重的链接中，加上rel="nofollow"属性。例如评论，广告、新闻链接，站内联系页面，CMS程序多余入口中的链接都适合添加这个属性。

例如我把换页的链接中加上rel="nofollow"属性：
```html
<li class="previous"><a href="<%- config.root %><%- page.prev_link %>" rel="external nofollow">&larr;  <%- __('next')%></a></li>
```

# 7 遇到的坑

## 目录 无法跳转
href="#undefined"
可以看我这个commit是怎么修改的 : [fix bug:  the content href="#undefined"](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/3d1a7c1dbdf332ed9922e8d65f130e4c80237671)

参考这两个链接：
1 [_config.yml的markdown-it设置里面加上](https://github.com/Haojen/hexo-theme-Anisina/issues/34)，
```yml
markdown:
  anchors:
    level: 1
    permalinkSymbol: ''
```
 2 [package.json文件中删除"hexo-toc"](https://github.com/ppoffice/hexo-theme-icarus/issues/286)

## Disqus用username无法显示
这个在[“评论”](../#disqus)里已经说了.

## Category 分类页面分页只显示10个文章

虽然页面空间很大，但只显示10个文章列表就分页了：
![10个文章列表就分页](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Git-Pages-Jekyll-Hexo-Build-your-own-blog/category%E5%88%86%E9%A1%B5%E6%AF%8F%E9%A1%B5%E6%95%B0%E9%87%8F.png)

参考了别人的文章： [Hexo程序archive页面数量设置](http://www.yuzhewo.com/2015/11/21/Hexo%E7%A8%8B%E5%BA%8Farchive%E9%A1%B5%E9%9D%A2%E6%95%B0%E9%87%8F%E8%AE%BE%E7%BD%AE/)
但试了试不起作用。。。
这三个插件我之前就装有，可以在package.json里查看：
    "hexo-generator-archive": "^0.1.4",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-feed": "^1.2.2",
    "hexo-generator-index": "^0.2.0",

_config.yml文件中添加配置也加了：
```
# Pagination
## Set per_page to 0 to disable pagination
per_page: 11
pagination_dir: archives

## 主页每页显示文章数
index_generator:
    per_page: 12
## archive分页每页显示文章数
archive_generator:
  per_page: 15
  yearly: true
  monthly: true
  daily: false
## tag分页每页显示文章数
tag_generator:
    per_page: 16
## category分页每页显示文章数
category_generator: 
    per_page: 30
```
要说唯一不同的是，我之前的pagination_dir: archives，而查阅的其他文章中都是pagination_dir: page。
但我改成page也还是不起作用。。。。

等我发布（hexo deploy）出来后发现，其实除了tag_generator 和 archive_generator 没有成功以外，其他的设置都成功了，可能是本地模式（hexo server）下没有更新。

整个修改过程参考commit： [category 分页样式修改+分页每页数量](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/4607f6174e0615bf5bcc4bdada7715c6934b0d29)

## ERROR EISDIR: illegal operation on a directory

``` bash
➜  Hexo-theme-zilan git:(master) ✗ hexo g
INFO  Start processing
INFO  Files loaded in 564 ms
ERROR EISDIR: illegal operation on a directory, read
Error: EISDIR: illegal operation on a directory, read
```
查了下貌似和npm有关，但我试了试网上的方法并不起作用，但是这个错也不影响我的博客功能。暂且放下，找到方法了再更新。

## [DEP0061] DeprecationWarning: fs.SyncWriteStream is deprecated
[fs.SyncWriteStream is deprecated](../Hexo-node-28561-DEP0061-DeprecationWarning-fs-SyncWriteStream-is-deprecated.html)

## 其他小的修改

页面内容width修改，在大屏幕（>1800px 和> 2400px）下，页面内容更宽。
commit：t[he .container with responsive when screen width is larger than 1800px](https://github.com/CatherineLiyuankun/Hexo-theme-zilan/commit/64a23dad122b7cf59039d754125fc59307c6a9f1)

``` css
@media (min-width: 2400px) {
  .container {
    width: 2070px !important;
  }
}
@media (min-width: 1800px) {
  .container {
    width: 1770px;
  }
}
```
-----

# 参考文章：
* 阮一峰的文章 [搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)

* 这篇适合懒得学git的小白，完全把作者的模板拷贝过来改改参数： [利用 GitHub Pages 快速搭建个人博客](https://www.jianshu.com/p/e68fba58f75c)

* [手把手教你使用Hexo + Github Pages搭建个人独立博客](https://linghucong.js.org/2016/04/15/2016-04-15-hexo-github-pages-blog/)

* [Github Pages 搭建笔记](https://www.jianshu.com/p/ec7953b9e5ab)

* [How to Choose the Right Static Generator: Jekyll vs. Hugo vs. Hexo](https://www.techiediaries.com/jekyll-hugo-hexo/) 

* [Hexo-Next 添加 Gitment 评论系统](https://ryanluoxu.github.io/2017/11/27/Hexo-Next-%E6%B7%BB%E5%8A%A0-Gitment-%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F/)

* [打造个性超赞博客 Hexo + NexT + GitHub Pages 的超深度优化](https://io-oi.me/tech/hexo-next-optimization/)

* [NexT 主题使用](http://theme-next.iissnan.com/getting-started.html)

* [【搜索优化】Hexo-next百度和谷歌搜索优化](http://www.ehcoo.com/seo.html)

