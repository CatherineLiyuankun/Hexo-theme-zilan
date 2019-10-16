---
title: ES6-Promise
catalog: true
date: 2019-10-13 14:05:41
subtitle:
header-img:
tags:
- ES6
categories:
- TECH
- FrontEnd
- ES6
---

# Promise
```javascript
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```
Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。

resolve函数的作用是，将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；reject函数的作用是，将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

Promise实例生成以后，可以用then方法分别指定resolved状态和rejected状态的回调函数。

```javascript
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```
then方法可以接受两个回调函数作为参数。第一个回调函数是Promise对象的状态变为resolved时调用，第二个回调函数是Promise对象的状态变为rejected时调用。其中，第二个函数是可选的，不一定要提供。这两个函数都接受Promise对象传出的值作为参数。

## Promise.prototype.then()
then方法的第一个参数是resolved状态的回调函数，第二个参数（可选）是rejected状态的回调函数
## Promise.prototype.catch()
.then(null, rejection)或.then(undefined, rejection)的别名，用于指定发生错误时的回调函数。
## Promise.prototype.finally()
finally方法用于指定不管 Promise 对象最后状态如何，都会执行的操作。该方法是 ES2018 引入标准的。


```javascript
// bad
promise
  .then(function(data) {
    // success
  }, function(err) {
    // error
  });

// good
promise
  .then(function(data) { //cb
    // success
  })
  .catch(function(err) {
    // error
    //.then(null, rejection)或.then(undefined, rejection)的别名，用于指定发生错误时的回调函数。
  })
  .finally(
      //不管 Promise 对象最后状态如何，都会执行的操作
      //与状态无关的，不依赖于 Promise 的执行结果
  );
```

```javascript
function timeout(ms) {
return new Promise((resolve, reject) => {
    console.log('setTimeout start');
    setTimeout(resolve, ms, 'done');
    console.log('setTimeout end');
});
}

timeout(100).then((value) => {
console.log(value);
});

// setTimeout start
// setTimeout end
// done
```
# 处理多个promise
## Promise.all() 
```javascript
const p = Promise.all([p1, p2, p3]);
```
return all resolved

p的状态由p1、p2、p3决定，分成两种情况。
（1）只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。

（2）只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。

## Promise.race()
```javascript
const p = Promise.race([p1, p2, p3]);
```
return first result

只要p1、p2、p3之中有一个实例率先改变状态，p的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给p的回调函数。

## Promise.allSettled()

return all end

只有等到所有这些参数实例都返回结果，不管是fulfilled还是rejected，包装实例才会结束。该方法由 ES2020 引入。
我们不关心异步操作的结果，只关心这些操作有没有结束。这时，Promise.allSettled()方法就很有用。如果没有这个方法，想要确保所有操作都结束，就很麻烦。Promise.all()方法无法做到这一点。

## Promise.any()

return any resolved

只要参数实例有一个变成fulfilled状态，包装实例就会变成fulfilled状态；如果所有参数实例都变成rejected状态，包装实例就会变成rejected状态。该方法目前是一个第三阶段的提案 。

# 返回一个新的 Promise 实例
## Promise.resolve()
需要将现有对象转为 Promise 对象。Promise.resolve()在本轮“事件循环”结束时执行
```javascript
Promise.resolve('foo')
// 等价于
new Promise(resolve => resolve('foo'))
```
## Promise.reject()
Promise.reject(reason)方法也会返回一个新的 Promise 实例，该实例的状态为rejected。
注意，Promise.reject()方法的参数，会原封不动地作为reject的理由，变成后续方法的参数。这一点与Promise.resolve方法不一致。

## Promise.try()

实际开发中，经常遇到一种情况：不知道或者不想区分，函数f是同步函数还是异步操作，但是想用 Promise 来处理它。因为这样就可以不管f是否包含异步操作，都用then方法指定下一步流程，用catch方法处理f抛出的错误。一般就会采用下面的写法。
```javascript
Promise.resolve().then(f)
```
上面的写法有一个缺点，就是如果f是同步函数，那么它会在本轮事件循环的末尾执行。
```javascript
const f = () => console.log('now');
Promise.resolve().then(f);
console.log('next');
// next
// now
```
上面代码中，函数f是同步的，但是用 Promise 包装了以后，就变成异步执行了。

那么有没有一种方法，让同步函数同步执行，异步函数异步执行，并且让它们具有统一的 API 呢？回答是可以的，并且还有两种写法。
### 第一种写法是用async函数来写。
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

### 第二种写法是使用new Promise()。
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
事实上，Promise.try存在已久，Promise 库Bluebird、Q和when，早就提供了这个方法。

由于Promise.try为所有操作提供了统一的处理机制，所以如果想用then方法管理流程，最好都用Promise.try包装一下。这样有许多好处，其中一点就是可以更好地管理异常。

function getUsername(userId) {
  return database.users.get({id: userId})
  .then(function(user) {
    return user.name;
  });
}
上面代码中，database.users.get()返回一个 Promise 对象，如果抛出异步错误，可以用catch方法捕获，就像下面这样写。

database.users.get({id: userId})
.then(...)
.catch(...)
但是database.users.get()可能还会抛出同步错误（比如数据库连接错误，具体要看实现方法），这时你就不得不用try...catch去捕获。

try {
  database.users.get({id: userId})
  .then(...)
  .catch(...)
} catch (e) {
  // ...
}
上面这样的写法就很笨拙了，这时就可以统一用promise.catch()捕获所有同步和异步的错误。

Promise.try(() => database.users.get({id: userId}))
  .then(...)
  .catch(...)
事实上，Promise.try就是模拟try代码块，就像promise.catch模拟的是catch代码块。


# Reference Links:
- http://es6.ruanyifeng.com/#docs/promise