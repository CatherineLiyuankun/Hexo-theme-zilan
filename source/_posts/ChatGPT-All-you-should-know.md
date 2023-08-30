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
| chat GPT | chat | OpenAI | https://chat.openai.com/chat |  | - None found. | 注册普通账号，免费18美元额度；ChatGPT Plus `$20`/月 |

## `ChatGPT`和`OpenAI`和`Microsoft` 关系？

- ChatGPT是OpenAI开发的聊天机器人，ChatGPT属于OpenAI面向用户的一个产品。你可以视为子集，OpenAI是它爸。
- OpenAI很早就成立了，后面拿到天使融资和投资才不停的壮大发展，目前已经过度到快要变现盈利阶段。
- 然后OpenAI还有个金主爸爸叫微软Microsoft。这位金主爸爸给自家的bing.com搜索引擎和office 365植入这个ChatGPT功能

## ChatGPT与GPT-3.5（OpenAI API）的区别

在[OpenAI官方网页](https://openai.com/blog/chatgpt/)中，我们可以看到官方对ChatGPT的描述为
>“ChatGPT is fine-tuned from a model in the GPT-3.5 series, which finished training in early 2022. You can learn more about the 3.5 series [here](https://beta.openai.com/docs/model-index-for-researchers). ChatGPT and GPT 3.5 were trained on an Azure AI supercomputing infrastructure”

从而得知ChatGPT与GPT-3.5是两个不同产品
官方对GPT-3.5系列的介绍里，`text-davinci-003`是其中的模型之一
我们再查阅官方对[OpenAI API KEY的介绍](https://beta.openai.com/docs/introduction/key-concepts)，其中有一句

>“The API is powered by a set of models with different capabilities and price points. Our base GPT-3 models are called Davinci, Curie, Babbage and Ada”

davinci等模型都提到了

我们可以得出结论：

- 现在所有使用OpenAI API KEY的项目，都不是基于ChatGPT开发的项目，官方并未发布ChatGPT的API接口
- 事实上，ChatGPT最近发生过登录认证风波，想了解详细过程的可以查看这个[issue](https://github.com/acheong08/ChatGPT/issues/261)
- 如果你自己有分别使用过ChatGPT的官方chat和OpenAI的API接口聊天，你会发现API接口比ChatGPT的官方“笨”得多。ChatGPT使用的训练数据量和参数个数是远远比OpenAI的API的多的。

## AI模型总结

混淆人工智能、机器学习、深度学习、深度神经网络、人工智能模型、对抗神经网络、卷积神经网络、大语言模型、GPT-3等等概念？
![AI模型总结](http://img.laoda.de/i/2023/02/15/hiigmz-2.webp)


- 人工智能（Artificial Intelligence，AI）是研究和开发使计算机能够模拟和执行人类智能活动的科学和技术领域。人工智能模型是用于执行特定任务的计算机程序或算法，这些模型可以通过机器学习或深度学习来训练和优化。
  - 机器学习（Machine Learning，ML）是一种人工智能的分支，它关注让计算机通过学习数据和经验，自动改进和优化其性能的方法和算法。
  - 自然语言处理（Natural Language Processing，NLP）是研究计算机与人类语言交互的领域，旨在使计算机能够理解、解释和生成自然语言。

- 深度学习（Deep Learning，DL）是机器学习的一个子领域，它使用多层神经网络模型来学习和表示数据的复杂特征。深度学习是通过大量数据和多层次的表示学习来实现高度抽象的方法。
  - 深度神经网络（Deep Neural Network，DNN）是一种由多个神经网络层级组成的网络结构，用于进行模式识别和特征提取。深度神经网络是深度学习模型的基本组成部分。
    - 对抗神经网络（Generative Adversarial Network，GAN）是一种包含生成器和判别器的深度学习模型，用于生成具有逼真度的新数据，如图像、音频等。
    - 卷积神经网络（Convolutional Neural Network，CNN）是一种特殊类型的深度神经网络，主要用于处理和分析具有网格结构的数据，如图像和语音。
    - 递归神经网络模型（Recurrent Neural Network，RNN）是一种递归神经网络模型，用于处理序列数据，其中数据的前后顺序具有重要的意义。RNN的设计灵感来自于人类的思维过程，它通过在网络内部引入循环连接，使得网络可以在处理每个序列元素时保留之前的信息。
- 大语言模型（Large Language Model，LLM）是一种利用深度学习技术训练的模型，用于处理和生成类似人类语言的文本。GPT-3是一种著名的大语言模型。
- Transformer是一种基于自注意力机制的深度学习架构，广泛应用于自然语言处理任务。
  - GPT（Generative Pre-trained Transformer）是一系列基于Transformer架构的语言模型，由OpenAI开发。
    - ChatGPT是基于GPT-3模型的一个应用，它是一个交互式的聊天机器人，可以进行自然语言对话。
    - Bard是OpenAI的一个项目，旨在开发更有创造力和控制性的文本生成模型。虽然具体的细节尚未公开，但可以推测Bard可能是一种基于深度学习或神经网络的生成模型。Bard可能是建立在先进的语言模型技术之上，例如GPT（Generative Pre-trained Transformer）系列模型。GPT模型使用Transformer架构和大量的预训练数据来生成高质量的文本。Bard可能扩展了GPT模型的功能，以增加生成文本的创造性和控制性。
  - LaMDA（Language Model for Dialogue Applications）是Google开发的一种语言模型，旨在更好地理解和生成自然语言对话。LaMDA的目标是实现更自然、更连贯的对话交互。LaMDA的设计灵感来自于对话的特点，它专注于处理对话中的上下文和多轮交互。相较于传统的语言模型，LaMDA更加注重对话的语义理解和生成能力。

- 人工智能（AI）
  - 机器学习（ML）
    - 深度学习（DL）
      - Generative AI
        - 大语言模型（LLM）
      - 深度神经网络（DNN）
        - 对抗神经网络（GAN）
        - 卷积神经网络（CNN）

      - NLP（自然语言处理）另一种维度的分类，不是某个具体的模型。
        - 大语言模型（LLM）深度学习中的一个重要应用, 不是技术上的分类，用到深度学习的各种模型。
          - Transformer
            - GPT-3
              - ChatGPT
          - LaMDA
            - Bard

这些概念之间存在层级关系，其中人工智能（AI）是最广泛的概念，包括机器学习（ML）和自然语言处理（NLP）。
深度学习（DL）是机器学习的子领域，它包括深度神经网络（DNN）、对抗神经网络（GAN）和卷积神经网络（CNN）。
自然语言处理（Natural Language Processing，NLP）可以看作是深度学习的一个子领域。深度学习是机器学习的一个分支，专注于具有多个层次的神经网络，使得模型能够学习数据的层次化表示。而NLP则关注计算机与人类语言的交互，使计算机能够理解、解释和生成自然语言。
大语言模型（LLM）是深度学习中的一个重要应用，包括Transformer架构，其中GPT-3是其中的一个具体实现，而ChatGPT是基于GPT-3的一个聊天机器人应用。
此外，还有其他的语言模型如LaMDA和Bard，它们旨在推动文本生成的创造力和控制性。

NLP（自然语言处理）和LLM（大型语言模型）的关系？
- NLP（自然语言处理）和LLM（大型语言模型）是密切相关的领域。NLP是一个更广泛的领域，涉及到处理和理解人类语言的计算技术。它包括文本分类、情感分析、命名实体识别、机器翻译、问答等任务。
- 而LLM是NLP领域中的具体模型，利用深度学习技术处理和生成类似人类文本。LLM，例如GPT（生成式预训练转换器）模型，通过大量的文本数据训练，能够生成连贯且与上下文相关的回答。
- LLM显著推动了NLP领域的发展，为各种与语言相关的任务提供了最先进的性能。它们能够理解和生成文本，因此在聊天机器人、语言翻译、文本摘要和内容生成等任务中非常有用。
- 总之，NLP是一个更广泛的领域，涵盖了处理语言的各种技术和方法，而LLM是NLP领域内利用深度学习实现出色文本生成能力的具体模型。LLM是NLP工具箱中强大的工具，对于自然语言理解和生成的进展有着重要的贡献。

## GPT 相关项目

### 编辑器

[`Cursor`](https://www.cursor.so/) 一款集成Gpt-4机器人的编辑器。

### [DocsGPT](https://github.com/arc53/DocsGPT)

With its integration of the powerful GPT models, developers can easily ask questions about a project and receive accurate answers.

### Shell GPT

[Shell GPT](https://github.com/TheR1D/shell_gpt)，A command-line productivity tool powered by OpenAI's GPT-3.5 model. As developers, we can leverage AI capabilities to generate shell commands, code snippets, comments, and documentation, among other things. Forget about cheat sheets and notes, with this tool you can get accurate answers right in your terminal, and you'll probably find yourself reducing your daily Google searches, saving you valuable time and effort.

### ChatGPT 中文调用版

- 川虎ChatGPT 2.0 现已在GitHub开源
  - 仓库地址：https://github.com/GaiZhenbiao/ChuanhuChatGPT
  - b站视频：【ChatGPT帮你量子速读！开源客户端川虎ChatGPT重磅更新！】 https://www.bilibili.com/video/BV1184y1w7aP/?share_source=copy_web&vd_source=17c28da67621241803b4287cfdcf14c4
- https://new.ctgpt.cn/ [介绍](https://iui.su/3854/) 基于 OpenAI API (gpt-3.5-turbo)开发，免费无次数限制
  - 网页端：https://new.ctgpt.cn
  - 安卓端：https://wwji.lanzouf.com/iVoeB0o7wrxe
  - 苹果端：https://wwji.lanzouf.com/iYlRb0o7wryf 苹果端需要去设置里安装
  - 它可以和 new bing 一样 对回答内容的保守程度进行调整
  - 预设了一些常用prompt
  - 可以给 ChatGPT 设定角色
- https://chat.jorto.net/  免费中文版
- https://chatgpt.laoda.de/  需要填写自己的OpenAI账号的APIKEY
<!-- - https://gpt.chatapi.art/ ，不用科学上网，不用注册，直接提问 已经无法访问 -->

## OpenAI账号

注册网址：https://chat.openai.com/，需要

- 邮箱
- 国外手机号。如果没有国外手机号，可使用短信转发平台：https://sms-activate.org/

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

- 首先注册好OpenAI账号，之后点击链接：https://platform.openai.com/account/api-keys 即可创建API。
  - 默认18美元额度，剩余额度和使用期限可以在 <https://platform.openai.com/account/usage> 查看
- 基于OPENAI API KEY的网页应用，可以参考这个GitHub：
  - [使用GPT-3.5中的text-davinci-003模型，利用OpenAI API实现简单HTML网页版在线聊天](https://github.com/slippersheepig/chatgpt-web)

### ChatGPT 的API

另一种是ChatGPT的API。不要钱！也是邀请制度。申请一下隔天就可以通过。

申请方法：

- 在有OpenAI账号情况下
- 进入OpenAI个人面板 (https://platform.openai.com/overview)
- 顶部有一行最新的是“Join the GPT-4 API waitlist” 之前是“ChatGPT is coming to our API soon, sign up to stay updated”
- 点击sign up
- 申请资料填报加入候补名单
- 耐心等待1天时间就可以了

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
  - 最新的New bing已经不需要排队申请了。
  - [新必应（New Bing）国内申请与使用教程](https://juejin.cn/post/7199557716998078522#heading-2)
  - [总是跳转到国内版(cn.bing.com)？New Bing使用全攻略](https://juejin.cn/post/7202531472720592951#heading-2)

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

## GPT prompt 提示词使用技巧

### 吴恩达课程-ChatGPT Prompt Engineering for Developers

- 课程链接：[ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/)
- DeepLearningAI 的YouTUbe： https://www.youtube.com/@Deeplearningai/videos

- 吴恩达《ChatGPT Prompt Engineering for Developers》课程中文版:
  - [Git 课程中文版](https://github.com/datawhalechina/prompt-engineering-for-developers)
  - bilibili课程中文版视频地址：https://www.bilibili.com/video/BV1Bo4y1A7FU

### [Git - Prompt Engineering Topic](https://github.com/prompt-engineering)

- [prompt-patterns](https://github.com/prompt-engineering/prompt-patterns) Prompt 编写模式：如何将思维框架赋予机器
- [awesome-prompts](https://github.com/prompt-engineering/awesome-prompt-engineering)
- [Prompt-Engineering-Guide](https://github.com/dair-ai/Prompt-Engineering-Guide) Prompt工程师课程和论文

### [ChatGPT Shortcut](https://github.com/rockbenben/ChatGPT-Shortcut)

好用的提示词聚合网站 [ChatGPT Shortcut](https://www.aishort.top/)
简单易用的 ChatGPT 快捷指令表，让生产力倍增！ | 标签筛选、关键词搜索和一键复制 Prompts

### 针对ChatGPT和NewBing效果最好的中文提示词

https://qddmercny4.feishu.cn/sheets/shtcnMklYu0WsXEDUXXanrSEB2m

## Reference

- [大白话！简单解释ChatGPT和OpenAI还有API KEYS](https://blog.laoda.de/archives/chatgpt-and-openai)
- [手把手教你ChatGPT API Key申请使用和充值方法](https://cloud.tencent.com/developer/article/2232954)
- [手把手教你注册和使用ChatGPT](https://juejin.cn/post/7199657558834692157)