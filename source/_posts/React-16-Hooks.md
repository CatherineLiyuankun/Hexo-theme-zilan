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

* constructor：函数组件不需要构造函数。你可以通过调用 `useState` 来初始化 state。如果计算的代价比较昂贵，你可以传一个函数给 `useState`。

* `getDerivedStateFromProps`：改为 在渲染时 安排一次更新。

* `shouldComponentUpdate`：详见 下方 React.memo.

* render：这是函数组件体本身。

* `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`：`useEffect` Hook 可以表达所有这些(包括 不那么 常见 的场景)的组合。

* `componentDidCatch` and `getDerivedStateFromError`：目前还没有这些方法的 Hook 等价写法，但很快会加上。

### On Mounting (componentDidMount)

生命周期方法 `componentDidMount` 会在第一次render完成后立即调用。以前有一个 componentWillMount 会在第一次render之前调用，但它被认为是传统方法，不建议在较新版本的 React 中使用。

```JavaScript
const FunctionalComponent = () => {
 React.useEffect(() => {
   console.log("Hello");
 }, []); // [] 作为依赖数组，与componentDidMount等效，会在第一次render完成后立即调用
 return <h1>Hello, World</h1>;
};
```

取代 `componentDidMount`，我们使用第二个参数为 `[]` 的 `useEffect` hook。 `useState` hook的第二个参数通常是一个包含变化状态的数组，而 `useEffect` 只会在这些选定的变化中被调用。但如果是像本例这样的空数组，则会在挂载时调用一次。这可以完美替代 `componentDidMount`。

```JavaScript
class ClassComponent extends React.Component {
 componentDidMount() {
   console.log("Hello");
 }
 render() {
   return <h1>Hello, World</h1>;
 }
}
```

这里发生的事情基本上是一样的：`componentDidMount` 是一个生命周期方法，在第一次render后会被调用一次。

### On Unmounting (componentWillUnmount)

```JavaScript
class ClassComponent extends React.Component {
 componentWillUnmount() {
   console.log("Bye");
 }
 render() {
   return <h1>Bye, World</h1>;
 }
}
```

```JavaScript
const FunctionalComponent = () => {
 React.useEffect(() => {
   return () => {       // 返回一个函数
     console.log("Bye");
   };
 }, []);
 return <h1>Bye, World</h1>;
};
```

好消息是，我们也可以使用 `useState` 钩子来卸载。但要注意，语法有些不同。你需要做的是在 `useEffect` 函数中返回一个在卸载时运行的`函数`。这在需要清理订阅（如 `clearInterval` 函数）时尤其有用，否则会在较大的项目中造成严重的内存泄漏。使用 useEffect 的一个好处是，我们可以在同一个地方编写挂载和卸载函数。例如：

```JavaScript
  useEffect(() => {
    // Function to be called when the component mounts
    const handleEvent = (event) => {
      console.log('Event occurred:', event);
    };

    // 挂载 Add event listener when the component mounts
    window.addEventListener('yourEventType', handleEvent);

    // 卸载 Clean up the event listener when the component unmounts
    return () => {
      window.removeEventListener('yourEventType', handleEvent);
    };
  }, []); // Empty dependency array means this effect runs only once (on mount)
```

```JavaScript
// custom hook
export const useDelayedRender = (delayTime: number) => {
  const [shouldRender, setShouldRender] = useState(false)

  useEffect(() => {
    const timeoutId = setTimeout(() => { // 挂载 
      setShouldRender(true)
    }, delayTime)

    return () => clearTimeout(timeoutId) // 卸载
  }, [delayTime])

  return shouldRender
}
```

```JavaScript
  useEffect(() => {
    // Function to be called at intervals
    const updateValue = () => {
      setValue((prevValue) => prevValue + 1);
    };

    // 挂载 Set an interval when the component mounts
    const intervalId = setInterval(updateValue, 1000); // Replace 1000 with your desired interval in milliseconds

    // Clean up the interval when the component unmounts
    return () => {
      clearInterval(intervalId); // 卸载
    };
  }, []); // Empty dependency array means this effect runs only once (on mount)
```

## 我该如何使用 Hook 进行数据获取？

该 [demo](https://codesandbox.io/s/jvvkoo8pq3) 会帮助你开始理解。欲了解更多，请查阅 [react-hooks-fetch-data](https://www.robinwieruch.de/react-hooks-fetch-data) 来了解如何使用 Hook 进行数据获取。

## Reference Links

* [新一代 React API — React Hooks React Conf 2018 React Today and Tomorrow 重點回顧](https://react.docschina.org/docs/portals.html)
* [官方文档英文版：hooks-intro](https://reactjs.org/docs/hooks-intro.html)
* [官方文档中文版：hooks](https://zh-hans.reactjs.org/docs/hooks-intro.html)
* [setTimeout in React Components Using Hooks](https://upmostly.com/tutorials/settimeout-in-react-components-using-hooks)
