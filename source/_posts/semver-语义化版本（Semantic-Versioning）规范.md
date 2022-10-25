---
title: semver - 语义化版本（Semantic Versioning）规范
catalog: true
date: 2022-10-25 23:07:46
subtitle:
header-img:
categories:
- TECH
- FrontEnd
- node.js
tags:
- node.js
---

## semver 官网+基本概念

- [npm semver](https://www.npmjs.com/package/semver)
  - [github npm/node-semver](https://github.com/npm/node-semver)
- [npm semver calculator](https://semver.npmjs.com/)
  - [semantic versioning](https://docs.npmjs.com/about-semantic-versioning)
- [语义化版本控制模块-Semver](https://juejin.cn/post/6844903516754935816)

### `x、X、*` 通配符

#### `*` 不包括???

- 0.5.0-rc.1
- 1.0.0-rc.1
- 1.0.0-rc.2
- 1.0.0-rc.3

![*](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/*.png)

#### 1.x.3 等同于1.x

![1.x.3](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/1.x.3.png)

### ^

`^` ：表示同一主版本号中，不小于指定版本号的版本号（允许在不修改[major, minor, patch]中最左非零数字的更改（匹配大于X、Y、Z的更新Y、Z的版本号））

在X.Y.Z结构的版本号中，X、Y、Z都是非负的整数，上面定义的意思就是说从左向右，遇到第一个非零数字是不可修改的，下一个数字可以更改，比如:

- X、Y、Z都不为0，`^15.6.1`,最左的非零数字是15，所以X是不允许更新的，也就是说主版本号不会超过15，表示的就是版本号`>=15.6.1 && <16.0.0`
- 如果X为0，那么第一个非零数字就是Y，就只能对z做出修改，`^0.1.2`表示版本号`>=0.1.2 && < 0.2.0`
- 如果X、Y的数字都是0的话，第一个非零数字就是Z，表示的就是版本号不允许更新；`^0.0.2`，主版本号和次版本号都是0，修订号为非零，表示的就是版本号`>=0.0.2 && < 0.0.3`


`^0.2.1` 表示 `>=0.2.1 && < 0.3.0`

![^0.2.1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/^0.2.1.png)
![^1.2.1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/^1.2.1.png)


### ~

~ ：表示同一主版本号和次版本号中，不小于指定版本号的版本号
匹配大于X.Y.Z，更新Z的版本号

- X、Y、Z都不为0，`~1.2.3`表示版本号`>=1.2.3 && < 1.3.0`
- X为0，`~0.2.3`表示版本号`>=0.2.3 && < 0.3.0`，这种情况下，~等价于^
- X、Y为0，`~0.0.3`表示版本号`>=0.0.3 && < 0.1.0`

![~4.11.1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/~4.11.1.png)


### -

`>、<、=、>=、<=、-`：用来指定一个版本号范围

![v2 - v3](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/v2%20-%20v3.png)

### ||

||：表示或
 `^2 <2.2 || > 2.3`

## npm 中 package-lock.json 的一些坑

在 npm install 后，会生成一个 package-lock.json 文件用于保存当前安装依赖的各种来源及版本号。

在 npm 5.4.2版本后，package-lock.json 的变动规则：

- 当在 install dependency 的指定版本时，会自动更新 package-lock.json 文件中该 dependency 的 version 到指定的 version
- 当在 install dependency 的范围版本时
  - 当前的 version `<=` package-lock.json 文件中对应的 dependency 的 version 时，会安装 package-lock.json 中的 version；
  - 当前的 version `>` package-lock.json 中对应的 dependency 的 version 时，会安装当前范围版本号中最高的版本，会更新 package-lock.json 文件中对应的版本号；

```json
package.json
"antd": "^3.6.1", // eg：最新版本是 3.9.4

package-lock.json
"antd": "3.7.1",

// 执行npm install 会安装 3.7.1 版本
```


## 参考文章

- [semver 语义化版本规范](https://www.jianshu.com/p/a7490344044f)
- [语义化版本控制模块-Semver](https://juejin.cn/post/6844903516754935816)
