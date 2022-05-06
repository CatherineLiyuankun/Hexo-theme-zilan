---
title: >-
  "Hexo fs.SyncWriteStream is deprecated"
catalog: true
date: 2019-05-13 15:08:08
subtitle: "(node:28561) [DEP0061] DeprecationWarning: fs.SyncWriteStream is deprecated."
header-img:
tags:
- Hexo
- Blog
- node.js
categories:
- TECH
- Hexo
---

# Problem

NodeJs V8 使用hexo时报错：

(node:28561) [DEP0061] DeprecationWarning: fs.SyncWriteStream is deprecated.

``` bash
➜  Hexo-theme-zilan git:(master) ✗ hexo g
(node:28561) [DEP0061] DeprecationWarning: fs.SyncWriteStream is deprecated.
INFO  Start processing
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
TypeError: Cannot set property 'lastIndex' of undefined
    at highlight (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/highlight.js/lib/highlight.js:511:35)
    at /Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/highlight.js/lib/highlight.js:561:21
    at Array.forEach (<anonymous>)
    at Object.highlightAuto (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/highlight.js/lib/highlight.js:560:40)
    at /Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/hexo-util/lib/highlight.js:117:25
    at highlight (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/hexo-util/lib/highlight.js:120:7)
    at highlightUtil (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/hexo-util/lib/highlight.js:22:14)
    at /Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/hexo/lib/plugins/filter/before_post_render/backtick_code_block.js:62:15
    at String.replace (<anonymous>)
    at Hexo.backtickCodeBlock (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/hexo/lib/plugins/filter/before_post_render/backtick_code_block.js:14:31)
    at Hexo.tryCatcher (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/util.js:16:23)
    at Hexo.<anonymous> (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/method.js:15:34)
    at Promise.each.filter (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/hexo/lib/extend/filter.js:63:65)
    at tryCatcher (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/util.js:16:23)
    at Object.gotValue (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/reduce.js:155:18)
    at Object.gotAccum (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/reduce.js:144:25)
    at Object.tryCatcher (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/promise.js:512:31)
    at Promise._settlePromise (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromiseCtx (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/promise.js:606:10)
    at Async._drainQueue (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/async.js:138:12)
    at Async._drainQueues (/Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/bluebird/js/release/async.js:143:10)
```

## Root cause

hexo-fs 老版本里有一行：

```
    exports.SyncWriteStream = fs.SyncWriteStream;
```

跟nodejs v8 有冲突。所以要更新 hexo-fs >= ^0.2.0

# Solutions

## Fix 1 use old version of nodejs

用nvm管理node版本。发现切换node后，zsh: command not found: hexo。
重新npm install hexo-cli -g 就好了

 ```
    ➜  Hexo-theme-zilan git:(master) ✗ nvm list
            v7.4.0
    ->       v8.9.1
            v9.3.0
    ➜  Hexo-theme-zilan git:(master) ✗ nvm use v7.4.0
    Now using node v7.4.0 (npm v4.0.5)
    ➜  Hexo-theme-zilan git:(master) ✗ npm install
    ➜  Hexo-theme-zilan git:(master) ✗ hexo g
    zsh: command not found: hexo

    ➜  Hexo-theme-zilan git:(master) ✗ npm install hexo-cli -g
```

## Fix 2 install hexo-fs

如果还想使用nodejs > v8, 可以更新hexo-fs

```
    ➜  Hexo-theme-zilan git:(master) ✗ npm install hexo-fs –save
```

试了下还是没解决。。。 Try again, still has the error...

## Fix 2 hexo --debug

会发现hexo-deployer-git 里使用了旧版本的hexo-fs，所以造成问题

  ```
    ➜  Hexo-theme-zilan git:(master) ✗ hexo --debug
        07:05:51.382 DEBUG Hexo version: 3.7.1
        07:05:51.385 DEBUG Working directory: ~/MyOwnGit/Hexo-theme-zilan/
        07:05:51.513 DEBUG Config loaded: ~/MyOwnGit/Hexo-theme-zilan/_config.yml
        07:05:51.579 DEBUG Plugin loaded: hexo-deployer-git
        (node:29976) [DEP0061] DeprecationWarning: fs.SyncWriteStream is deprecated.
        07:05:51.728 DEBUG Plugin loaded: hexo-fs
        07:05:51.731 DEBUG Plugin loaded: hexo-generator-archive
        07:05:51.733 DEBUG Plugin loaded: hexo-generator-category
        07:05:51.737 DEBUG Plugin loaded: hexo-generator-feed
        07:05:51.738 DEBUG Plugin loaded: hexo-generator-index
        07:05:51.783 DEBUG Plugin loaded: hexo-generator-seo-friendly-sitemap
        07:05:51.784 DEBUG Plugin loaded: hexo-generator-tag
        07:05:51.788 DEBUG Plugin loaded: hexo-renderer-ejs
        07:05:52.277 DEBUG Plugin loaded: hexo-renderer-jade
        07:05:52.278 DEBUG Plugin loaded: hexo-renderer-markdown-it
        07:05:52.280 DEBUG Plugin loaded: hexo-renderer-stylus
        07:05:52.360 DEBUG Plugin loaded: hexo-server
        07:05:52.364 DEBUG Script loaded: themes/zilan/scripts/fancybox.js
   ```

## Fix 2 modify hexo-deployer-git

 ```
    ➜  Hexo-theme-zilan git:(master) ✗ npm install hexo-deployer-git hexo-serve --save
 ```

试了下还是没解决。。。 Try again, still has the error...
看了下hexo-deployer-git并没什么更新，只能自己手动改了

注释掉 /Users/liyuankun/MyOwnGit/Hexo-theme-zilan/node_modules/hexo-deployer-git/node_modules/hexo-fs/lib/fs.js 中的

```javascript
    //exports.SyncWriteStream = fs.SyncWriteStream;
```

# Reference Links

[fs.SyncWriteStream is deprecated [Nodejs v8.0]](https://github.com/hexojs/hexo/issues/2598)
