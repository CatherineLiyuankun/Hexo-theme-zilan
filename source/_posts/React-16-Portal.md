---
title: React 16 - Portal
catalog: true
date: 2019-09-03 11:07:35
subtitle:
header-img:
tags:
- React 16
categories:
- TECH
- FrontEnd
- React
---

转[传送门：React Portal](https://zhuanlan.zhihu.com/p/29880992)， 在这个基础上做了小的修改。

似乎所有说React Portal都直接用Portal这个单词，没听过这词的朋友可能觉得不知所云，其实，Portal可以有一个很形象的翻译——“传送门”。

## 什么是传送门？
曾经有一款游戏就叫做Portal，玩家手上一杆很厉害很科幻的枪，朝墙上开一枪，就可以开出两个“传送门”，人钻进这个传送门，可以从另一个传送门里走出来，也就是说，两个不同位置的传送门之间形成了对接。

![传送门](https://pic4.zhimg.com/80/v2-a650d2d42e0ed880c4413340ec961a27_hd.jpg)

如果还不明白Portal是啥，那就拿范冰冰在《X战警：逆转未来》所演角色的GIF动图来看吧。
![《X战警：逆转未来》](https://pic1.zhimg.com/v2-89a003124def7b845832f3789ba8c4e8_b.jpg)



你看一个哨兵机器人扑过来攻击一个X战警，范冰冰从一个传送门里神速穿越而来，顺手又甩出两个传送门，让哨兵机器人扑进了一个传送门，从另一个传送门一个踉跄掉了出来，从而救了那个X战警。

现在明白Portal是怎么回事了吧。

## 为什么React需要传送门？
React Portal之所以叫Portal，因为做的就是和“传送门”一样的事情：**render到一个组件里面去，实际改变的是网页上另一处的DOM结构**。

在React的世界中，一切都是组件，用组件可以表示一切界面中发生的逻辑，不过，有些特例处理起来还比较麻烦，比如，某个组件在渲染时，在某种条件下需要显示一个对话框(Dialog)，这该怎么做呢？

最直观的做法，就是直接在JSX中把Dialog画出来，像下面代码的样子。
``` JavaScript
<div class="foo">
   <div> ... </div>
   { needDialog ? <Dialog /> : null }
</div>
```
问题是，我们写一个Dialog组件，就这么渲染的话，Dialog最终渲染产生的HTML就存在于上面JSX产生的HTML一起了，类似下面这样。
``` JavaScript

<div class="foo">
   <div> ... </div>
   <div class="dialog">Dialog Content</div>
</div>
```
可是问题来了，对于对话框，从用户感知角度，应该是一个独立的组件，通常应该显示在屏幕的最中间，现在Dialog被包在其他组件中，要用CSS的position属性控制Dialog位置，就要求从Dialog往上一直到body没有其他postion是relative的元素干扰，这……有点难为作为通用组件的Dialog，毕竟，谁管得住所有组件不用position呢。

还有一点，Dialog的样式，因为包在其他元素中，各种样式纠缠，CSS样式太容易搞成一坨浆糊了。

### When to use React传送门？【liyuankun 增加】
当父组件样式有 overflow: hidden 或者 z-index，但是你需要子组件看起来“break out”它所在的container. 例如dialogs, hover cards 和 tool-tips.

### React 16 之前怎么实现传送门？
看样子这样搞局限很多啊，行不通，有没有其他办法？

#### 通过Redux或者其他通讯方式
有一个其他办法，就是在React组件树的最顶层留一个元素专属于Dialog，然后通过Redux或者其他什么通讯方式给这个Dialog发送信号，让Dialog显示或者不显示。
![Dialog](https://pic1.zhimg.com/80/v2-4022e89a8d7a22461e426cf6c653e18c_hd.jpg)
这种方法看起来还凑合着，但是，就这点事还要动用Redux有点高射炮打蚊子，而且，要控制两个不用位置的组件，好麻烦。

而且，如果我们把Dialog做成一个通用组件，希望里面的内容完全定制，这招就更加麻烦了。
``` JavaScript
<div class="foo">
  <div> ... </div>
  { needDialog ? 
    <Dialog> 
       <header>Any Header</header>
       <section>Any content</section>
    </Dialog>
    : null }
</div>
```
像上面那样，我们既希望在组件的JSX中选择使用Dialog，把Dialog用得像一个普通组件一样，但是又希望Dialog内容显示在另一个地方，就需要Portal上场了。

Portal就是建立一个“传送门”，让Dialog这样的组件在表示层和其他组件没有任何差异，但是渲染的东西却像经过传送门一样出现在另一个地方。

#### React 15 API

React在v16之前的传送门实现方法
在v16之前，实现“传送门”，要用到两个秘而不宣的React API

- unstable_renderSubtreeIntoContainer
- unmountComponentAtNode

第一个unstable_renderSubtreeIntoContainer，都带上前缀unstable了，就知道并不鼓励使用，但是没办法啊，不用也得用，还好React一直没有deprecate这个API，一直挺到v16直接支持portal。这个API的作用就是建立“传送门”，可以把JSX代表的组件结构塞到传送门里面去，让他们在传送门的另一端渲染出来。

第二个unmountComponentAtNode用来清理第一个API的副作用，通常在unmount的时候调用，不调用的话会造成资源泄露的。

一个通用的Dialog组件的实现差不多是这样，注意看renderPortal中的注释。
``` JavaScript
import React from 'react';
import {unstable_renderSubtreeIntoContainer, unmountComponentAtNode} 
  from 'react-dom';

class Dialog extends React.Component {
  render() {
    return null;
  }

  componentDidMount() {
    const doc = window.document;
    this.node = doc.createElement('div');
    doc.body.appendChild(this.node);

    this.renderPortal(this.props);
  }

  componentDidUpdate() {
    this.renderPortal(this.props);
  }

  componentWillUnmount() {
    unmountComponentAtNode(this.node);
    window.document.body.removeChild(this.node);
  }

  renderPortal(props) {
    unstable_renderSubtreeIntoContainer(
      this, //代表当前组件
      <div class="dialog">
        {props.children}
      </div>, // 塞进传送门的JSX
      this.node // 传送门另一端的DOM node
    );
  }
}
```

首先，render函数不要返回有意义的JSX，也就说说这个组件通过正常生命周期什么都不画，要是画了，那画出来的HTML/DOM就直接出现在使用Dialog的位置了，这不是我们想要的。

在componentDidMount里面，利用原生API来在body上创建一个div，这个div的样式绝对不会被其他元素的样式干扰。

然后，无论componentDidMount还是componentDidUpdate，都调用一个renderPortal来往“传送门”里塞东西。

总结，这个Dialog组件做得事情是这样：

1. 它什么都不给自己画，render返回一个null就够了；
2. 它做得事情是通过调用renderPortal把要画的东西画在DOM树上另一个角落。

在renderPortal中，利用unstable_renderSubtreeIntoContainer函数往直前创建的div里塞JSX，这里我们用的JSX是这样。
``` JavaScript
  <div class="dialog">
       {props.children}
   </div>
```
因为是吧children画出来，所以使用Dialog可以加上任意的子组件。
``` JavaScript
 <Dialog>
      What ever shit
      <div>Hello</div>
      <p>World</p>
  </Dialog>
```
你看，所谓React Portal，就是能够表面上渲染在一个地方，实际上渲染到了另一个地方。
![Portal](https://pic4.zhimg.com/80/v2-60771cc0b94e780ca29bdd72f2761d57_hd.jpg)

是不是感觉好厉害，不光好厉害，而且像Dialog这样的场景Portal简直就是必不可少。

到了v16，React干脆直接支持Portal，当然，v15还将被使用一段时间，所以大家看了上面的内容也不算浪费时间:-)

## React v16的Portal支持

在v16中，使用Portal创建Dialog组件简单多了，不需要牵扯到componentDidMount、componentDidUpdate，也不用调用API清理Portal，关键代码在render中，像下面这样就行。
``` JavaScript
import React from 'react';
import {createPortal} from 'react-dom';

class Dialog extends React.Component {
  constructor() {
    super(...arguments);

    const doc = window.document;
    this.node = doc.createElement('div');
    doc.body.appendChild(this.node);
  }

  render() {
    return createPortal(
      <div class="dialog">
        {this.props.children}
      </div>, //塞进传送门的JSX
      this.node //传送门的另一端DOM node
    );
  }

  componentWillUnmount() {
    window.document.body.removeChild(this.node);
  }
}
```
v16提供createPortal函数来创建“传送门”，我个人觉得这个函数应该叫renderPortal好一些，因为组件的render函数除了mount时会被调用，update时也会被调用，update时还叫createPortal有点不大合适。

## 穿越Portal的事件冒泡
v16之前的React Portal实现方法，有一个小小的缺陷，就是Portal是单向的，内容通过Portal传到另一个出口，在那个出口DOM上发生的事件是不会冒泡传送回进入那一端的。

也就是说，这样的代码。
``` JavaScript
<div onClick={onDialogClick}>   
   <Dialog>
     What ever shit
   </Dialog>
</div>
```
在Dialog画出的内容上点击，onDialogClick是不会被触发的。

当然，这只是一个小小的缺陷，大部分场景下事件不传过来也没什么大问题。

在v16中，通过Portal渲染出去的DOM，事件是会冒泡从传送门的入口端冒出来的，上面的onDialogClick也就会被调用到了。

### why事件冒泡可以到react parent 【liyuankun 增加】

可以看这个例子：[Dialog 嵌套 Dialog demo](https://codepen.io/catherineliyuankun/pen/oNvpxKv)

从真实的DOM结构上来看，Dialog组件中的onClick事件不应该被
```html
<div class="container">Here contain Dialog:</div>
```
组件捕获。
但从虚拟DOM的结构上来看，Dialog却是"container"组件的子节点，事件冒泡是遵循虚拟DOM的.

真实的DOM结构:
![真实的DOM结构1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/React-16-Portal/Real%20Dom%201.png)
![真实的DOM结构2](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/React-16-Portal/Real%20Dom%202.png)

虚拟DOM的结构:
``` JavaScript
    <div onClick={onDialogClick}>
      <div className="container">
        Here contain Dialog:
      </div>
      <Dialog onClick={onDialog1Click}>
         <div>Dialog 1</div>
          <Dialog onClick={onDialog2Click}>
            <div>Dialog 2 Inside Dialog 1 </div>    
          </Dialog>
      </Dialog>
    </div>
```



## 总结
React v16直接支持Portal，是因为Portal这个功能真的是必不可少，不然对话框这样的场景都没法应付。

## Reference Links

- [官网文档中文版](https://react.docschina.org/docs/portals.html)
- [传送门：React Portal](https://zhuanlan.zhihu.com/p/29880992)
- [Understanding Portals in React](https://www.beautifulcode.co/blog/46-understanding-portals-in-react)


