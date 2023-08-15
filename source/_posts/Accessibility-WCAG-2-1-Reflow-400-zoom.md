---
title: Accessibility-WCAG 2.1 Reflow (400% zoom)
catalog: true
date: 2023-08-15 13:50:52
subtitle:
header-img:
tags:
categories:
- TECH
- FrontEnd
- Accessibility
---

基于 WCAG 2.1 Reflow (400% zoom) 标准不太好理解的情况，找到了一些 W3C 委员会对它的讨论和解释。

- [Change 1.4.10 Reflow to level A](https://github.com/w3c/wcag/issues/1050)
- [SC 1.4.10: What is the minimum height for vertically scrolling content?](https://github.com/w3c/wcag/issues/987)
- [WCAG 2.1 Understanding 1.4.10 Reflow - additional clarifications](https://github.com/w3c/wcag/issues/1188)

## 总结

讨论中也没有明确提及一个推荐测试用的固定分辨率，但可以确定的是我们不必一直在 320*256 下测试，可以适当放宽一些要求，比如测试 320*480。
480 是把现在最常见的 1920*1080 分辨率显示器竖直放置后由长边 1920 施加 400% 缩放得到的。
480 并未直接出现上面的讨论中，读完讨论结合实际情况理解得来的，如果考虑使用更大的高度来测试应该也可以，但不能确保那仍是符合规范的。

## responsive 模式测试问题

测 Reflow 的时候直接用浏览器的 devtools 的 responsive 模式测试可能会以 mobile 的形式渲染导致测不到一些 desktop 特有的问题，这里贴一下解决方法

The user Agent String:

```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.0.0 Safari/537.36
```

<iframe width="560" height="315" src="https://www.youtube.com/embed/3NlmMmb1ka4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>