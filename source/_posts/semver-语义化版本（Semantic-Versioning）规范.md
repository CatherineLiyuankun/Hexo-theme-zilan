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

### `*` 不包括???

- 0.5.0-rc.1
- 1.0.0-rc.1
- 1.0.0-rc.2
- 1.0.0-rc.3

![*](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/*.png)

### 1.x.3 等同于1.x

![1.x.3](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/1.x.3.png)

### ^

![^0.2.1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/^0.2.1.png)
![^1.2.1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/^1.2.1.png)


### ~

![~4.11.1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/~4.11.1.png)


### -

![v2 - v3](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/semver/v2%20-%20v3.png)
