---
title: "[Hexo] Theme Zilan"
catalog: true
date: 2018-08-18 10:51:24
subtitle: "This is hexo theme Demo."
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/hexotheme/hexo-cover.png"
tags:
- Hexo
- Blog
categories:
- TECH
- Hexo
---
> Ported Theme of [Hux Blog](https://github.com/Huxpro/huxpro.github.io), Thank [Huxpro](https://github.com/Huxpro) for designing such a flawless theme.
> 
> This Zilan theme created by [YuankunLi](https://catherineliyuankun.github.io/) modified from the original Porter [Kaijun](http://kaijun.rocks/hexo-theme-huxblog/) and [YuHsuan](http://beantech.org/)

# Demo [Live Demo](https://catherineliyuankun.github.io/)
---
[Zilan Blog](https://catherineliyuankun.github.io/)

# Usage
---
I publish the whole project for your convenience, so you can just follow the instruction down below, then you can easily customiz your own blog!

Let's begin!!!

## Init
---
```bash
git clone https://github.com/catherineliyuankun/hexo-theme-zilan.git ./hexo-zilan
cd hexo-zilan
npm install
```

## Modify
---
Modify `_config.yml` file with your own info.
Especially the section:
### Deployment
Replace to your own repo!
```yml
deploy:
  type: git
  repo: https://github.com/<yourAccount>/<repo>
  branch: <your-branch>
```

### Sidebar settings
Copy your avatar image to `<root>/img/` and modify the `_config.yml`:
```yml
sidebar: true    # whether or not using Sidebar.
sidebar-about-description: "<your description>"
sidebar-avatar: img/<your avatar path>
```
and activate your personal widget you like
```yml
widgets:         # here are widget you can use, you can comment out
- featured-tags
- short-about
- recent-posts
- friends-blog
- archive
- category
```
if you want to add sidebar widget, please add at `layout/_widget`.
### Signature Setup
Copy your signature image to `<root>/img/signature` and modify the `_config.yml`:
```yml
signature: true   # show signature
signature-img: img/signature/<your-signature-ID>
```
### Go to top icon Setup
My icon is using iron man, you can change to your own icon at `css/image`.

### Post tag and category
You can decide to show post tags and categories or not.
```yml
home_posts_tag: true
home_posts_category: true
```
![home_posts_tag-true](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/hexotheme/home_posts_tag-true.png)
```yml
home_posts_tag: false
home_posts_category: false
```
![home_posts_tag-false](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/hexotheme/home_posts_tag-false.png)

### Page Header category
You can decide to show page_header categories or not.
```yml
page_header_category: true
```
![page_header_category-true](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/hexotheme/page_header_category-true.png)
```yml
page_header_category: false
```
![page_header_category-false](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/hexotheme/page_header_category-false.png)

### forkme
forkme: false # Fork me on GitHub
forkme-url: https://github.com/CatherineLiyuankun/Hexo-theme-zilan # GitHub url

### donate
donate: true
donate-alipay: https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/base/alipay.png
donate-wechat: https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/base/wechatpay.png

### Markdown render
My markdown render engine plugin is [hexo-renderer-markdown-it](https://github.com/celsomiranda/hexo-renderer-markdown-it).
```yml
# Markdown-it config
## Docs: https://github.com/celsomiranda/hexo-renderer-markdown-it/wiki
markdown:
  render:
    html: true
    xhtmlOut: false
    breaks: true
    linkify: true
    typographer: true
    quotes: '“”‘’'
```
and if you want to change the header anchor 'ℒ', you can go to `layout/post.ejs` to change it.
```javascript
async("https://cdn.bootcss.com/anchor-js/1.1.1/anchor.min.js",function(){
        anchors.options = {
          visible: 'hover',
          placement: 'left',
          icon: ℒ // this is the header anchor "unicode" icon
        };
```

## Hexo Basics
---
Some hexo command:
```bash
hexo new post "<post name>" # you can change post to another layout if you want
hexo clean && hexo generate # generate the static file
hexo server # run hexo in local environment
hexo deploy # hexo will push the static files automatically into the specific branch(gh-pages) of your repo!
```

# Start your own blog!
---
<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>
<!-- Place this tag where you want the button to render. -->

Please <a class="github-button" href="https://github.com/catherineliyuankun/hexo-theme-zilan.git" data-icon="octicon-star" aria-label="Star Li,Yuankun/hexo-theme-zilan on GitHub">Star</a> this Project if you like it! <a class="github-button" href="https://github.com/CatherineLiyuankun" aria-label="Follow @CatherineLiyuankun on GitHub">Follow</a> would also be appreciated!
Peace!
