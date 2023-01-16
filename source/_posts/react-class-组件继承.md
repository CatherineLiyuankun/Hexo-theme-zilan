---
title: react class 组件继承
catalog: true
date: 2023-01-16 22:26:42
subtitle:
header-img:
tags:
- React
categories:
- TECH
- FrontEnd
- React
---

## react class 组件继承坑点

A组件 extends B 组件，方法调用和改写

- A组件中要通过this.b调用B组件的b方法，则b方法的写法可以是箭头函数或者非箭头函数，但如果A组件中要通过super.b调用B组件中的b方法，则b的写法必须是非箭头函数。
- 如果A组件中只是要重写b方法，则b方法在B组件中如果是箭头函数的写法，在A组件中改写也必须是箭头函数的改写形式。
- 如果A组件中只是要重写b方法，则b方法在B组件中如果是非箭头函数的写法，在A组件中改写可以是箭头函数，也可以是非箭头函数。

## 参考文章

- [react class 组件继承坑点](https://juejin.cn/post/7049552567746953230)
- [探索 React 中 es6 的继承机制](https://juejin.cn/post/6844903495116521486)
- [面试官问：JS的继承](https://zhuanlan.zhihu.com/p/57336944)

- [10种React组件之间通信的方法](https://zhuanlan.zhihu.com/p/326254966)
- [Create Ref using React.createRef without using constructor in React?](https://stackoverflow.com/questions/54257762/create-ref-using-react-createref-without-using-constructor-in-react)
