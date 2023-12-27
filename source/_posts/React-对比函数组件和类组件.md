---
title: React 对比函数组件和类组件
catalog: true
date: 2023-12-27 18:54:37
subtitle: React Differences between Functional Components and Class Components
header-img:
tags:
- React 16
categories:
- TECH
- FrontEnd
- React
---

## Rendering JSX

首先，它们的明显区别在于语法。正如它们的名字一样，功能组件只是一个返回 JSX 的普通 JavaScript 函数。类组件是一个扩展了 React.Component 的 JavaScript 类，它有一个 render 方法。有点困惑？让我们来看一个简单的例子。
功能组件是一个返回 JSX 的函数。

```JavaScript
import React from "react";
 
const FunctionalComponent = () => { // arrow functions
 return <h1>Hello, world</h1>;
};
```

或者

```JavaScript
import React from "react";

function FunctionalComponent() {
 return <h1>Hello, world</h1>;
}
```

在定义类组件时，必须创建一个扩展了 `React.Component` 的类。要渲染的 JSX 将在 render 方法中返回。

```JavaScript
import React, { Component } from "react";

class ClassComponent extends Component {
 render() {
   return <h1>Hello, world</h1>;
 }
}

```

## Passing props

传递props可能会让人感到困惑，让我们来看看类和功能组件中是如何编写props的。假设我们像下面这样传递名称为 "propsA "的props。

```JavaScript
<Component name="propsA" />
```

```JavaScript
const FunctionalComponent = ({ name }) => {
 return <h1>Hello, {name}</h1>;
};
```

在功能组件中，我们将props作为函数的参数传递。请注意，我们在这里使用了destructuring。或者，我们也可以不使用destructuring。

```JavaScript
const FunctionalComponent = (props) => {
 return <h1>Hello, {props.name}</h1>;
};
```

既然它是一个类，就需要用它来引用props。当然，在使用基于类的组件时，我们可以使用destructuring来获取props内部的名称。

```JavaScript
class ClassComponent extends React.Component {
  render() {
    const { name } = this.props;
    return <h1>Hello, { name }</h1>;
 }
}
```

## Handling state

### Counter using Class Components

这是用 ReactJS 构建的大多数现代网络应用的基础。这些组件是简单的类（由为应用程序添加功能的多个函数组成）。

```javascript
import React, { Component } from "react"; 

class ClassComponent extends React.Component { 
    constructor() { 
        super(); 
        this.state = { 
            count: 0 
        }; 
        this.increase = this.increase.bind(this); 
    } 

    increase() { 
        this.setState({ count: this.state.count + 1 }); 
    } 

    render() { 
        return ( 
            <div style={{ margin: '50px' }}> 
                <h1>Welcome to Geeks for Geeks </h1> 
                <h3>Counter App using Class Component : </h3> 
                <h2> {this.state.count}</h2> 
                <button onClick={this.increase}> Add</button> 
            </div> 
        ) 
    } 
} 

export default ClassComponent; 

```

### Counter using Functional Components

功能组件是在 React 中工作时会遇到的一些更常见的组件。它们只是 JavaScript 函数。我们可以通过编写 JavaScript 函数为 React 创建一个功能组件。

```javascript
import React, { useState } from "react"; 

const FunctionalComponent = () => { 
    const [count, setCount] = useState(0); 

    const increase = () => { 
        setCount(count + 1); 
    } 

    return ( 
        <div style={{ margin: '50px' }}> 
            <h1>Welcome to Geeks for Geeks </h1> 
            <h3>Counter App using Functional Component : </h3> 
            <h2>{count}</h2> 
            <button onClick={increase}>Add</button> 
        </div> 
    ) 
} 

export default FunctionalComponent; 
```

对于功能组件，我们使用hooks（useState）来管理状态。如果编写了一个功能组件，并意识到需要为其添加一些状态，以前必须将其转换为类组件。现在，可以在现有的函数组件中使用hooks来管理状态，而无需将其转换为类组件。hooks是 React 16.8 新增的功能。它们让无需编写类即可使用状态和其他 React 功能。我们可以在功能组件中使用hooks来代替类，因为这是一种更简单的状态管理方式。

- hooks只能用于功能组件，不能用于类内组件!
- hooks 详细介绍可以看之前的文章： [hooks](./React-16-Hooks.html)

## Lifecycle Methods

最后，让我们来谈谈生命周期。生命周期在渲染的时间安排上起着重要作用。对于那些从类组件迁移到功能组件的人来说，一定很想知道有什么可以替代类组件中的 `componentDidMount()` 等生命周期方法。没错，有一个hook可以完美地实现这一目的，让我们一起来看看吧！

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

```JavaScript

```

```JavaScript

```

## 对比函数组件和类组件总结

| [**Functional Components**](https://www.geeksforgeeks.org/reactjs-functional-components/)                                                                                                                                      | [**Class Components**](https://www.geeksforgeeks.org/reactjs-class-based-components/)                                                                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 功能组件只是一个纯 JavaScript pure函数，它接受props作为参数，并返回一个 React 元素（JSX）。                                                                                                                                    | 类组件要求您从 React.Component 扩展（extend），并创建返回 React 元素的render函数。并创建一个返回 React 元素的render函数。                                                                                                                  |
| no `render` method                                                                                                                                                                                                             | 必须有`render()` method 返回 JSX (语法上类似于HTML)                                                                                                                                                                                        |
| 功能组件从上到下依次运行，一旦功能返回，它就无法继续存活。Functional components run from top to bottom and once the function is returned it can’t be kept alive.                                                               | 类组件被实例化后，不同的生命周期方法会保持活力，并根据类组件所处的阶段运行和调用。 The class component is instantiated and different life cycle method is kept alive and is run and invoked depending on the phase of the class component. |
| 也被称为无状态组件，因为它们只是接受数据并以某种形式显示出来，主要负责渲染用户界面。Also known as Stateless components as they simply accept data and display them in some form, they are mainly responsible for rendering UI. | 也被称为有状态组件，因为它们实现了逻辑和状态。Also known as Stateful components because they implement logic and state.                                                                                                                    |
| 功能组件中不能使用 React 生命周期方法（例如 componentDidMount）。React lifecycle methods (for example, componentDidMount) cannot be used in functional components.                                                             | React 生命周期方法可用于类组件内部（例如 componentDidMount）。React lifecycle methods can be used inside class components (for example, componentDidMount).                                                                                |
| Hooks可以很容易地用于功能组件，使其成为有状态的组件。Hooks can be easily used in functional components to make them Stateful. <br>Example:<br>`const [name,SetName]= React.useState(' ')`                                      | 在类组件中实现hook需要不同的语法。It requires different syntax inside a class component to implement hooks.<br>Example:<br>`constructor(props) {  super(props);  this.state = {name: ' '}`                                                 |
| 不使用构造函数。Constructors are not used.                                                                                                                                                                                     | 使用构造函数，因为它需要存储状态。Constructor is used as it needs to store state.                                                                                                                                                          |

## Reference Links

- [Differences between Functional Components and Class Components](https://www.geeksforgeeks.org/differences-between-functional-components-and-class-components/)
- [Understanding Functional Components vs. Class Components in React](https://www.twilio.com/blog/react-choose-functional-components)
