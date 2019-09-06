---
title: React 16 - Error Handling
catalog: true
date: 2019-09-03 11:06:09
subtitle:
header-img:
tags:
- React 16
categories:
- TECH
- FrontEnd
- React
---



## React 15：
渲染过程中有出错，直接crash整个页面，并且错误信息不明确，可读性差.
一旦某个组件发生错误，整个组件树将会从根节点被unmount下来。

``` JavaScript
class BuggyCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { counter: 0 };
    this.handleClick = this.handleClick.bind(this);
  }
  
  componentWillMount() {
    throw new Error('I am crash');
  }
  
  handleClick() {
    this.setState(({counter}) => ({
      counter: counter + 1
    }));
  }
  
  render() {
    if (this.state.counter === 5) {
      // Simulate a JS error
      throw new Error('I crashed!');
    }
    return <h1 onClick={this.handleClick}>{this.state.counter}</h1>;
  }
}

function App() {
  return (
    <div>
      <p>
        <b>
          This is an example of error boundaries in React 16.
          <br /><br />
          Click on the numbers to increase the counters.
          <br />
          The counter is programmed to throw when it reaches 5. This simulates a JavaScript error in a component.
        </b>
      </p>
      <hr />
        <p>These two counters are inside the same error boundary. If one crashes, the error boundary will replace both of them.</p>
        <BuggyCounter />
      <hr />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

### [demo地址](https://codepen.io/anon/pen/ErBjZM?editors=0010)

比如上面这个App，可以看到子组件BuggyCounter出了点问题，在没有Error Boundary的时候，整个App都会crash掉，所以显示白屏。

## React 16：
React之前没有提供一种合适的处理组件错误的方法，而React16.0中通过Error Boundaries来处理组件内部的错误，从而可以修正错误组件。
用于捕获子组件树的组件异常（即错误边界只可以捕获组件在树中比他低的组件错误。），记录错误并展示一个用Error Boundary提供的内容替代错误组件。

### 捕获范围：

渲染期间
生命周期内
整个组件树构造函数内

### 如何使用：
最佳实践：
- 如果一个 class 组件中定义了 static getDerivedStateFromError() 或 componentDidCatch() 这两个生命周期方法中的任意一个（或两个）时，那么它就变成一个错误边界。当抛出错误后，请使用 static getDerivedStateFromError() 渲染备用 UI ，使用 componentDidCatch() 打印错误信息。
``` JavaScript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // 更新 state 使下一次渲染能够显示降级后的 UI
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    // 你同样可以将错误日志上报给服务器
    logErrorToMyService(error, info);
  }

  render() {
    if (this.state.hasError) {
      // 你可以自定义降级后的 UI 并渲染
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children; 
  }
}
```
- 将ErrorBoundary抽象为一个公用的组件类， 我们可以在容易出错的组件外使用ErrorBoundary将它包裹起来。
``` JavaScript
<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>
```

### componentDidCatch（）生命周期函数

componentDidCatch是一个新的生命周期函数，当组件有了这个生命周期函数，就成为了一个Error Boundaries。下面我们来看componnetDidCatch()中的参数：
``` JavaScript
componentDidCatch(error, info) {
}
```
error参数，表示的是被抛出的错误的信息，而info是一个对象包含了组件堆栈中的信息（也就是在发生错误的子组件中层层传递错误信息，到顶层的Error Boundaries，每一层中的组件名）。

### Component Stack Traces

下面我们来看组件堆栈轨迹，我们假设这样一个结构：
``` JavaScript
<App>
  <div>
      <ErrorBoundary>
        <Child></Child>
      </ErrorBoundary>
  </div>
</App>
```

如果在Child组件中发生了js错误，那么堆栈的报错信息应该如下：
``` JavaScript
the error is located at :
     in Child  (created by App)
     in ErrorBoundary(created by App)
     in div (created by App)
     in App
```
如果需要报错信息显示错误组件所在的具体的行数和位置，可以使用babel-plugin-transform-react-jsx-source插件。


``` JavaScript
// 先定一个组件ErrorBoundary
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { error: null, errorInfo: null };
  }
  
  componentDidCatch(error, errorInfo) {
    // Catch errors in any components below and re-render with error message
    this.setState({
      error: error,
      errorInfo: errorInfo
    })
    // You can also log error messages to an error reporting service here
  }
  
  render() {
    // 有错误的时候展示回退
    if (this.state.errorInfo) {
      // Error path
      return (
        <div>
          <h2>Something went wrong.</h2>
          <details style={{ whiteSpace: 'pre-wrap' }}>
            {this.state.error && this.state.error.toString()}
            <br />
            {this.state.errorInfo.componentStack}
          </details>
        </div>
      );
    }
    // 正常的话，直接展示组件
    return this.props.children;
  }  
}

class BuggyCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { counter: 0 };
    this.handleClick = this.handleClick.bind(this);
  }
  
  componentWillMount() {
    throw new Error('I am crash');
  }
  
  handleClick() {
    this.setState(({counter}) => ({
      counter: counter + 1
    }));
  }
  
  render() {
    if (this.state.counter === 5) {
      // Simulate a JS error
      throw new Error('I crashed!');
    }
    return <h1 onClick={this.handleClick}>{this.state.counter}</h1>;
  }
}

function App() {
  return (
    <div>
      <p>
        <b>
          This is an example of error boundaries in React 16.
          <br /><br />
          Click on the numbers to increase the counters.
          <br />
          The counter is programmed to throw when it reaches 5. This simulates a JavaScript error in a component.
        </b>
      </p>
      <hr />
        <ErrorBoundary>
        <p>These two counters are inside the same error boundary. If one crashes, the error boundary will replace both of them.</p>
        <BuggyCounter />
        </ErrorBoundary>
      <hr />

    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

### [demo地址](https://codepen.io/gaearon/pen/wqvxGa?editors=0010)


可以看到加上Error Boundary之后，除了出错的组件，其他的地方都不受影响。

而且它很清晰的告诉我们是哪个组件发生了错误。

### 注意事项：

Error Boundary无法捕获下面的错误：

1. 事件函数里的错误
``` JavaScript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { error: null };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    try {
      // Do something that could throw
    } catch (error) {
      this.setState({ error });
    }
  }

  render() {
    if (this.state.error) {
      return <h1>Caught an error.</h1>
    }
    return <div onClick={this.handleClick}>Click Me</div>
  }
}
```
上面的例子中，handleClick方法里面发生的错误，Error Boundary是捕获不到的。因为它不发生在渲染阶段，所以采用try/catch来捕获。

2. 异步代码（例如setTimeout 或 requestAnimationFrame 回调函数）
``` JavaScript
class A extends React.Component {
     render() {
        // 此错误无法被捕获，渲染时组件正常返回 `<div></div>`
        setTimeout(() => {
            throw new Error('error')
        }, 1000)
        return (
            <div></div>
        )
    }
}
```
3. 服务端渲染

因为服务器渲染不支持Error Boundary

4. Error Boundary自身抛出来的错误 （而不是其子组件）

### 错误边界放在哪里?
一般来说，有两个地方：

1. 可以放在顶层，告诉用户有东西出错。但是我个人不建议这样，这感觉失去了错误边界的意义。因为有一个组件出错了，其他正常的也没办法正常显示了

2. 包在子组件外面，保护其他应用不崩溃。



## Reference Links

- [官网文档中文版](https://react.docschina.org/docs/error-boundaries.html)
- [React Error Handling in React 16](https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html)
- [React16新特性](https://my.oschina.net/u/2332658/blog/3019283)
- [React 16 新特性全解（上）](https://zhuanlan.zhihu.com/p/57544233)
- [React 16.0中的新特性——Error Boundaries及其注意点](https://blog.csdn.net/liwusen/article/details/78521006)


