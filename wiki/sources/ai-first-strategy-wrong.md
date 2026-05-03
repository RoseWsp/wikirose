---
type: article
date: 2026-04-14
author: Peter Pang (CREAO), 宝玉xp (翻译/评论)
url: https://weibo.com/ttarticle/p/show?id=2309405287623509016731
raw: raw/clips/为什么你的″AI 优先″战略可能大错特错.md
---

# 为什么你的"AI 优先"战略可能大错特错？

**TL;DR** AI First 听着美好，但没有工程基础支撑就是在沙子上盖楼。与其说 AI First，不如说软件工程 First——测试、CI/CD、监控、架构、任务管理做扎实了，AI 的能力自然释放。

![](https://wx4.sinaimg.cn/large/66fd066bgy1ic6c9nxc4aj20zk0jz783.jpg)

## 核心叙事

CREAO（25人AI Agent平台公司）实现了99%生产代码由AI编写，每天3-8次部署，功能当天上当天撤。这不是装个Copilot插件就能做到的——他们彻底重构了整个工程流程。

**三个致命瓶颈**驱动了这场变革：PM花几周做需求vs AI两小时实现、QA测三天vs AI写代码两小时、25人vs对手数百人。解决方案不是加人，而是把人从链条里拿掉，让AI端到端负责。

## 关键概念：脚手架工程

OpenAI 2026年2月提出的概念，CREAO在实践中先行摸索出了同一路径：**工程团队的核心工作不再是写代码，而是赋能智能体让它们完成有价值的工作。** 当系统出错，不是"再试一次"，而是问：AI缺失了什么能力？如何让这个能力对智能体清晰可见？

## AI First的五大前提

1. **自动化测试**——没有测试覆盖，AI每次提交都得人工回归
2. **CI/CD流水线**——从提交到部署全自动化，否则代码堆积等人
3. **A/B测试和线上监控**——没有数据说话，AI一天产五个功能你不知道留哪个
4. **任务管理**——任务拆到合适粒度，多Agent并行时谁做哪个、哪个优先
5. **系统架构**——架构太乱AI跟人一样头疼，改一处崩三处

![](https://wx1.sinaimg.cn/large/66fd066bly4ic6c70wsqmj21hr0u00z6.jpg)

## 适合vs不适合的场景

**适合**：后端逻辑为主（API服务、数据处理）、内部工具、早期产品快速试错

**不适合**：UI密集产品（AI搞不定复杂界面交互）、功能质量敏感产品（Anthropic/OpenAI都不敢在核心产品上全自动迭代）、安全性要求高场景（银行、交易平台）

## 自愈反馈循环

整个体系的灵魂：每天早上自动健康检查→Claude分析错误模式→分诊引擎聚类评估→自动创建工单（含日志、影响范围、排查方向）→工程师验证修复→CI/CD验证→部署→分诊引擎复检→工单自动关闭。同一套流水线，新功能和Bug修复共用。

![](https://wx3.sinaimg.cn/large/66fd066bly4ic6c71b8q3j21hr0u043n.jpg)

## 架构师-操作员模型

未来只有两种工程师：**架构师**（1-2人，设计脚手架、定义"好"的标准、批判AI方案）和**操作员**（验证诊断、审核风险）。反直觉发现：初级工程师比资深工程师适应更快——没有旧习惯要破除。

**批评AI的能力将比写代码的能力更有价值。**

## 宝玉xp的评论

原文看着在讲AI，底下全是软件工程。AI First的真正终点未必是让AI干所有活，而是借着这股力量，把一直想做但没动力做的工程改进真正推动起来。仰望星空，脚踏实地。

## 与wiki现有概念的关联

- [[harness-engineering]]——本文的核心概念
- [[ai-first-prerequisites]]——五大前提条件
- [[architect-operator-model]]——新的工程组织架构
- [[self-healing-pipeline]]——自愈反馈循环
- [[agentic-engineering]]——脚手架工程是Agentic Engineering的具体实践
- [[vibe-coding]]——本文明确批评Vibe Coding只能做原型验证
- [[product-taste]]——架构师的核心价值是批判性思维和产品品味
- [[action-based-ai]]——AI First是行动派AI在组织层面的落地
- [[role-convergence]]——架构师-操作员模型是角色融合的极端形式
- [[dual-horizon-planning]]——CREAO的极快迭代周期是双极规划的另一种体现
- [[dogfooding-as-method]]——CREAO用智能体平台重建智能体平台
