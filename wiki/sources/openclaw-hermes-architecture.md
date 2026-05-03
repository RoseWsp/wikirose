---
type: article
date: 2026-05-03
author: unknown
url: unknown
raw: raw/clips/OpenClaw 和 Hermes Agent 到底是怎么分别构建.md
---

# OpenClaw 和 Hermes Agent 到底是怎么分别构建的

OpenClaw是"身体+大脑"，Gateway是承重墙；Hermes是"大脑即全部"，Agent自己就是最上层。这个结构性分歧几乎解释了两个代码库的一切不同。

## 核心分歧：谁在编排？

**OpenClaw**：Gateway是老大。AI大脑（Pi）作为独立运行时存在于Gateway之下，只是更大编排系统的一个组成部分。消息路由、session管理、事件调度全部由Gateway掌控。

**Hermes Agent**：AI大脑本身就是主要决策者。没有压在上面的Gateway。Agent直接掌握对话循环，消息平台、工具、记忆都是挂在Agent身上的。

一句话：OpenClaw是身体+大脑，Hermes是大脑即全部。详见[[agent-architecture-patterns]]。

## OpenClaw四层架构

1. **Channels层**：25+消息平台适配器（WhatsApp、Telegram、Discord、Slack、iMessage、Signal等），归一化为统一格式
2. **Gateway层**：WebSocket服务器充当中央神经系统，处理五类输入——人类消息、heartbeat、cron job、状态变更hook、外部webhook。一切皆事件
3. **Agent Runtime（Pi）**：agentic loop运行处，模型收prompt→决定处理→调工具→拿结果→下一步
4. **记忆层**：SOUL.md（人格与行为规则）+ MEMORY.md（事实与偏好）+ Dreaming系统（夜间三阶段：Light/REM/Deep，六因素加权打分，仅Deep写入）

Gateway承重，agent runtime被刻意分离为嵌入式进程。状态存JSON，原子写入保一致性。

## Hermes Agent五层架构

### 第1层：对话循环
同步while循环+预算计数器（每轮最多90次LLM调用，加1次宽限调用做总结）。OpenClaw无此上限，循环会一直跑到模型提供方停下。

三个关键机制：
- **预算**：预付费卡式上限
- **打断**：每轮检查用户新消息，有则优雅退出
- **压缩**：对话过长时裁剪旧工具结果→保护最近消息→总结中间部分。三轮仍过长则拆分会话，子会话关联父会话

### 第2层：Prompt系统
Session开始时一次性构造system prompt并缓存全生命周期。四个缓存断点：system prompt + 最近3条消息。从第二轮起每轮命中缓存。

两个额外缓存优化：
- JSON工具调用参数按字母序排序，key顺序不同也能命中缓存
- 同session复用同一AIAgent对象，缓存跨轮次存在

**OpenClaw相反**：每轮重新构造prompt，只加载本轮相关技能——prompt更精瘦；Hermes路线——prompt更容易缓存。取舍不同，目标一样：控制API开销。

### 第3层：工具系统
46个内置工具，启动时自动注册，无需配置文件。部分工具有快速可用性检查（缺API key则静默隐藏）。

执行环境六选一：本机、Docker、SSH远程服务器、Singularity（高校HPC集群）、Modal（serverless cloud）、Daytona（开发环境）。

并行处理：读取操作始终并行；写入操作并行执行，除非碰同一文件。

### 第4层：记忆系统（三本笔记本）
- **MEMORY.md**：用户明确告知的事实（时区、语言、项目约定）。Session开始时快照冻结进system prompt，session中不改
- **USER.md**："你是谁"——风格、偏好、雷区。可接外部提供方（Honcho、Mem0、Hindsight）
- **Skills**：完成复杂任务后写下的文档，扫描文件系统检索，下次使用时继续打磨

没有后台进程，没有额外LLM调用。初始对话结束后，记忆维护几乎"免费"。

### 第5层：学习循环
OpenClaw的skill是YAML frontmatter的Markdown，由用户编写、发布到ClawHub、安装后基本不变。

Hermes允许Agent自己创建和改进skill。完成任务后询问是否保存→写入`~/.hermes/skills/`→下次找到并执行→继续精炼。

闭环：做事→反思→生成skill→持久化→回忆→精炼。

**后果**：积累经验后，同类任务工具调用更少（skill文档已写明有效步骤），API成本可测量下降。

## Session持久化

| | OpenClaw | Hermes |
|---|---|---|
| 存储 | JSON/JSONL，原子写入 | SQLite，WAL模式，FTS5 |
| 检索 | LanceDB向量检索（语义相似强，精确关键词弱） | 全文关键词检索+总结（无需向量数据库） |
| schema迁移 | 无 | 第6版，带迁移机制 |
| 分叉 | 不支持 | `/branch`命令复制session，树状结构（parent_session_id外键） |

## 适配器层

**OpenClaw**：Gateway是WebSocket服务器，agent是子进程。按接口规范接入平台即自动获得session路由和事件排队。

**Hermes**：AIAgent是主进程，GatewayRunner是薄适配层。每个平台一个BasePlatformAdapter子类，归一化消息后直接交给Agent。Agent内置cron调度器。

## 多Agent

**OpenClaw**：Gateway supervisor tree，agent互传消息，深度可配置。Task Flows增加崩溃安全编排。→给你灵活性。

**Hermes**：每个子任务新建AIAgent。子agent只能用父agent已有工具，禁用delegation/clarify/memory/code_execution。最大深度默认2，独立IterationBudget上限50。→给你护栏。

## 核心洞察

> 两个代码库真正的架构差异，不只是功能或能力层面的差异，而是那些结构性的选择——正是这些选择，决定了后面一切是如何运作的。

---
*源文件：`raw/clips/OpenClaw 和 Hermes Agent 到底是怎么分别构建.md`*
