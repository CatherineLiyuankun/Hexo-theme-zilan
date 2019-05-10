---
title: Force IE rerender
catalog: true
date: 2019-04-24 16:09:43
subtitle:
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Force-IE-rerender/header-IE.jpg"
tags:
- IE
categories:
- TECH
- FrontEnd
- IE issues
---

# The height of same row is different of grid

![compare](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Force-IE-rerender/compare.png)
![mark](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Force-IE-rerender/mark.png)
![html](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Force-IE-rerender/html.png)

# Fix by javascript code

迫使IE重新render

```javascript
if (ISIE) { //judge whether it is IE
    window.setTimeout(function() {
        el.style.zoom = el.style.zoom == '1' ? '100%' : '1';
    }, 100);
}
```