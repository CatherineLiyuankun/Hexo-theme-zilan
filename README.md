> Ported Theme of [Hux Blog](https://github.com/Huxpro/huxpro.github.io), Thank [Huxpro](https://github.com/Huxpro) for designing such a flawless theme.
> 
> This Zilan theme created by [YuankunLi](https://catherineliyuankun.github.io/) modified from the original Porter [Kaijun](http://kaijun.rocks/hexo-theme-huxblog/) and [YuHsuan](http://beantech.org/)

# Demo [Live Demo](https://catherineliyuankun.github.io/)
[Zilan Blog](https://catherineliyuankun.github.io/)

# Usage
I publish the whole project for your convenience, so you can just follow the instruction down below, then you can easily customiz your own blog!

Let's begin!!!

## Init
```bash
git clone https://github.com/CatherineLiyuankun/Hexo-theme-zilan.git ./hexo-zilan
cd hexo-zilan
npm install
```

## Modify
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
async("//cdn.bootcss.com/anchor-js/1.1.1/anchor.min.js",function(){
        anchors.options = {
          visible: 'hover',
          placement: 'left',
          icon: 'ℒ'
        };
        anchors.add().remove('.intro-header h1').remove('.subheading').remove('.sidebar-container h5');
    })
```

## Hexo Basics
Some hexo command:
```bash
hexo new post "<post name>" # you can change post to another layout if you want
hexo clean && hexo generate # generate the static file
hexo server # run hexo in local environment
hexo deploy # hexo will push the static files automatically into the specific branch(gh-pages) of your repo!
```


Please [Star](https://github.com/catherineliyuankun/hexo-theme-zilan) this Project if you like it! [Follow](https://github.com/catherineliyuankun) would also be appreciated!
Peace!
