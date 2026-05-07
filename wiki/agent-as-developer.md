# Agent 即开发者 (Agent as Developer)

**TL;DR** Fork的单位是开发者，不是分支。给agent一张桌子、一台电脑、一个独立环境，让它push branch like everyone else。

## 这意味着什么

当你说"另一个开发者加入团队"时，你给他的不是你checkout的Git worktree——你给他clone repo、装依赖、跑app、push branch的全部自主权。Agent应该得到同样的待遇。

Finbarr Taylor的核心洞察：**Git worktree只隔离了.git，但一个开发者需要的远不止git。** 依赖、缓存、环境变量、运行时服务——这些都不在版本控制里，但全是"开发者的机器"上不可少的部分。用分支建模"另一个开发者"是错配的抽象 ([[finbarr-treat-agents-like-developers]])。

## 从worktree到"给Alice一张桌子"

> 如果我雇了Alice，我不会说"Alice，请作为我当前checkout的Git worktree操作"。我会说"Alice，clone repo，装依赖，跑app，做完push branch。"

这个对比揭示了一个深层模式：**人类团队已经发明了完整的协作协议**——各自clone、各自commit、remote是同步点、PR是审查点。Agent只需要走同样的路。

yolobox用命名强化了这个心智模型：

```bash
yolobox fork --name alice codex
yolobox fork --name bob claude
yolobox fork --name carol codex
```

不是`--name new-billing-flow`，是人名。每个fork是"另一个开发者的机器"。

## 目标：让agent更不特殊

> "The goal is not to make agents special. The goal is to make agents *less* special."

这句话是整篇文章的承重墙。AI-native不是让agent变成魔法存在，而是让它降格为"初级开发者"——需要自己的工位、自己的环境、自己的审查流程，也需要和人类一样的工程纪律。

这与Addy Osmani的[[addyosmani-agent-skills|Agent Skills]]形成完美互补：

| 维度 | Finbarr (yolobox) | Addy (Agent Skills) |
|---|---|---|
| 解决什么 | "身体"——环境隔离 | "纪律"——流程约束 |
| 核心机制 | 全量拷贝 + 命名空间 | 反合理化表格 + 退出标准 |
| 隐喻 | 给agent一张桌子 | 让agent走完SDLC |
| 缺了什么 | 有桌子没纪律 | 有纪律没桌子 |

合在一起才是完整的"agent = developer"：一个初级开发者需要的不只是一台电脑，还需要有人盯着他走完spec → plan → build → test → review → ship。

## 抽象之梯上的位置

用[[abstraction-ladder|抽象之梯]]来看：

- **贴脸** — `yolobox fork --name alice codex`
- **站远** — 每个agent独立的文件系统 + Compose命名空间 + URL
- **更远** — [[agent-isolation|隔离是并行的前提]]，全量拷贝胜过精巧方案
- **最远** — **AI-native的瓶颈不在模型能力，在运营基础设施**。通向AI-native的路不是让agent更魔法，而是让它更不特殊

最远那一层与wiki多条线索共振：[[harness-engineering|脚手架工程]]（瓶颈在护栏不在模型）、[[org-process-gap|组织流程代差]]（瓶颈在流程不在技术）、[[clarity-before-automation|先清晰再自动化]]（瓶颈在清晰不在自动化）。同一枚硬币的不同面。

## 关联

- [[agent-isolation]] — agent即开发者的基础设施后果：需要开发者级别的隔离
- [[harness-engineering]] — 脚手架工程为agent搭护栏，agent-as-developer为护栏提供正确的心智模型
- [[agent-matrix]] — Agent矩阵的每个节点都是一个"开发者"，需要独立工位
- [[agentic-engineering]] — agent即开发者是Agentic Engineering的隐含前提
- [[addyosmani-agent-skills]] — 互补：纪律vs身体，合在一起才是完整的agent=developer
- [[loop-scheduling]] — Boris的几百个Loop是"agent即开发者"的极端实践
- [[scope-discipline]] — 范围纪律是agent作为开发者必须遵守的第一条规则
- [[anti-rationalization]] — 反合理化是agent作为初级开发者最需要的纪律约束
- [[abstraction-ladder]] — agent-as-developer这个命题在不同抽象层级上都有站得住的论点
