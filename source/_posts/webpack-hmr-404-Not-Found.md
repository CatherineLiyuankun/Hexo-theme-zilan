---
title: __webpack_hmr 404 (Not Found)
catalog: true
date: 2023-07-13 11:50:04
subtitle:
header-img:
tags:
- Webpack
categories:
- TECH
- FrontEnd
- BuildTool
---

调试 `webpack-dev-server` 和 `webpack-dev-middleware` 的时候，突然发现了控制台出现了一个错误提示：

```bash
GET http://localhost:8080/__webpack_hmr 404 (Not Found)
```

 webpack.config.js 配置文件：

```javascript
 module.exports = {
  // ...
  entry: [
    'webpack-hot-middleware/client',
    './src/index.js'
  ],
  devServer: {
    hot: true,
    open: true,
    inline: false
  },
}
```

发现入口文件有一个 webpack-hot-middleware/client，经过一番搜索，在 Stack Overflow 有一个类似的提问 [Stack Overflow Webpack hmr: __webpack_hmr 404 not found](https://stackoverflow.com/questions/41342144/webpack-hmr-webpack-hmr-404-not-found)。

大概原因是，webpack-hot-middleware/client 是 webpack-hot-middleware 的要求，可用于除 webpack-dev-server 之外的任何服务器（例如 express 或类似服务器），所以把它从入口文件删去就好了。

## 参考文章

- [__webpack_hmr 404 (Not Found)](https://www.jianshu.com/p/b4f70049afad)
- [Stack Overflow Webpack hmr: __webpack_hmr 404 not found](https://stackoverflow.com/questions/41342144/webpack-hmr-webpack-hmr-404-not-found)
