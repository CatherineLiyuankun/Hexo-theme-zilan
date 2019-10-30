---
title: Javascript aync异步编程
catalog: true
subtitle:
header-img:
tags:
---



JavaScript之异步编程
JavaScript语言执行环境是单线程的，单线程在程序执行时，所走的程序路径按照连续顺序排下来，前面的必须处理好，后面的才会执行。在某个特定的时刻只有特定的代码能够被执行，且会阻塞其它的代码，而异步编程能弥补其不足，本篇我们阐述JavaScript异步编程。

JavaScript之单线程
单线程在程序执行时，所走的程序路径按照连续顺序排下来，前面的必须处理好，后面的才会执行。在某个特定的时刻只有特定的代码能够被执行，且会阻塞其它的代码。

单线程就是一心一意，用情专一的痴情少年。单线程就是进程只有一个线程；多线程就是进程有多个线程。

基于JavaScript的单线程语言执行环境及其不足，提出了JavaScript的同步与异步编程方式。

同步，即任务一步一步执行，当前代码执行完毕后才能继续执行后续代码；异步则是开始执行当前代码后不需要等待，即可继续执行后续任务，当前任务执行结束后可以通过状态、通知和回调来通知调用者。

JavaScript之异步编程实现
JavaScript异步编程实现主要归为三类：回调函数、发布订阅、Promise对象。

回调函数

    function a(fn) {
        //a函数任务...
        setTimeout(function() {
            fn();
        }, 0);
        console.log('a');
    }
    function b(fn) {
        //b函数任务
        console.log('b');
    }
    a(b);
以上代码打印值顺序如何呢？结果是先a后b。至于为什么，不得不说说setTimeout。再细微的东西，只要存在，我们都能从中弄出些精华，就比如setTimeout。
请看代码：
···

for (var i = 0; i < 5; i ++) {
    setTimeout(function(){
        console.log(i);
    }, 0);
}
console.log(i);
//5 ; 5 ; 5 ; 5; 5
···
全部打印出5，要明白为什么，需理解三点：

i在此处是for循环所在上下文环境的变量，有且只有一个i;
循环结束时i==5;
JavaScript单线程事件处理器在线程空闲前不会执行下一事件。
你可能看过类似这样的代码：

···

function f1(callback) {
    setTimeout(function() {
        f2(functions() {
            setTimeout({    
               callback(...) ;
            }, 0); 
        });
    }, 0);
}
function(callback) {//...}
···
请避免这样的多层嵌套回调。

发布订阅
PubSub,即Publish/Subscribe,发布、订阅模式， 用以分发事件。常见的有jQuery的自定义事件监听、Node的EventEmitter对象等。

jQuery事件监听

    $('#btn').on('myEvent', function(e) {
        console.log('There is my Event');
    });
    $('#btn').trigger('myEvent');
PubSub

    var PubSub = function(){
        this.handlers = {}; 
    };
    PubSub.prototype.subscribe = function(eventType, handler) {
        if (!(eventType in this.handlers)) {
            this.handlers[eventType] = [];
        }
        this.handlers[eventType].push(handler); //添加事件监听器
        return this;//返回上下文环境以实现链式调用
    };
    PubSub.prototype.publish = function(eventType) {
        var _args = Array.prototype.slice.call(arguments, 1);
        for (var i = 0, _handlers = this.handlers[eventType]; i < _handlers.length; i++) {
            _handlers[i].apply(this, _args);//遍历事件监听器
        }
        return this;
    };
    var event = new PubSub;//构造PubSub实例
    event.subscribe('list', function(msg) {
        console.log(msg);
    });
    event.publish('list', {data: ['one,', 'two']});
    //Object {data: Array[2]}
以上代码就是一个简易的订阅发布模式基本实现，还可以对其进行完善，如添加只执行一次事件监听器等。

Promise对象
Promise是CommonJS的规范之一，拥有resolve、reject、done、fail、then等方法，能够帮助我们控制代码的流程。

一个promise可能有三种状态：等待（pending）、已完成（fulfilled）、已拒绝（rejected）;
一个promise的状态只可能从“等待”转到“完成”态或者“拒绝”态，不能逆向转换，同时“完成”态和“拒绝”态不能相互转换;
promise必须实现then方法（可以说，then就是promise的核心），而且then必须返回一个promise，同一个promise的then可以调用多次，并且回调的执行顺序跟它们被定义时的顺序一致;
then方法接受两个参数，第一个参数是成功时的回调，在promise由“等待”态转换到“完成”态时调用，另一个是失败时的回调，在promise由“等待”态转换到“拒绝”态时调用。
同时，then可以接受另一个promise传入，也接受一个“类then”的对象或方法，即thenable对象。
* jQuery之Promise


    var prom = new $.Deferred();
    prom.done(function(value) {
        console.log(value + ' Done');
    });
    prom.fail(function(value) {
        console.log(value + ' Fail');
    });
    prom.always(function(v) {
        console.log(' always here');
    });

    prom.resolve('OK');
Deferred是Promise的超集，相对于Promise只提供then方法添加调用，触发这些调用需要其他支持，使用Deferred实例可直接触发调用。

Promise简单实现

    function defer() {
            var tasks = [],
        progresses = [],
        state = 'pending',
        value,
        reason;
            return {
                resolve: function(_value) {
                    if (tasks) {
                        value = ref(_value);
                        tasks.forEach(function(task) {                      
                            nextTick(function() {
                                value.then.apply(value, task);
                            });
                        });
                        tasks = null;
                        state = 'resolved';
                    }else {
                        if (state === 'resolved') {
                            throw new Error('A promise should been resolved once.');
                        }
                    }
                },
                reject: function(reason) {
                    if (tasks) {
                        value = ref(reason);
                        tasks.forEach(function(task) {
                            nextTick(function() {
                                value.then.apply(value, [task[1], task[0]]);
                            });
                        });
                        tasks = undefined;
                        state = 'rejected';
                    }else {
                        if (state === 'rejected') {
                            throw new Error('A promise should been rejected once.');
                        }
                    }
                },
                notify: function(progress) {
                    if (state === 'resolved' || state === 'rejected') {
                        return;
                    }
                    progresses.push(progress);
                },
                promise: {
                    then: function(_callback, _errback, _notifyback) {
                        var deferred = defer();
                        _callback = _callback || function(value) {
                            return value;
                        };
                        _errback = _errback || function(reason) {
                            return reject(reason);
                        };
                        _notifyback = _notifyback || function(progress) {
                            return progress;
                        };
                        var callback = function(value) {
                            var result;
                            try {
                                result = _callback(value);
                            }catch(e) {
                                deferred.reject(e);
                            }finally {
                                deferred.resolve(result);
                            }
                        };      
                        var errback = function(reason) {
                            var result;
                            try {
                                result = _errback(reason);
                            }catch(e) {
                                deferred.reject(e);
                            }finally {
                                deferred.resolve(result);
                            }
                        }
                        nextTick(function() {
                            while (progresses.length) {
                                try {
                                    _notifyback(progresses.shift());
                                }catch(e) {
                                    deferred.reject(e);
                                    break;
                                }
                            }
                        });             
                        if (tasks) {
                            tasks.push([callback, errback]);
                        }else {
                            nextTick(function() {
                                if (state === 'rejected') {
                                    value.then(errback);
                                }else if (state === 'resolved') {   
                                    value.then(callback);
                                }
                            });
                        }
                        return deferred.promise;
                    }
                }
            };
        }
        var ref = function(value) {
            if (value && typeof value.then === 'function') {
                return value;
            }
            return {
                then: function(callback) {
                    return ref(callback(value));
                }
            }
        };
        var reject = function(reason) {
            return {
                then: function(callback, errback) {
                    return ref(errback(reason));
                }
            };
        };
        var nextTick = function(callback) {
            setTimeout(callback, 0);
        };
        //Promise实例
        var deferred = defer(),
            promise = deferred.promise;
        promise.then(function(value) {
            console.log(value);
            throw 'zhangsan';
        }).then(function (v) {
            console.log(v);
        }, function (err) {
            console.error(err);
            done();
        });
        setTimeout(function () {
            deferred.resolve('zhangsan1');
        }, 1000);
以上为一个简单的Promise基本功能实现，比较基础，更多有关知识有待日后继续研究总结。


------

2017-04-252017-04-25 by 熊 建刚 / 13/ 16893
还记得一年前写过一篇关于JavaScript异步编程简述的文章，主要介绍了JavaScript的单线程特性与异步编程实现方式：
回调函数，发布订阅模式，Promise对象三种，关于Promise介绍的比较简略，决定再详细总结一下，既是对上一篇文章的补充，也能以更深刻的方式分享自己关于异步编程的理解。

索引

1 前言
2 同步与异步
2.0.1 多线程
2.0.2 JavaScript单线程
2.0.3 并行与并发
3 JavaScript异步机制
4 并发模型（Concurrency model）
4.0.1 堆栈与队列
4.1 事件循环（Event Loop）
4.1.1 任务
4.1.2 事件循环流程
4.1.2.1 并发模型与事件循环
4.1.3 再谈setTimeout(…0)
4.1.4 Web Workers
5 JavaScript异步实现
5.0.1 参考：
前言
如果你有志于成为一个优秀的前端工程师，或是想要深入学习JavaScript，异步编程是必不可少的一个知识点，这也是区分初级，中级或高级前端的依据之一。如果你对异步编程没有太清晰的概念，那么我建议你花点时间学习JavaScript异步编程，如果你对异步编程有自己的独特理解，也欢迎阅读本文，一起交流。

同步与异步
介绍异步之前，回顾一下，所谓同步编程，就是计算机一行一行按顺序依次执行代码，当前代码任务耗时执行会阻塞后续代码的执行。

同步编程，即是一种典型的请求-响应模型，当请求调用一个函数或方法后，需等待其响应返回，然后执行后续代码。

一般情况下，同步编程，代码按序依次执行，能很好的保证程序的执行，但是在某些场景下，比如读取文件内容，或请求服务器接口数据，需要根据返回的数据内容执行后续操作，读取文件和请求接口直到数据返回这一过程是需要时间的，网络越差，耗费时间越长，如果按照同步编程方式实现，在等待数据返回这段时间，JavaScript是不能处理其他任务的，此时页面的交互，滚动等任何操作也都会被阻塞，这显然是及其不友好，不可接受的，而这正是需要异步编程大显身手的场景，如下图，耗时任务A会阻塞任务B的执行，等到任务A执行完才能继续执行B：

同步编程任务阻塞流程

当使用异步编程时，在等待当前任务的响应返回之前，可以继续执行后续代码，即当前执行任务不会阻塞后续执行。

异步编程，不同于同步编程的请求-响应模式，其是一种事件驱动编程，请求调用函数或方法后，无需立即等待响应，可以继续执行其他任务，而之前任务响应返回后可以通过状态、通知和回调来通知调用者。

多线程
前面说明了异步编程能很好的解决同步编程阻塞的问题，那么实现异步的方式有哪些呢？通常实现异步方式是多线程，如C#, 即同时开启多个线程，不同操作能并行执行，如下图，耗时任务A执行的同时，在线程二中任务B也可以执行：

多线程异步编程无阻塞流程

JavaScript单线程
JavaScript语言执行环境是单线程的，单线程在程序执行时，所走的程序路径按照连续顺序排下来，前面的必须处理好，后面的才会执行，而使用异步实现时，多个任务可以并发执行。那么JavaScript的异步编程如何实现呢，下一节将详细阐述其异步机制。

并行与并发
前文提到多线程的任务可以并行执行，而JavaScript单线程异步编程可以实现多任务并发执行，这里有必要说明一下并行与并发的区别。

并行，指同一时刻内多任务同时进行；
并发，指在同一时间段内，多任务同时进行着，但是某一时刻，只有某一任务执行；
通常所说的并发连接数，是指浏览器向服务器发起请求，建立TCP连接，每秒钟服务器建立的总连接数，而假如，服务器处10ms能处理一个连接，那么其并发连接数就是100。

JavaScript异步机制
本节介绍JavaScript异步机制，首先来看一个例子：


    for (var i = 0; i < 5; i ++) {
        setTimeout(function(){
            console.log(i);
        }, 0);
    }
    console.log(i);
    //5 ; 5 ; 5 ; 5; 5
应该明白最后输出的全是5：

i在此处是for循环所在上下文环境的变量，有且只有一个i;
循环结束时i==5;
JavaScript单线程事件处理器在线程空闲前不会执行下一事件。
如上面第三点所述，如果要真正理解以上例子中的setTimeout()，及JavaScript异步机制，需要理解JavaScript的事件循环和并发模型。

并发模型（Concurrency model）
目前，我们已经知道，JavaScript执行异步任务时，不需要等待响应返回，可以继续执行其他任务，而在响应返回时，会得到通知，执行回调或事件处理程序。那么这一切具体是如何完成的，又以什么规则或顺序运作呢？接下来我们需要解答这个问题。

注：回调和事件处理程序本质上并无区别，只是在不同情况下，不同的叫法。

前文已经提到，JavaScript异步编程使得多个任务可以并发执行，而实现这一功能的基础是JavScript拥有一个基于事件循环的并发模型。

堆栈与队列
介绍JavaScript并发模型之前，先简单介绍堆栈和队列的区别：

堆（heap）：内存中某一未被阻止的区域，通常存储对象（引用类型）；
栈（stack）：后进先出的顺序存储数据结构，通常存储函数参数和基本类型值变量（按值访问）；
队列（queue）：先进先出顺序存储数据结构。
事件循环（Event Loop）
JavaScript引擎负责解析，执行JavaScript代码，但它并不能单独运行，通常都得有一个宿主环境，一般如浏览器或Node服务器，前文说到的单线程是指在这些宿主环境创建单一线程，提供一种机制，调用JavaScript引擎完成多个JavaScript代码块的调度，执行（是的，JavaScript代码都是按块执行的），这种机制就称为事件循环（Event Loop）。

注：这里的事件与DOM事件不要混淆，可以说这里的事件包括DOM事件，所有异步操作都是一个事件，诸如ajax请求就可以看作一个request请求事件。

JavaScript执行环境中存在的两个结构需要了解：

消息队列(message queue)，也叫任务队列（task queue）：存储待处理消息及对应的回调函数或事件处理程序；
执行栈(execution context stack)，也可以叫执行上下文栈：JavaScript执行栈，顾名思义，是由执行上下文组成，当函数调用时，创建并插入一个执行上下文，通常称为执行栈帧（frame），存储着函数参数和局部变量，当该函数执行结束时，弹出该执行栈帧；
注：关于全局代码，由于所有的代码都是在全局上下文执行，所以执行栈顶总是全局上下文就很容易理解，直到所有代码执行完毕，全局上下文退出执行栈，栈清空了；也即是全局上下文是第一个入栈，最后一个出栈。

任务
分析事件循环流程前，先阐述两个概念，有助于理解事件循环：同步任务和异步任务。

任务很好理解，JavaScript代码执行就是在完成任务，所谓任务就是一个函数或一个代码块，通常以功能或目的划分，比如完成一次加法计算，完成一次ajax请求；很自然的就分为同步任务和异步任务。同步任务是连续的，阻塞的；而异步任务则是不连续，非阻塞的，包含异步事件及其回调，当我们谈及执行异步任务时，通常指执行其回调函数。

事件循环流程
关于事件循环流程分解如下：

宿主环境为JavaScript创建线程时，会创建堆(heap)和栈(stack)，堆内存储JavaScript对象，栈内存储执行上下文；
栈内执行上下文的同步任务按序执行，执行完即退栈，而当异步任务执行时，该异步任务进入等待状态（不入栈），同时通知线程：当触发该事件时（或该异步操作响应返回时），需向消息队列插入一个事件消息；
当事件触发或响应返回时，线程向消息队列插入该事件消息（包含事件及回调）；
当栈内同步任务执行完毕后，线程从消息队列取出一个事件消息，其对应异步任务（函数）入栈，执行回调函数，如果未绑定回调，这个消息会被丢弃，执行完任务后退栈；
当线程空闲（即执行栈清空）时继续拉取消息队列下一轮消息（next tick，事件循环流转一次称为一次tick）。
使用代码可以描述如下：


    var eventLoop = [];
    var event;
    var i = eventLoop.length - 1; // 后进先出

    while(eventLoop[i]) {
        event = eventLoop[i--]; 
        if (event) { // 事件回调存在
            event();
        }
        // 否则事件消息被丢弃
    }
这里注意的一点是等待下一个事件消息的过程是同步的。

并发模型与事件循环

    var ele = document.querySelector('body');

    function clickCb(event) {
        console.log('clicked');
    }
    function bindEvent(callback) {
        ele.addEventListener('click', callback);
    }   

    bindEvent(clickCb);
针对如上代码我们可以构建如下并发模型：

JavaScript并发模型

如上图，当执行栈同步代码块依次执行完直到遇见异步任务时，异步任务进入等待状态，通知线程，异步事件触发时，往消息队列插入一条事件消息；而当执行栈后续同步代码执行完后，读取消息队列，得到一条消息，然后将该消息对应的异步任务入栈，执行回调函数；一次事件循环就完成了，也即处理了一个异步任务。

再谈setTimeout(…0)
了解了JavaScript事件循环后我们再看前文关于setTimeout(...0)的例子就比较清晰了：

setTimeout(...0)所表达的意思是：等待0秒后（这个时间由第二个参数值确定），往消息队列插入一条定时器事件消息，并将其第一个参数作为回调函数；而当执行栈内同步任务执行完毕时，线程从消息队列读取消息，将该异步任务入栈，执行；线程空闲时再次从消息队列读取消息。

再看一个实例：


    var start = +new Date();
    var arr = [];

    setTimeout(function(){
        console.log('time: ' + (new Date().getTime() - start));
    },10);

    for(var i=0;i<=1000000;i++){
        arr.push(i);
    }
执行多次输出如下：

setTimeout(...0)

在setTimeout异步回调函数里我们输出了异步任务注册到执行的时间，发现并不等于我们指定的时间，而且两次时间间隔也都不同，考虑以下两点：

在读取消息队列的消息时，得等同步任务完成，这个是需要耗费时间的；
消息队列先进先出原则，读取此异步事件消息之前，可能还存在其他消息，执行也需要耗时；
所以异步执行时间不精确是必然的，所以我们有必要明白无论是同步任务还是异步任务，都不应该耗时太长，当一个消息耗时太长时，应该尽可能的将其分割成多个消息。

Web Workers
每个Web Worker或一个跨域的iframe都有各自的堆栈和消息队列，这些不同的文档只能通过postMessage方法进行通信，当一方监听了message事件后，另一方才能通过该方法向其发送消息，这个message事件也是异步的，当一方接收到另一方通过postMessage方法发送来的消息后，会向自己的消息队列插入一条消息，而后续的并发流程依然如上文所述。

JavaScript异步实现
关于JavaScript的异步实现，以前有：回调函数，发布订阅模式，Promise三类，而在ES6中提出了生成器（Generator）方式实现，关于回调函数和发布订阅模式实现可参见另一篇文章，后续将推出一篇详细介绍Promise和Generator。

参考：
Concurrency model and Event Loop


http://webcache.googleusercontent.com/search?q=cache:http://blog.codingplayboy.com/2017/04/25/js_async/&strip=1&vwsrc=0