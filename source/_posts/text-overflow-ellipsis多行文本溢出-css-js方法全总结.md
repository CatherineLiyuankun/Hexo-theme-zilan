---
title: 'text-overflow: ellipsis多行文本溢出...css/js方法全总结'
catalog: true
date: 2020-02-05 22:23:29
subtitle:
header-img:
tags:
- text-overflow
categories:
- TECH
- FrontEnd
- CSS
---

# 多行显示并在最后一行截断文字？
---
text-overflow基本知识请看上篇文章：
[text-overflow: ellipsis;什么时候可能不生效？](http://liyuankun.top/text-overflow-ellipsis-%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%AF%E8%83%BD%E4%B8%8D%E7%94%9F%E6%95%88%EF%BC%9F)

单行文字我们为了能够截断文字，使用了
```css
white-space: nowrap; // 强制文本在一行显示
```
如果我确实有多行并在最后一行截断文字显示的需求呢？怎么实现？
![multiline例子图片](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/text-overflow-ellipsis-%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%AF%E8%83%BD%E4%B8%8D%E7%94%9F%E6%95%88%EF%BC%9F/multiline%20ellipsis.png)

# 方法1 -Webkit-line-clamp property
**优点**: 最简单的方法
**缺点**: 但是很遗憾，它不支持跨浏览器（在Firefox和Internet Explorer中不起作用）。

> [-webkit-line-clamp](https://developer.mozilla.org/zh-CN/docs/Web/CSS/-webkit-line-clamp) CSS 属性 可以把 块容器 中的内容限制为指定的行数.

> 它只有在 display 属性设置成 -webkit-box 或者 -webkit-inline-box 并且 -webkit-box-orient 属性设置成 vertical时才有效果

> 在大部分情况下,也需要设置 overflow 属性为 hidden, 否则,里面的内容不会被裁减,并且在内容显示为指定行数后还会显示省略号(ellipsis ).

> 当他应用于锚(anchor)元素时,截取动作可以发生在文本中间,而不必在末尾.

使用方法：

```css
.block-with-text {
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;  
}
```
# 方法2 Text-overflow: -o-ellipsis-lastline
从10.60版开始，Opera增加了在多行块上剪切文本的功能。 老实说，我从未尝试过，理论上只在Opera 10.6以后可以使用，不建议使用。

# 方法3 JavaScript

```css
#block-with-text { 
    height: 3.6em; 
}
```
```JavaScript
function ellipsizeMultiLineText(id) {
    var element = document.getElementById(id);
    var words = element.innerHTML.split(' ');
    while(element.scrollHeight > element.offsetHeight) {
        words.pop();
        element.innerHTML = words.join(' ') + '...';
     }
}
ellipsizeMultiLineText('block-with-text');
```

# 方法4 纯CSS解决 & 跨浏览器

## 优点
1. 纯CSS
2. 自适应 Responsive 
3. 改变大小后或者 字体加载事件后 不需要重新计算
4. 跨浏览器

## 缺点
1. 文字小于指定行数的时候，我们需要一个背景色来掩盖‘…’
2. 我们需要空间来放‘…’, 而且如果父节点`overflow: hidden` 或者 `overflow: auto` 我们需要去掉style `margin-right: -1em;`.

## 实现方法
```css
/* styles for '...' */ 
.block-with-text {
  /* hide text if it more than N lines  */
  overflow: hidden;
  /* for set '...' in absolute position */
  position: relative; 
  /* use this value to count block height */
  line-height: 1.2em;
  /* max-height = line-height (1.2) * lines max number (3) */
  max-height: 3.6em; 
  /* fix problem when last visible word doesn't adjoin right side  */
  text-align: justify;  
  /* place for '...' */
  margin-right: -1em;
  padding-right: 1em;
}
/* create the ... */
.block-with-text:before {
  /* points in the end */
  content: '...';
  /* absolute position */
  position: absolute;
  /* set position to right bottom corner of block */
  right: 0;
  bottom: 0;
}
/* hide ... if we have text, which is less than or equal to max lines */
.block-with-text:after {
  /* points in the end */
  content: '';
  /* absolute position */
  position: absolute;
  /* set position to right bottom corner of text */
  right: 0;
  /* set width and height */
  width: 1em;
  height: 1em;
  margin-top: 0.2em;
  /* bg color = bg color under block */
  background: white;
}
```
## 实现原理
1. 大于3行时
:before 的内容"..." 在右下角, 因为文字被justify （text-align: justify;）不会看到文字与"..."之间有空隙:

![大于3行时1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/text-overflow-ellipsis-%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%AF%E8%83%BD%E4%B8%8D%E7%94%9F%E6%95%88%EF%BC%9F/more-3-lines.png)

去除CSS `text-align: justify;`会看到文字与"..."之间有空隙:
![大于3行时2](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/text-overflow-ellipsis-%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%AF%E8%83%BD%E4%B8%8D%E7%94%9F%E6%95%88%EF%BC%9F/more-3-lines-nonjustified.png)

2. 小于3行时
看不到"..." 
![小于3行时](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/text-overflow-ellipsis-%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%AF%E8%83%BD%E4%B8%8D%E7%94%9F%E6%95%88%EF%BC%9F/less-3-lines.png)

3. 等于3行时
看不到"..." 
![等于3行时](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/text-overflow-ellipsis-%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%AF%E8%83%BD%E4%B8%8D%E7%94%9F%E6%95%88%EF%BC%9F/equal-3-lines.png)


# 方法5 纯SCSS解决 & 跨浏览器
因为方法4中的缺点，所以写了个SCSS mixin。这样的话使用起来也更方便，也有复用性。

**CodePen** [multiline例子链接](https://codepen.io/catherineliyuankun/pen/poJzLKx)

```html
<p class="block-with-text">1.大于三行例子：最简单的方法，但是很遗憾，它不支持跨浏览器,在Firefox和Internet Explorer中不起作用. CSS属性可以把块容器中的内容限制为指定的行数.它只有在 display属性设置成-webkit-box或者-webkit-inline-box并且-webkit-box-orient属性设置成vertical时才有效果在大部分情况下,也需要设置overflow属性为hidden, 否则,里面的内容不会被裁减,并且在内容显示为指定行数后还会显示省略号(ellipsis )</p>
<p class="block-with-text">2.小于一行的例子，不会出现“...”在文末</p>
<p class="block-with-text" style="width: 250px;">3. 2.5 行的例子: 最简单的方法，但是很遗憾，它不支持跨浏览器,在Firefox和Internet Explorer中不起作用.</p>

```
```css
body {
  margin: 0;
  padding: 50px;
  font: 400 14px/1.2em sans-serif; 
  background: white;
}

p {
  width: 500px;
}

/* mixin for multiline */
@mixin multiLineEllipsis($lineHeight: 1.2em, $lineCount: 1, $bgColor: white){
  overflow: hidden;
  position: relative;
  line-height: $lineHeight;
  max-height: $lineHeight * $lineCount; 
  text-align: justify;
  margin-right: -1em;
  padding-right: 1em;
  &:before {
    content: '...';
    position: absolute;
    right: 0;
    bottom: 0;
  }
  &:after {
    content: '';
    position: absolute;
    right: 0;
    width: 1em;
    height: 1em;
    margin-top: 0.2em;
    background: $bgColor;
  }
}

.block-with-text {
  @include multiLineEllipsis($lineHeight: 1.2em, $lineCount: 2, $bgColor: white);  
}
```


---
# The reference link

[MDN text-overflow](https://developer.mozilla.org/en-US/docs/Web/CSS/text-overflow) 
