---
title: React 16 - Hooks
catalog: true
date: 2019-10-21 11:45:22
subtitle:
header-img:
tags:
- React 16
categories:
- TECH
- FrontEnd
- React
---

# Hooks FAQ
觉得[Hooks FAQ](https://zh-hans.reactjs.org/docs/hooks-faq.html)里面回答了很多很实际的疑问。

## 生命周期方法要如何对应到 Hook？
* constructor：函数组件不需要构造函数。你可以通过调用 useState 来初始化 state。如果计算的代价比较昂贵，你可以传一个函数给 useState。

* getDerivedStateFromProps：改为 在渲染时 安排一次更新。

* shouldComponentUpdate：详见 下方 React.memo.

* render：这是函数组件体本身。

* componentDidMount, componentDidUpdate, componentWillUnmount：useEffect Hook 可以表达所有这些(包括 不那么 常见 的场景)的组合。

* componentDidCatch and getDerivedStateFromError：目前还没有这些方法的 Hook 等价写法，但很快会加上。

## 我该如何使用 Hook 进行数据获取？

该 [demo](https://codesandbox.io/s/jvvkoo8pq3) 会帮助你开始理解。欲了解更多，请查阅 [react-hooks-fetch-data](https://www.robinwieruch.de/react-hooks-fetch-data) 来了解如何使用 Hook 进行数据获取。

## Reference Links

- [新一代 React API — React Hooks React Conf 2018 React Today and Tomorrow 重點回顧](https://react.docschina.org/docs/portals.html)
- [官方文档英文版：hooks-intro](https://reactjs.org/docs/hooks-intro.html)
- [官方文档中文版：hooks](https://zh-hans.reactjs.org/docs/hooks-intro.html)
- [setTimeout in React Components Using Hooks](https://upmostly.com/tutorials/settimeout-in-react-components-using-hooks)
