---
type: blog
date: 2026-05-11
author: Akshay (译：宝玉xp)
url: https://weibo.com/ttarticle/p/show?id=2309405297277882728607
raw: raw/blog/深度拆解：AI Agent Harness 的构造.md
---

# 深度拆解：AI Agent Harness 的构造

Akshay对Agent Harness的结构化全景拆解，横跨Anthropic、OpenAI、Perplexity和LangChain四家框架。核心贡献是冯·诺依曼架构类比和12组件分解。

### 核心内容

- **冯·诺依曼架构类比**：原生LLM=无内存CPU，上下文窗口=RAM，外部数据库=硬盘，工具=设备驱动，**Harness=操作系统**。Millidge："我们重新发明了冯·诺依曼架构，因为这是任何计算系统最自然的抽象方式"
- **Agent vs Harness区分**：Agent是用户感知的行为实体，Harness是产生这种行为的背后机器。"如果你不是模型本身，那你就是Harness"（LangChain Vivek Trivedy）
- **12个核心组件**：编排循环、工具、记忆、上下文管理、提示词构建、输出解析、状态管理、错误处理、护栏与安全、验证循环、子Agent编排
- **三层记忆架构**（Claude Code）：~150字符轻量索引（始终加载）→按需主题文件→仅搜索访问的原始日志。原则："Agent将自己的记忆视为一种提示，行动前必须根据实际状态验证"
- **上下文腐烂**：关键信息在窗口中间时模型表现下降30%+（斯坦福"迷失在中间"）。应对：压缩、观察掩码、即时检索、子Agent委托
- **错误处理四类**（LangGraph）：临时性（重试）、模型可恢复（错误作为工具消息返回）、用户可修复（暂停等人类）、意外错误（上报调试）
- **护栏三层**（OpenAI）：输入护栏→输出护栏→工具护栏，Tripwire机制即时停止
- **验证循环**：区分"玩具"和"生产级"的关键。Boris Cherny：让模型验证自己的工作，产出质量提升2-3倍
- **脚手架隐喻的推论**：房子盖好后脚手架要拆→**协同进化原则**：模型训练时已考虑Harness存在，Harness设计越好，模型升级时性能自动提升
- **7个关键决策**：单Agent vs 多Agent、ReAct vs 先规划后执行、上下文管理策略、验证循环设计、权限架构、工具范围、Harness厚度
- **框架对比**：Anthropic（笨循环+智慧在模型）、OpenAI（代码优先Python表达）、LangGraph（显式状态图）、CrewAI（角色协作）、AutoGen（多编排模式）

### 关键引述

> "如果你不是模型本身，那你就是Harness。" — LangChain Vivek Trivedy

> "我们重新发明了冯·诺依曼架构。" — Beren Millidge

> "仅仅改变Harness，就能让排名变动20多位。" — TerminalBench证据

### 关联页面

[[harness-engineering]]、[[agent-output-verification]]、[[generator-evaluator-loop]]、[[agent-immune-system]]、[[bounded-rationality]]、[[agent-isolation]]、[[anti-rationalization]]
