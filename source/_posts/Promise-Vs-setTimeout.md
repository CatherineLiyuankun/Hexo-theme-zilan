---
title: Promise Vs setTimeout
catalog: true
date: 2019-10-29 14:17:43
subtitle:
header-img:
tags:
- Promise
categories:
- TECH
- FrontEnd
- JS
---

了解这个，就得了解JavaScript异步编程，了解任务队列才能知其根本。

一个事件循环（event loop）+多个任务队列（task queue）

## 事件循环（event loop）

## Task Queue
### Macrotask Queue 宏任务队列:
* setTimeout
* setInterval
* setImmediate
* requestAnimationFrame
* UI rendeing
* NodeJS中的`I/O （fs.readFile）等

### Microtask Queue 微任务队列:
主要包括两类：

- 独立回调microTask：如Promise，其成功／失败回调函数相互独立；
- 复合回调microTask：如 Object.observe, MutationObserver 和NodeJs中的 process.nextTick ，不同状态回调在同一函数体；

### MacroTask MicroTask 两者关系
入栈过程：
> 1. 开始执行JavaScript脚本，将任务JavaScript Run入栈macroTask队列；
> 2. 同步resolvePromise后；
> 3. 入栈`第一个`setTimeout任务进入macroTask队列
> 4. 入栈Proimse.then任务进入microTask队列；
> 5. 入栈第二个setTimeout任务进入macroTask队列；
出栈执行过程：
> 6. 同步执行代码，退出第一个macroTask，即JavaScript Run;
> 7. 按顺序执行microTask queue 所有microTask；
> 8. 执行下一个macroTask；

可以参考这个流程图：
![流程图](http://www.programmersought.com/images/250/ae6f91d1cb68f1e5d05b95a66a2cba72.png)


## Show me the code
例题1-5 来自[ES6 Book ](http://es6.ruanyifeng.com/#docs/promise)：

### 例题1

Promise 新建后就会立即执行。

```javascript
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('resolved.');
});

console.log('Hi!');

// Promise
// Hi!
// resolved
```
上面代码中，Promise 新建后立即执行，所以首先输出的是Promise。然后，then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以resolved最后输出。

### 例题2

```javascript
new Promise((resolve, reject) => {
  resolve(1);
  console.log(2);
}).then(r => {
  console.log(r);
});
// 2
// 1
```
上面代码中，调用resolve(1)以后，后面的console.log(2)还是会执行，并且会首先打印出来。这是因为立即 resolved 的 Promise 是在本轮事件循环的末尾执行，总是晚于本轮循环的同步任务。

一般来说，调用resolve或reject以后，Promise 的使命就完成了，后继操作应该放到then方法里面，而不应该直接写在resolve或reject的后面。所以，最好在它们前面加上return语句，这样就不会有意外。

```javascript
new Promise((resolve, reject) => {
  return resolve(1);
  // 后面的语句不会执行
  console.log(2);
})
```
### 例题3
需要注意的是，立即resolve()的 Promise 对象，是在本轮“事件循环”（event loop）的结束时执行，而不是在下一轮“事件循环”的开始时。
```javascript
setTimeout(function () {
  console.log('three');
}, 0);

Promise.resolve().then(function () {
  console.log('two');
});

console.log('one');

// one
// two
// three
```
上面代码中，setTimeout(fn, 0)在下一轮“事件循环”开始时执行，Promise.resolve()在本轮“事件循环”结束时执行，console.log('one')则是立即执行，因此最先输出。

### 例题4 Promise.try
```javascript
const f = () => console.log('now');
Promise.resolve().then(f);
console.log('next');
// next
// now
```
上面代码中，函数f是同步的，但是用 Promise 包装了以后，就变成异步执行了。

那么有没有一种方法，让同步函数同步执行，异步函数异步执行，并且让它们具有统一的 API 呢？回答是可以的，并且还有两种写法。第一种写法是用async函数来写。

```javascript
const f = () => console.log('now');
(async () => f())();
console.log('next');
// now
// next
```
上面代码中，第二行是一个立即执行的匿名函数，会立即执行里面的async函数，因此如果f是同步的，就会得到同步的结果；如果f是异步的，就可以用then指定下一步，就像下面的写法。

```javascript
(async () => f())()
.then(...)

```
需要注意的是，async () => f()会吃掉f()抛出的错误。所以，如果想捕获错误，要使用promise.catch方法。

```javascript
(async () => f())()
.then(...)
.catch(...)

```
第二种写法是使用new Promise()。

```javascript
const f = () => console.log('now');
(
  () => new Promise(
    resolve => resolve(f())
  )
)();
console.log('next');
// now
// next

```
上面代码也是使用立即执行的匿名函数，执行new Promise()。这种情况下，同步函数也是同步执行的。

鉴于这是一个很常见的需求，所以现在有一个提案，提供Promise.try方法替代上面的写法。

```javascript
const f = () => console.log('now');
Promise.try(f);
console.log('next');
// now
// next
```

例题5, 6 来自[浅析setTimeout与Promise](https://juejin.im/post/5b7057b251882561381e69bf)：
### 例题5
```javascript
var p1 = new Promise(function(resolve, reject){
    console.log("Before resolve");
    resolve(1);
})
setTimeout(function(){
  console.log("will be executed at the top of the next Event Loop");
},0)
p1.then(function(value){
  console.log("p1 fulfilled");
})
setTimeout(function(){
  console.log("will be executed at the bottom of the next Event Loop");
},0)
```

```json
Before resolve
p1 fulfilled
will be executed at the top of the next Event Loop
will be executed at the bottom of the next Event Loop
```
> 1. 开始执行JavaScript脚本，将任务JavaScript Run入栈macroTask队列；
> 2. 同步resolvePromise后；
> 3. 入栈第一个setTimeout任务进入macroTask队列
> 4. 入栈Proimse.then任务进入microTask队列；
> 5. 入栈第二个setTimeout任务进入macroTask队列；
> 6. 同步执行代码完毕，退出第一个macroTask，即JavaScript Run;  输出 Before resolve
> 7. 执行清空microTask；输出 p1 fulfilled
> 8. 执行下一个macroTask；输出 will be executed at the top of the next Event Loop
will be executed at the bottom of the next Event Loop

### 例题6

```javascript
setTimeout(function(){
  console.log("will be executed at the top of the next Event Loop")
},0)
var p1 = new Promise(function(resolve, reject){
    setTimeout(() => { resolve(1); }, 0);
});
setTimeout(function(){
    console.log("will be executed at the bottom of the next Event Loop")
},0)
for (var i = 0; i < 100; i++) {
    (function(j){
        p1.then(function(value){
           console.log("promise then - " + j)
        });
    })(i)
}
// will be executed at the top of the next Event Loop
// promise then - 0
// promise then - 1
// promise then - 2
// ...
// promise then - 99
// will be executed at the bottom of the next Event Loop
```

### 例题7
来源： [Promise的队列与setTimeout的队列有何关联？](https://www.zhihu.com/question/36972010)
```javascript
setTimeout(function(){console.log(4)},0);
new Promise(function(resolve){
    console.log(1)
    for( var i=0 ; i<10000 ; i++ ){
        i==9999 && resolve()
    }
    console.log(2)
}).then(function(){
    console.log(5)
});
console.log(3);

//1,2,3,5,4
```
```javascript

```
```javascript

```


1. 首先同步执行完所有代码，其间注册了三个setTimeout异步任务，100个Promise异步任务；
2. 然后检查MacroTask队列，取第一个到期的MacroTask，执行输出will be executed at the top of the next Event Loop;
3. 然后检查MicroTask队列，发现没有到期的MicroTask，进入第4步；
4. 再次检查MacroTask，执行第二个setTimeout处理函数，resolve Promise；
5. 然后检查MicroTask队列，发现Promise已解决，其异步处理函数均可执行，依次执行，输出promise then - 0 至promise then - 99；
6. 最后再次检查MacroTask队列，执行输出will be executed at the bottom of the next Event Loop
7. 交替往复检查两个异步任务队列，直至执行完毕；

## Reference Links
- [浅析setTimeout与Promise](https://juejin.im/post/5b7057b251882561381e69bf)
- [What is the relationship between event loop and Promise [stackoverflow]](https://juejin.im/post/5b7057b251882561381e69bf)
- [ES6 Book ](http://es6.ruanyifeng.com/#docs/promise)
- [Promise的队列与setTimeout的队列有何关联？](https://www.zhihu.com/question/36972010)
- [Writing a JavaScript framework - Execution timing, beyond setTimeout](https://blog.risingstack.com/writing-a-javascript-framework-execution-timing-beyond-settimeout)
- [6-Concurrency model and event loop -part B](https://github.com/deenjohn/NodeRevision/blob/master/6-Concurrency%20model%20and%20event%20loop%20-part%20B.md)
- [Microtasks vs Events and how to define what as which?](https://stackoverflow.com/questions/34753342/microtasks-vs-events-and-how-to-define-what-as-which)
- [JavaScript: How is callback execution strategy for promises different than DOM events callback?](https://medium.com/@jitubutwal144/javascript-how-is-callback-execution-strategy-for-promises-different-than-dom-events-callback-73c0e9e203b1)