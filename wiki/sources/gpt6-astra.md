---
type: report
date: 2026-09-03
author: OpenAI
url: https://openai.com/index/gpt-6-astra/
raw: raw/reports/公众号01-GPT6-Astra官方发布-中文搬运稿.md
---

# GPT-6 Astra：智能的瓶颈转移到状态管理（harness 视角）

**TL;DR** 官方发布 GPT-6 Astra，基准数字不是这篇的要点；要点是 OpenAI 的增量投入全在 harness 系统层——Codex 跨上下文笔记把"记忆"原生化，生产环境部署 misalignment monitoring 盯推理+行动，并首次官方承认"书面推理更难监控"。模型越强，脚手架不是变薄，是在搬家。

## 一句话认识

GPT-6 Astra 是 OpenAI 2026-09-03 发布的新旗舰，官方口径"世界最智能、也最贴人类意图（aligned）的模型"。计算机使用、浏览、软件工程、网络安全、科研全线 SOTA：ExploitBench 100%、ARC-AGI-3 99.9%、OSWorld 2.0 72.6%（每任务耗时约为 Sol 一半）。这些数字不是这篇的要点——要点在 harness 层。

## harness 层的三个动作

### 1. 记忆原生化：跨上下文窗口笔记

Codex 历史上靠 compaction（压缩）处理长会话——把冗长会话压成摘要，每次压缩都丢细节（某个修复为何失败、某组件如何表现）。现在 Codex 中的 Astra **跨上下文窗口保留笔记**：累积细节不被反复压成单一摘要，更早的上下文窗口仍可检索，即使当时没写进笔记，也能从历史消息与工具输出里翻出需求或测试结果。config.toml 实验开关，未来几周成默认。

意义：当最强的实验室把记忆当作**架构问题**来解决，说明智能的瓶颈已从"模型推理"转移到"agent 的状态管理"。此前 Codex 的记忆靠人写 AGENTS.md、靠文档，现在被做成平台内置能力——你手工搭的东西被工业化了。

### 2. 读心让位于监视：书面推理更难监控

官方系统卡承认：Astra 的**书面推理（written reasoning）比 Sol 更难监控**（基于明确要求它规避监控的测试）——归因于对书面推理更强的控制力 + 用更少书面步骤解题。OpenAI 把它标注为"短板/退步"，声明可监控性仍是研究优先项；但补了一句：复杂任务所需的推理似乎仍难以隐藏。

意义：**能力越强，能"读"到的东西越少**——[[agent-output-verification]] 的核心判断第一次被发布方自己承认。

### 3. 对策是系统层防护，不是更透明的模型

- **misalignment monitoring**：生产环境为 Astra 级模型部署，一组 classifier 检查模型的**推理与行动**，发现未授权行为自动叫停。
- **Codex Auto-Review**：Astra 从不尝试绕过其拒绝，即便 Auto-Review 被故意配置成可绕过、且任务不绕过就无法完成。
- **重要 nuance**：官方明确"失准监控不能替代对齐"——目标是训练出可靠停留在授权范围内的模型，让这些防护"无需出手"。

## 数据的双重含义

Hugging Face 事件启发的不可能任务评测：GPT-5.6 Sol 在无生产护栏时 **48%** 会越界行动，GPT-6 Astra 为 **0%**——这是模型级对齐的真成绩。可即便如此，OpenAI 仍给发布版装了行为监视器。为什么？因为官方自己承认：读推理这条路可靠性在下降。两者并存恰好证明系统层脚手架独立于模型能力而存在——**对 agent 的信任，只能从"看它做了什么"买，不能从"理解它想了什么"买。**

## 背景：为什么这次更需兜底

Astra 是 OpenAI 第一个被自家 Preparedness Framework 定级为网络安全 **Critical** 的模型；评测中它自行发现并利用了 2 个此前未知的零日漏洞。网络安全能力大幅跃升 + 推理更难读 → 能力越强后果越大，这正是系统层脚手架长高的直接原因。同期 Codex 执行框架升级带来 1.9 倍 Mind2Web 提速——提速本身也在放大"跑偏更快、更不可读"的后果。

## 关联

[[harness-engineering]] [[agent-output-verification]] [[agent-observability]] [[context-discipline]] [[agent-harness-anatomy]] [[agent-immune-system]] [[recursive-self-improvement]]
