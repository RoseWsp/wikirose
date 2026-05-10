---
type: blog
date: 2026-03-24
author: Prithvi Rajasekaran (Anthropic Labs)
url: https://www.anthropic.com/engineering/harness-design-long-running-apps
raw: raw/blog/anthropic-harness-design.html
---

# Harness design for long-running application development

Anthropic Labs团队将GAN（生成对抗网络）思想引入Agent架构的设计突破。将前端设计和全栈编码两个不同领域的经验统一到一个框架下。

### 核心内容

- **GAN启发式三Agent架构**：Planner（拓展spec）+ Generator（按sprint增量实现）+ Evaluator（Playwright做QA）
- **前端设计四维评分**：Design Quality、Originality、Craft、Functionality（权重倾斜质量和原创性）
- **Sprint Contract机制**：Generator和Evaluator在写代码前协商"done"的定义
- **Context Reset > Compaction**：清空上下文+结构化交接比原地压缩更有效（尤其对Sonnet 4.5的"Context Anxiety"）
- **迭代简化原则**：Opus 4.6需要比4.5少得多的脚手架；逐个移除组件测试其必要性
- **Evaluator调优**：需要多轮迭代才能让Evaluator的评判标准与人类对齐
- **效果数据**：全栈DAW应用约4小时/$124.70，3轮Build-QA循环

### 关键引述

> "将做事的Agent和评判的Agent分开，是一个强有力的杠杆（Powerful Lever）。"

> "Out of the box, Claude is a poor QA agent."

> "It is always good practice to experiment with the model you're building against, read its traces on realistic problems, and tune its performance."

### 关联页面

[[harness-engineering]]、[[agent-failure-modes]]、[[context-architecture]]、[[generator-evaluator-loop]]
