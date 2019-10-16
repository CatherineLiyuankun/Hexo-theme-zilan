---
title: "Responsive web - Flexbox"
catalog: true
date: 2019-10-15 13:18:56
subtitle:
header-img:
tags:
- Flexbox
categories:
- TECH
- FrontEnd
- CSS
- Flexbox
---

## 基础教程：
- [ 官方文档 A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) 
- [ 阮一峰 Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html) 

但是看完还是有些不懂的地方：
## Flex Basis 具体的含义:
- [ flex-basis MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-basis)
 以及和width的区别：
- [ Flex Basis与Width的区别](https://www.jianshu.com/p/17b1b445ecd4)
- [ The Difference Between Width and Flex Basis](https://gedd.ski/post/the-difference-between-width-and-flex-basis/) 


## flex-grow、flex-shrink、flex-basis 是怎么此消彼长的
如果分配剩余空间？
- [ 深入理解css3中的flex-grow、flex-shrink、flex-basis](https://zhoon.github.io/css3/2014/08/23/flex.html) 

## 小实践：
Code Pen - Flexbox Form:
[Flexbox Form](https://codepen.io/catherineliyuankun/pen/dyyMKzW)
有个困惑， 比如.wrapper 的width只有比如100px; 但是lable/span又不想换行，这时lable的flex-grow:1,.date的flex-grow:3. 也就是比例是1：3，lable就会被截断。 当然如果flex-grow:1都为1，input和lable同比例缩小，会解决。
但是在lable不长的情况下，不想让lable 和 input 部分的比例为1：1.

当然通过 media query 来实现修改flex的值，但是如果我想以.wrapper的宽度来修改flex-grow的值要怎么做呢？或者以lable的长度来修改.date的flex-grow的值？（lable长的时候，lable: .date = 1：1，lable短的时候，1：3）?

```CSS
@media screen and (min-width: 768px) {
   	.form-row > .date {
    	flex: 3;  
   }
  }
 @media screen and (min-width: 992px) {
   	.form-row > .date {
    	flex: 4;  
   }
  }
```

```CSS
  .form-row > span {
    display: inline-block;
    padding: .5em 1em .5em 0;
    flex: 1;
    white-space: nowrap;
    overflow: hidden;
  }
  .form-row > .date {
    display: flex;
    align-items: baseline;
    flex: 3;
  }
```
# Reference Links:

- [ 官方文档 A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) 
- [ 阮一峰 Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html) 
- [ How to Align Form Elements with Flexbox](https://www.quackit.com/css/flexbox/tutorial/align_form_elements_with_flexbox.cfm) 
- [ Flex Basis与Width的区别](https://www.jianshu.com/p/17b1b445ecd4)
- [ The Difference Between Width and Flex Basis](https://gedd.ski/post/the-difference-between-width-and-flex-basis/) 
