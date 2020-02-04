---
title: 'text-overflow: ellipsis;什么时候可能不生效？'
catalog: true
date: 2020-02-04 21:28:48
subtitle: 实现...文首截取&多行文本截取
header-img:
tags:
- Flexbox
categories:
- TECH
- FrontEnd
- CSS
---

# Ⅰ text-overflow: ellipsis;什么时候可能不生效？
---

1. 设置在width有效的元素上，并且设置必要的width。
    - 块级元素（block level element） width、height 属性默认有效.[example 1]
    - 内联元素（inline element 有的人也叫它行内元素）width、height 属性无效。[example 2]
    可以通过改变display，使得width、height属性有效。

    ```css
    display: block; //inline-block;
    ```

2. 要想这两个属性起真正的作用，需要配合：
    ```css
    overflow: hidden; // 超出文本的部分不显示
    white-space: nowrap; // 强制文本在一行显示
    ```

3. 在table内td除了满足前两个条件之外。要在table的样式里定义一个属性 ```table-layout:fixed```
[example 3] 

```html
<!-- example 1 -->
<div class="divTitle">div text-overflow: ellipsis;什么时候可能不生效？</div>
<!-- example 2 -->
<span class="spanTitle">span text-overflow: ellipsis;什么时候可能不生效？</span>
<!-- example 3 -->
<table>
  <tr>
    <td  class="box  ellipsis">
      <span>Here is some long content that doesn't fit.Here is some long content that doesn't fit</span>A
    </td>
  </tr>
</table>
```
    ```css
    // example 1
    .divTitle {
        width: 10px; // or other value
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
    }

    // example 2
    .spanTitle {
        display: inline-block;
        width: 10px;
        text-overflow: ellipsis;
        overflow: hidden;
        white-space: nowrap;
    }

    // example 3
    table { 
        table-layout:fixed; 
    }
    td { 
        text-overflow: ellipsis; 
        white-space: nowrap; 
        overflow: hidden; 
        width: 10px; 
    } 
    ```
---
# Ⅱ text-overflow的不同样式
---

- clip
这个关键字的意思是"在内容区域的极限处截断文本"，因此在字符的中间可能会发生截断。为了能在两个字符过渡处截断，你必须使用一个空字符串值 ('')(To truncate at the transition between two characters, the empty string value ('') must be used.)。此为默认值。
- ellipsis
这个关键字的意思是“用一个省略号 ('…', U+2026 HORIZONTAL ELLIPSIS)来表示被截断的文本”。这个省略号被添加在内容区域中，因此会减少显示的文本。如果空间太小到连省略号都容纳不下，那么这个省略号也会被截断。
- string 自定义字符串
string用来表示被截断的文本。字符串内容将被添加在内容区域中，所以会减少显示出的文本。如果空间太小到连省略号都容纳不下，那么这个字符串也会被截断。但是这个属性在很多浏览器中都不支持，要谨慎使用。

最有意思的是，如果结合使用
```
direction: rtl
```
可以指定截断文本是在文末还是在开头。

CodePen [text-overflow例子链接](https://codepen.io/catherineliyuankun/pen/gjzLav)
![text-overflow的不同样式例子图片](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/text-overflow-ellipsis-%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%AF%E8%83%BD%E4%B8%8D%E7%94%9F%E6%95%88%EF%BC%9F/text-overflow%E7%9A%84%E4%B8%8D%E5%90%8C%E6%A0%B7%E5%BC%8F.png)


```html
<p class="overflow-visible">overflow-visible Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
<p class="overflow-clip">overflow-clip Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
<p class="overflow-ellipsis">overflow-ellipsis Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
<p class="overflow-ellipsis first">overflow-ellipsis first Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
<p class="overflow-string">overflow-string Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
```

    ```css
    p {
    width: 200px;
    border: 1px solid;
    padding: 2px 5px;

    /* BOTH of the following are required for text-overflow */
    white-space: nowrap;
    overflow: hidden;
    }

    .overflow-visible {
    white-space: initial;
    }

    .overflow-clip {
    text-overflow: clip;
    }

    .overflow-ellipsis {
    text-overflow: ellipsis;
    }

    .overflow-ellipsis.first {
    direction: rtl;
    text-overflow: ellipsis;
    }

    .overflow-string {
    /* Not supported in most browsers, 
        see the 'Browser compatibility' section below */
    text-overflow: " [..]"; 
    }
    ```
---
# Ⅲ ...文首截断？
---

我们一般都会在文末截断...
如果我确实有文首截断的需求呢？怎么实现？

## 方法一

结合使用direction可以指定截断文本是在文末还是在开头。
```
direction: rtl; // at right end 文末
```
```
direction: ltr // at left end 开头
```

例子：
![文首截断例子图片](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/text-overflow-ellipsis-%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%AF%E8%83%BD%E4%B8%8D%E7%94%9F%E6%95%88%EF%BC%9F/reverse%20ellipsis%201.png)

```html
<p class="overflow-ellipsis">overflow-ellipsis Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
<p class="overflow-ellipsis first">overflow-ellipsis first Lorem ipsum dolor sit 
```
```css
p {
  width: 200px;
  border: 1px solid;
  padding: 2px 5px;

  /* BOTH of the following are required for text-overflow */
  white-space: nowrap;
  overflow: hidden;
}
.overflow-ellipsis {
  text-overflow: ellipsis;
}

.overflow-ellipsis.first {
  direction: rtl;
  text-overflow: ellipsis;
}
```

## 方法二

如果方法一在有些浏览器中不支持的话，可以使用：before添加content来实现。

![文首截断2例子图片](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/text-overflow-ellipsis-%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%AF%E8%83%BD%E4%B8%8D%E7%94%9F%E6%95%88%EF%BC%9F/reverse%20ellipsis%202.png)

CodePen [reverse ellipsis例子链接](https://codepen.io/catherineliyuankun/pen/ajGpvV)

---
# Ⅳ 多行显示并在最后一行截断文字？
---

上面我们为了能够截断文字，使用了
```css
white-space: nowrap; // 强制文本在一行显示
```
如果我确实有多行显示的需求呢？怎么实现？

![multiline例子图片](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/text-overflow-ellipsis-%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%8F%AF%E8%83%BD%E4%B8%8D%E7%94%9F%E6%95%88%EF%BC%9F/multiline%20ellipsis.png)

CodePen [multiline例子链接](https://codepen.io/catherineliyuankun/pen/poJzLKx)

```html
<p class="block-with-text">The Hitch Hiker's Guide to the Galaxy has a few things to say on the subject of towels. A towel, it says, is about the most massivelyuseful thing an interstellar hitch hiker can have. Partly it has great practical value - you can wrap it around you for warmth as you bound across the cold moons of  Jaglan Beta.</p>
<p class="block-with-text">Small text, less then one row. Without dottes.</p>
<p class="block-with-text" style="width: 250px;">2.5 lines example: A towel is about the most massively useful thing an interstellar hitch hiker can have</p>

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

[Pure CSS for multiline truncation with ellipsis](http://hackingui.com/front-end/a-pure-css-solution-for-multiline-text-truncation/) 
[MDN text-overflow](https://developer.mozilla.org/en-US/docs/Web/CSS/text-overflow) 
