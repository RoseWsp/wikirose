---
type: blog
date: 2026-02-11
author: Ryan Lopopolo (OpenAI)
url: https://openai.com/index/harness-engineering/
raw: raw/blog/openai-harness-engineering.html
---

# Harness engineering: leveraging Codex in an agent-first world

OpenAI团队用Codex构建百万行代码产品的完整经验分享。3→7人团队，5个月，一行人工代码未写，交付~1M LOC、1,500 PRs。

### 核心内容

- **AGENTS.md是地图不是百科全书**：~100行的索引，指向深层docs/目录。实现了"渐进式披露"
- **代码仓库即记录系统**：所有知识必须版本化地存在于仓库中——Slack讨论、Google Docs对Agent来说不存在
- **约束编码化**：Custom Linter + Structure Tests + Taste Invariants，完全替代文档层面的"建议"
- **"Waiting is expensive, fixing is cheap"**：智能体吞吐量远超人类注意力时，纠错成本低而等待成本高
- **熵的垃圾回收**：后台Agent定期扫描偏差，发起重构PR。"技术债务就像高息贷款，持续还小额比积累后一次解决痛苦少得多"
- **6+小时单次运行**：Codex常在人类睡眠时间持续工作，处理单任务超6小时
- **Agent审核Agent**：几乎所有审核工作从人工转向Agent-to-Agent
- **从25%到90%的自主度提升**：从辅助到端到端驱动新功能（验证→修复→测试→PR→合并）

### 关键引述

> "When everything is 'important,' nothing is."

> "Waiting is expensive, fixing is cheap."

> "The agent's knowledge boundary equals the repository's file boundary."

> "If it can't be mechanically enforced, the agent will drift."

### 关联页面

[[harness-engineering]]、[[agent-native-tooling]]、[[agent-output-verification]]、[[agent-matrix]]、[[entropy-garbage-collection]]、[[architect-operator-model]]、[[self-healing-pipeline]]、[[scope-discipline]]
