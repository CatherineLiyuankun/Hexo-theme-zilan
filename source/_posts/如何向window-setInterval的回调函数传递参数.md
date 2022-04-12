---
title: 如何向window.setInterval的回调函数传递参数
catalog: true
date: 2022-04-12 15:24:47
subtitle: Pass parameters in setInterval function
header-img:
tags:
categories:
- TECH
- FrontEnd
- JavaScript
---

## Example

```javascript
function myCallback(a, b)
{
 // Your code here
 // Two Parameters of the myCallback function.
 console.log(a);
 console.log(b);
}

// 错误传参方法
var intervalIDWrong = window.setInterval(myCallback('parameterWrong1', 'parameterWrong2'), 5000, );  
//Wrong way, it will eval and excute myCallback('parameter2') immediately, and return undefined to  window.setInterval as first parameter actually
//运行后发现，参数会被立即打印出来，这是因为func并不是setInterval的回调函数，因为func会立即执行（也就是网址会被立即打印的原因），实际传递给setInterval的是func的返回值（当然它的返回值为undefined）。

// Solution 1
var intervalID1 = window.setInterval(myCallback, 5000, 'parameter1-1',  'parameter1-2');

// Solution 2
var intervalID2 = window.setInterval(function() {myCallback('parameter2-1' , 'parameter2-2');}, 5000);

// Solution 3
var intervalID3 =setInterval(myCallback.bind(null, 'parameter3-1' , 'parameter3-2'), 5000);

```

## 错误传参方法

```javascript
var intervalIDWrong = window.setInterval(myCallback('parameterWrong1', 'parameterWrong2'), 5000, );  

// VM1417:1 Refused to evaluate a string as JavaScript because 'unsafe-eval' is not an allowed source of script in the following Content Security Policy directive: "script-src 'self'".
```

Wrong way, it will eval and excute myCallback('parameter2') immediately, and return undefined to  window.setInterval as first parameter actually
运行后发现，参数会被立即打印出来，这是因为func并不是setInterval的回调函数，因为func会立即执行（也就是网址会被立即打印的原因），实际传递给setInterval的是func的返回值（当然它的返回值为undefined）。

因为是通过`eval`立即执行myCallback，所以有些设置有较高安全Content Security Policy的网页上会报错：

```console
VM1417:1 Refused to evaluate a string as JavaScript because 'unsafe-eval' is not an allowed source of script in the following Content Security Policy directive: "script-src 'self'".
```

## Solution 1 third parameter of window.setInterval

If you don't need to support IE

`var intervalID = window.setInterval(myCallback, 5000, 'parameter1-1',  'parameter1-2');`

由于IE9和IE9以下浏览器不支持第三个参数，所以较早的教程很少教程。

## Solution 2  a wrapper function

If you want to support IE <=9

`var intervalID2 = window.setInterval(function() {myCallback('parameter2-1' , 'parameter2-2');}, 5000);`

1. setInterval第一个参数是一个匿名函数。
2. 此匿名函数执行后返回一个函数，返回的函数才是真正传递给setInterval的回调函数。
3. 根据作用域与作用域链的原理，返回的函数可以使用通过外层函数传递进来的参数。
4. 于是可以正常打印出传递的参数。

## Solution 3 Function.prototype.bind() method

If you want to support IE <=9

now with ES5, bind method Function prototype: [Function.prototype.bind()](https://javascript.info/bind)

`var intervalID3 =setInterval(myCallback.bind(null, 'parameter2-1' , 'parameter2-2'), 5000);`

## Solution 4 替换掉IE内置的setTimeout/setInterval

时至此刻，要想在IE下也能使用，就只有替换掉IE内置的setTimeout/setInterval方法了。如下：

```javascript
(function(){ // reset timer for IE
    if (navigator.appName == 'Microsoft Internet Explorer') {
        var _preTimeout = window.setTimeout,_preInterval = window.setInterval;

        window.setTimeout = function(callback, after){
            var l = arguments.length;
            if (l > 2) {
                var args = [];
                for (var i = 2; i < l; i++) {
                    args.push(arguments[i]);
                }
                 
                return _preTimeout(function(){
                    callback.apply(this, args);
                }, after); //记得返回timer id
            }
            else {
                return _preTimeout.apply(this, arguments);
            }
        }
         
        window.setInterval = function(callback, cycle){
            var l = arguments.length;
            if (l > 2) {
                var args = [];
                for (var i = 2; i < l; i++) {
                    args.push(arguments[i]);
                }
                 
                return _preInterval(function(){
                    callback.apply(this, args);
                }, cycle);
            }
            else {
                return _preInterval.apply(this, arguments);
            }
        }
    }
})();

```
## 参考文章

- [Mdn web docs window.setInterval 英文版](https://developer.mozilla.org/en-US/docs/Web/API/setInterval)
- [Mdn web docs window.setInterval 中文版](https://developer.mozilla.org/zh-CN/docs/Web/API/setInterval#%E5%9B%9E%E8%B0%83%E5%8F%82%E6%95%B0)
- [stackoverflow](https://stackoverflow.com/questions/457826/pass-parameters-in-setinterval-function)
