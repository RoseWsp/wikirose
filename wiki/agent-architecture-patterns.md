# Agent架构模式

AI Agent存在两种根本不同的架构模式：**Gateway-first**（外部编排层堆叠）和**Agent-first**（内部学习循环内化）。这不是功能差异，而是结构性选择——它决定了系统后续一切如何运作。([[openclaw-hermes-architecture]])

## TL;DR

Gateway-first把AI当组件塞进更大的编排系统；Agent-first让AI自己就是编排系统。前者扩张快，后者收敛强。

## Gateway-first：身体+大脑

代表：[[ai-agent-frameworks|OpenClaw]]

Gateway是承重墙。消息路由、session管理、事件调度、heartbeat、cron全由Gateway掌控。AI运行时（Pi）被刻意分离为嵌入式进程，只是系统的一个组成部分。

**优势**：接入新平台只需按接口规范写适配器，自动获得session路由和事件排队。生态扩张快——25+消息渠道、13000+社区技能的市场规模由此而来。

**代价**：复杂度外溢。Agent与Gateway是两个独立进程，状态同步需要JSON原子写入。prompt每轮重新构造以保持精瘦，代价是放弃缓存命中——每次调用都要重新处理全部token。记忆依赖夜间Dreaming系统（三阶段：Light/REM/Deep，六因素加权打分），只有Deep阶段写入，每天额外消耗API调用。多agent靠supervisor tree——灵活但没有护栏，agent间可互传消息、深度可配置，但缺少预算上限和工具白名单。循环没有LLM调用上限，会一直跑到模型提供方停下 ([[openclaw-hermes-architecture]])。

## Agent-first：大脑即全部

代表：[[ai-agent-frameworks|Hermes Agent]]

AIAgent是主进程。消息平台、工具、记忆全部挂在Agent身上。Gateway只是薄适配层。

**优势**：复杂度收敛进模型和学习循环。prompt一次构造全生命周期缓存，从第二轮起每轮命中缓存——API开销随时间递减。缓存策略有三个细节值得注意：(1) 四个缓存断点（system prompt + 最近3条消息），(2) JSON工具调用参数按字母序排序——key顺序不同也能命中缓存，(3) 同session复用同一AIAgent对象，缓存跨轮次存在。记忆三本笔记本（MEMORY.md + USER.md + Skills）无需后台进程。自我进化闭环（做事→反思→生成skill→持久化→回忆→精炼）让同类任务工具调用越来越少——skill文档已写明有效步骤，不需要重新摸索，API成本可测量下降。对话循环带预算计数器（每轮最多90次LLM调用+1次宽限调用做总结），对话过长时三轮压缩后拆分会话，支持`/branch`命令分叉为树状结构 ([[openclaw-hermes-architecture]])。

**代价**：对模型规模要求更高。学习曲线陡峭。子agent有严格护栏——只能用父agent已有工具，禁用delegation/clarify/memory/code_execution，最大深度默认2，独立IterationBudget上限50。灵活性受限，但防止成本指数级增长 ([[openclaw-hermes-architecture]])。

## 六个维度的结构性后果

### 1. API成本曲线

Gateway-first：prompt每轮重建，token消耗稳定不变。循环无LLM调用上限，跑到模型提供方停下。
Agent-first：prompt缓存（四个断点+JSON排序+对象复用） + skill积累减少工具调用 + 预算计数器硬性限流，成本随时间下降。

### 2. 记忆系统复杂度

Gateway-first：2个文件 + 夜间Dreaming进程（三阶段：Light/REM/Deep，六因素加权打分，仅Deep写入，额外API调用）。
Agent-first：3个文件，session开始时快照冻结进system prompt，session中途不改，无后台进程，维护"免费"。

### 3. 执行环境广度

Gateway-first：本机或Docker，二选一。
Agent-first：六选一——本机、Docker、SSH、Singularity（HPC）、Modal（serverless）、Daytona。Agent可以"住"在这些地方。

### 4. Session持久化

Gateway-first：JSON/JSONL + LanceDB向量检索。语义相似强，精确关键词弱。
Agent-first：SQLite WAL + FTS5全文检索，schema第6版带迁移。支持session分叉（树状结构）。

### 5. 安全哲学

Gateway-first：应用级检查，完全本地访问，信任用户。
Agent-first：多后端沙箱隔离，子agent工具白名单+预算上限+深度限制。

### 6. 进化路径

Gateway-first：社区市场驱动。skill由他人编写，安装后基本不变。横向扩展。13,000+社区技能的市场规模。
Agent-first：个人经验驱动。skill由agent自创自改进，越用越好。纵向深化。完成复杂任务后询问是否保存→写入`~/.hermes/skills/`→下次找到并执行→继续精炼，闭环导致API成本可测量下降 ([[openclaw-hermes-architecture]])。

## 为什么这个区分重要

这两种模式不是"哪个更好"的问题，而是**结构决定行为**。选了Gateway-first，你的系统天然适合快速扩张生态和团队协作；选了Agent-first，你的系统天然适合长期自主任务和成本收敛。试图在一种模式上嫁接另一种模式的优势，往往比从一开始就选对路径更昂贵。

一个典型例子：prompt策略。OpenClaw每轮重新构造prompt，只加载本轮相关技能——prompt更精瘦；Hermes一次性构造全生命周期缓存。取舍不同，目标一样：控制API开销。但两种策略的选择决定了后续一切——记忆系统、缓存架构、技能市场——都沿着这条路径分化 ([[openclaw-hermes-architecture]])。

这也解释了为什么[[ai-agent-frameworks|组合使用]]成为最佳实践——用Gateway-first做入口和分发，用Agent-first做执行和优化。 ([[openclaw-hermes-architecture]])

## 与相关概念的关系

- [[ai-agent-frameworks]] — 三足鼎立格局中的具体框架定位
- [[agentic-engineering]] — 大规模部署Agent需要的工程纪律
- [[action-based-ai]] — 两种架构模式都是行动派AI的技术实现
- [[product-taste]] — 架构模式选择本身就是产品品味决策
- [[general-specialized-architecture]] — 通用+专用架构是Gateway-first在更宏观层面的映射：通用编排器调用专用工具
- [[continual-learning]] — 持续学习是Agent-first架构自我进化的前提，也是当前Agent无法"交付后不管"的根因

---
*基于[[openclaw-hermes-architecture]]的深度架构对比分析。*
