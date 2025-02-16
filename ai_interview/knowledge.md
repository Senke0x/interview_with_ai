# 飞书教程
- https://gofurther.feishu.cn/docx/Enofdl25BotoVrxth8ec4rNBn5c
# 本地教程
## 1. 什么是 LLM（Large Language Model）
### 1.1 基本概念
- LLM 是指在海量文本上进行训练、参数规模巨大的语言模型，能够理解和生成自然语言文本。
- 其核心是通过对上下文信息的理解，为各种任务（问答、翻译、写作、推理等）提供可行的、相对连贯的输出。
### 1.2 常见讨论话题
- 模型架构：如 Transformer 架构在 LLM 中的重要性（见下面“Transformer”章节）。
- 训练数据：模型是如何用海量文本数据进行训练，并能通过“记忆”和“泛化”来形成语言理解能力。
- 应用场景：问答、信息提取、对话系统、代码生成、文本摘要等。
- 局限性与风险：包括幻觉（Hallucination）、偏见（Bias）以及对隐私和安全的担忧。
### 1.3 常用 Blog 或 YouTube 链接
- OpenAI 官方博客（很多关于 GPT 系列的研究和应用）：https://openai.com/blog
- Andrew Ng 的 DeepLearning.AI 频道（介绍机器学习与深度学习的前沿）：https://www.youtube.com/@deeplearningai
- Two Minutes Paper（英文频道，介绍新晋 AI 论文，简单易懂）：https://www.youtube.com/@TwoMinutePapers

## 2. 什么是 Transformer
- 基于你提供的链接 “什么是 GPT？通过图形化的方式来理解 Transformer 架构 [译] | 宝玉的分享” ，可得到以下简要总结。
### 2.1 基本概念
- Transformer 是 2017 年 Google 提出的神经网络架构，核心组件是“自注意力机制（Self-Attention）”，能够并行地处理序列数据。
相较于传统的 RNN/CNN，Transformer 不需要严格的时序递归，训练效率高且能更好地捕捉长距离依赖关系。
### 2.2 常见讨论话题
- 注意力机制（Attention）如何帮助模型了解上下文中的重要信息。
- Encoder-Decoder 结构：Encoder 适合理解输入语义、Decoder 负责预测或生成。GPT 则是只用 Decoder 的 Transformer。
- 多头注意力（Multi-Head Attention）与前馈网络（Feed-Forward Layer）在实际实现中的细节作用。
- 位置编码（Positional Encoding）是如何在无卷积/循环结构下，让模型依旧“知道”输入的位置关系。
### 2.3 常用 Blog 或 YouTube 链接
- 原论文《Attention is All You Need》：https://arxiv.org/abs/1706.03762
- Jay Alammar 的可视化博客（图解 Transformer 非常直观）：https://jalammar.github.io/

## 3. 什么是 Prompt
### 3.1 Prompt Engineering 的定义
- Prompt：在与大型语言模型交互时，向模型提供的输入描述或指令，使模型按照人类预期去生成文本。
- Prompt Engineering：通过设计或微调 Prompt，提升模型生成文本的准确性、相关性或创意度。
### 3.2 常见讨论话题
- Prompt 结构：包括 System Prompt、User Prompt、以及可选的 Few-shot 示例。
- 指令式 Prompt（Instruction-based）与角色式 Prompt（Role-based）的区别和应用场景。
- 提示词的迭代：如何在多轮交互中不断完善提示，使得模型输出更符合需求。
- 在工业应用中如何使用 Prompt 模板化（Prompt Templates）来适应不同任务。
### 3.3 常用 Blog 或 YouTube 链接
- GitHub 上各种 Prompt 工程示例：https://github.com/f/awesome-chatgpt-prompts
- Prompt Engineering 入门教程（YouTube 搜索 “Prompt Engineering tutorial” 有很多相关资源）

## 4. 什么是 RAG（Retrieval-Augmented Generation）
- 基于你提供的链接 “RAG 系统开发中的 12 大痛点及解决方案 [译] | 宝玉的分享” ，可得到以下信息。
### 4.1 基本概念
- RAG 指的是在生成式模型基础上，额外整合检索步骤：先从知识库中找到与问题相关的文档或信息，再将这些信息传给语言模型进行生成。
- 好处：减少“幻觉”，增强回答的事实准确度，且能够动态更新知识库而无需每次都大规模微调语言模型。
### 4.2 常见讨论话题
- 检索方式：常见如向量搜索，如何进行嵌入（Embedding），以及如何处理长文本切分（chunk_size）。
- 索引与排序：similarity_top_k、reranker、embedding 微调等细节。
- 上下文窗口的限制与信息丢失：如何应对文档过长造成的上下文切分问题。
- 长文本场景下如何进行信息压缩、LongContextReorder等策略。
- 数据质量与数据清洗在 RAG 中的重要性。
### 4.3 常用 Blog / YouTube 链接
- Hugging Face 关于 RAG 的官方介绍：https://huggingface.co/docs/transformers/main_classes/rag
- Haystack 文档（流行的 RAG 解决方案之一）：https://haystack.deepset.ai/overview/introduction
- Twitter 上关于 RAG 的讨论（devv.ai 的作者）：https://x.com/forrestzh_/status/1731478506465636749
## 5. 什么是 Agent
### 5.1 基本概念
- 在当前对话式 AI 场景下，“Agent” 常指可自动执行多步任务的智能体，它会先解析用户意图，再通过工具或插件去获取信息或调用外部操作，最终给出结果。
- 一般在 LangChain 或类似框架中，Agent 会利用“思维链式提示”来规划执行步骤，并调用 API、检索数据库、执行计算等。
### 5.2 常见讨论话题
- Agent 思维流程：如何让模型产生“工具使用结论”与“最终回答”分离（ReAct 思想）。
- 安全与可控性：当 Agent 拥有执行外部操作的权限时，需要避免滥用或越权。
- 工具接入：如查询数据库、调用第三方 API、执行 Python 代码等技术细节。
### 5.3 常用 Blog / YouTube 链接
- LangChain 官方对 Agents 的介绍：https://python.langchain.com/docs/modules/agents
- Harrison Chase 的技术分享（LangChain 主要作者，YouTube 搜索 “LangChain Harrison Chase”）。

## 6. 什么是 LangChain
### 6.1 基本概念
- LangChain 是一个框架，提供了一整套工具让开发者可在大型语言模型之上快速构建应用，包括 Prompt 模板、内存管理、检索整合、Agent 工作流等功能模块。
### 6.2 常见讨论话题
- LangChain 核心概念：PromptTemplate、LLMChain、ConversationBufferMemory、VectorStore、Agent、Tool 等。
- 模块化与可扩展性：如何使用不同的插桩（Hooks）或组件对接自定义功能，如检索器、数据库、API 工具等。
- 性能与部署：面向生产部署时如何进行拓展、监控与调试。
### 6.3 常用 Blog / YouTube 链接
- LangChain 官方文档：https://langchain.com/
- 官方 GitHub：https://github.com/hwchase17/langchain