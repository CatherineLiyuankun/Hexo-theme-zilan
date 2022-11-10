---
title: cryptic abbreviations of Github comments
catalog: true
date: 2019-08-08 20:31:39
subtitle: Github 常用的迷之缩写
header-img:
tags:
- abbr
- git
categories:
- TECH
- SE life
---

我们Github code review 的时候第一次遇到这些缩写时，一脸懵逼，一无所知脸的偷偷去搜搜是什么意思？
这里整理一下这些缩写都是什么含义，以后我们也可以欢快地装逼了，装作娴熟的司机们来使用缩写来达到提高逼格的效果~~

* PR: Pull Request. 拉取请求，给其他项目提交代码
* LGTM: Looks Good To Me. ~~朕知道了~~ 代码已review，可以合并
* SGTM: Sounds Good To Me. 和上面那句意思差不多，也是已经通过了 review 的意思
* ACK — acknowledgement, i.e. agreed/accepted change 同意/接受改动
* NACK/NAK —negative acknowledgement, i.e. disagree with change and/or concept 不同意/接受改动
* RFC — request for comments, i.e. I think this is a good idea, lets discuss 我觉得不错，你怎么看？
* AFAIK/AFAICT — as far as I know / can tell 据我所知
* IIRC — if I recall correctly 如果我recall的正确的话
* IANAL — “I am not a lawyer”, but I smell licensing issues
* WIP: Work In Progress, do not merge yet. 传说中提 PR 的最佳实践是，如果你有个改动很大的 PR，可以在写了一部分的情况下先提交，但是在标题里写上 WIP，以告诉项目维护者这个功能还未完成，方便维护者提前 review 部分提交的代码。
* PTAL: Please Take A Look. 你来瞅瞅？用来提示别人来看一下
* TBR: To Be Reviewed. 提示维护者进行 review
* TL;DR: Too Long; Didn't Read. 太长懒得看。也有很多文档在做简略描述之前会写这么一句
* TBD: To Be Done(or Defined/Discussed/Decided/Determined). 根据语境不同意义有所区别，但一般都是还没搞定的意思
* NIT: Sometimes the reviewer will prefix his comments with "Nit:". This means that he's just "nitpicking" -- you don't have to fix these points, but we'd like you to. 指"吹毛求疵", 小问题（small or unimportant errors or faults），不强制要求修改，但建议修改。


有些也使用比特币的黑客术语：
* Concept ACK — agree with the concept, but haven’t reviewed the changes 理论上同意，但我还没review过。。。
* utACK (aka. Untested ACK) — agree with the changes and reviewed them, but didn’t test review过并同意改动，但我没测过~~~
* Tested ACK — agree with the changes, reviewed and tested 同意改动，我也review过并测过了


Reference links:
[LGTM? 那些迷之缩写](https://farer.org/2017/03/01/code-review-acronyms/)
[What do cryptic Github comments mean?](https://www.freecodecamp.org/news/what-do-cryptic-github-comments-mean-9c1912bcc0a4/)
