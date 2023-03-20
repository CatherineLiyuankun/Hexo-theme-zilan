---
title: ChatGPT All you should know
catalog: true
date: 2023-03-20 20:40:15
subtitle:
header-img:
tags:
categories:
- TECH
- AI
---

# ChatGPT

| AI tools name | category | production company | URL | pros | cons | charging method and amount |
| --- | --- | --- | --- | --- | --- | --- |
| GPT-3 | writing | OpenAI | https://openai.com/gpt-3/ | - One of the most powerful AI writing tools on the market. <br> - Capable of generating human-like text. | - None found. | Paid |
| GPT-4 | writing | OpenAI | https://openai.com/product/gpt-4 | - GPT-4 is OpenAI’s most advanced system, producing safer and more useful responses | - None found. | Paid |
| chat GPT | chat | OpenAI | https://chat.openai.com/chat |  | - None found. | Paid |

## `ChatGPT`和`OpenAI`和`Microsoft` 关系？

- ChatGPT是OpenAI开发的聊天机器人，ChatGPT属于OpenAI面向用户的一个产品。你可以视为子集，OpenAI是它爸。
- OpenAI很早就成立了，后面拿到天使融资和投资才不停的壮大发展，目前已经过度到快要变现盈利阶段。
- 然后OpenAI还有个金主爸爸叫微软Microsoft。这位金主爸爸给自家的bing.com搜索引擎和office 365植入这个ChatGPT功能

## AI模型总结

混淆人工智能、机器学习、深度学习、深度神经网络、人工智能模型、对抗神经网络、卷积神经网络、大语言模型、GPT-3等等概念？
![AI模型总结](http://img.laoda.de/i/2023/02/15/hiigmz-2.webp)

## GPT 相关项目

### [DocsGPT](https://github.com/arc53/DocsGPT)

With its integration of the powerful GPT models, developers can easily ask questions about a project and receive accurate answers.

### ChatGPT 中文调用版

- https://chat.jorto.net/
- https://new.ctgpt.cn/ [介绍](https://iui.su/3854/)

## OpenAI账号

OpenAI只要是成功注册的账号都有API。
OpenAI账号不管是否PLUS都有免费的额度。目前来说是18刀免费账户额度。一天能花0.1刀个人问答都很厉害了的，OpenAI靠免费额度限制滥用。

功能 | 普通账号 | ChatGPT Plus
---------|----------|---------
 demand | Available when demand is low | - Available even when demand is high
 speed | Standard response speed | Faster response speed
 updates | Regular model updates | Priority access to new features 可以使用GPT-4
 token limit | 4,096 tokens which roughly translates to 500 words1. | 4,096 tokens which roughly translates to 500 words1.
 收费 | 免费，18刀免费账户额度 | `$20`/月

## API

### OpenAI的API

一种是OpenAI的API key 只要你有账号就都有。可以直接调用有账号情况下，这个模式下就可以自己制作机器人。不需要升级PLUS就可以实现。

申请方法：

首先注册好账号，之后点击这个链接：https://platform.openai.com/account/api-keys 即可创建API，默认18美元额度。

基于OPENAI API KEY的网页应用，可以参考这个GitHub：

使用GPT-3.5中的text-davinci-003模型，利用OpenAI API实现简单HTML网页版在线聊天

### ChatGPT 的API

另一种是ChatGPT 的API。不要钱！也是邀请制度。申请一下隔天就可以通过。

申请方法：

在有账号情况下——进入OpenAI个人面板 (https://platform.openai.com/overview) ——顶部有一行“ChatGPT is coming to our API soon, sign up to stay updated”点击sign up——申请资料填报加入候补名单——耐心等待1天时间就可以了

## GPT收费标准

### [GPT API 收费标准](https://openai.com/pricing)

首先，我们需要理解一个概念`token`，可以将token标记视为用于自然语言处理的单词片段。对于英文文本，1 个token标记大约为 4 个字符或 0.75 个单词。作为参考，莎士比亚全集约有 900000 字或 120 万个token标记。

其次，语言模型有非常多个，每个模型的能力不同，收费不同，主要的模型价格有：

Ada：$0.0004  / 1K tokens（最快的轻量模型）
Babbage：$0.0005  / 1K tokens
Curie：$0.0020  / 1K tokens
Davinci：$0.0200  / 1K tokens（能力最强的模型）
注意，我这里说的是语言模型，如果您使用图像模型来处理图片，价格需要另外支付图像模型的钱。

收费计算上，将输入的词数量加上生成的词数量，求和计算出token，然后根据模型的价格进行收费.
Token看似便宜，实际上需要回传历史消息才能延续上下文连续回话能力，何况当前还有4096个token的限制，真正使用下来，一个月也比Plus的`$20`定价也便宜不了多少。

### Token限制

GPT-3 不同model，token上限： https://platform.openai.com/docs/models/gpt-3
GPT-3.5 不同model，token上限：https://platform.openai.com/docs/models/gpt-3-5
GPT-4 不同model，token上限： https://platform.openai.com/docs/models/gpt-4

## ChatGPT 4

### GPT 4使用方法

- 方法1 使用ChatGPT Plus
  - ChatGPT Plus 为ChatGPT 收费版本，月费20美元，当中可让用户使用GPT-4，每4小时提问次数为100次。
- [Poe](https://apps.apple.com/us/app/poe-fast-ai-chat/id1640745955) 免费版用户可每4小时向GPT-4提问1次。如果是Poe收费订阅用户，则可每月提问300次。
- 新Bing 让你免费用GPT-4
  - Microsoft 已表示新Bing 已经使用GPT-4，如果用户在过去5周曾用过新Bing，那么现在已经可以使用GPT-4。

2023.3.20 目前为止GPT 4的各种使用方法都还没有开放功能图片功能。

### 如何得知使用的 Chatbot 在使用 GPT-4？

如果你问Chatbot，他们很可能会说在用GPT-3 或不告诉你用什么技术。不过，OpenAI 提供了一个GPT-4 实例如下：
> Andrew is free from 11 am to 3 pm, Joanne is free from noon to 2 pm and then 3:30 pm to 5 pm. Hannah is
available at noon for half an hour, and then 4 pm to 6 pm. What are some options for start times for a 30
minute meeting for Andrew, Hannah, and Joanne?
Andrew 上午 11 点到下午 3 点有空，Joanne 中午到下午 2 点有空，然后是下午 3:30 到 5 点。Hannah 中午有空半小时，然后是下午 4 点到 6 点。Andrew、Hannah 和 Joanne 的 30 分钟会议的开始时间有哪些选择？

GPT3 回答：
![GPT3 回答](https://www.yundongfang.com/wp-content/uploads/2023/03/GPT3-1024x592.webp-1.jpeg)

GPT4 回答：
![GPT 回答](https://www.yundongfang.com/wp-content/uploads/2023/03/GPT4-1024x501.webp-1.jpeg)

## 针对ChatGPT和NewBing效果最好的中文提示词

https://qddmercny4.feishu.cn/sheets/shtcnMklYu0WsXEDUXXanrSEB2m

## Reference

- [大白话！简单解释ChatGPT和OpenAI还有API KEYS](https://blog.laoda.de/archives/chatgpt-and-openai)
- [手把手教你ChatGPT API Key申请使用和充值方法](https://cloud.tencent.com/developer/article/2232954)

