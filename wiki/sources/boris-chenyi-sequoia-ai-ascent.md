---
type: source
date: 2026-05-05
author: Boris Cherny / 龙玥
url: https://wallstreetcn.com/articles/3771572
raw: raw/blog/ClaudeCode之父："全员编程"时代，企业真正领先在于"组织流程的代差".md
---

# Boris Cherny × Sequoia：编程已解决，组织流程才是真正鸿沟

## TL;DR

Claude Code创造者Boris Cherny在Sequoia AI Ascent 2026上宣布：他2026年没写过一行代码，每天用手机调度数百Agent，一天最多150个PR。真正的竞争优势不是技术——同样的模型对所有人开放——而是[[org-process-gap|组织流程的代差]]。

## 核心论点

### 编程问题已解决

Boris自2025年10-11月起100%代码由模型完成。Claude Code代码库本身也很简单——TypeScript + React，选这两个是因为训练分布中占比高。真正的转折点是Opus 4发布，此后每次模型更新都带来指数级增长。

### [[loop-scheduling|Loop是未来]]

Boris最依赖的工作方式是Loop——用cron调度重复任务，每分钟、每5分钟、每天运行。他运行几十个Loop：一个看护PR（自动修复CI、rebase），一个维持CI健康（修复flaky test），一个每30分钟抓Twitter反馈聚类。"即使你关上笔记本，它也会继续跑。"

### [[org-process-gap|组织流程代差]]

被问及Anthropic领先多少个月，Boris的回答出人意料：模型层面没有差距，dogfooding要求他们用和外部一样的模型。**真正的差距在组织流程**——Anthropic内部所有事情都用Claude，Claude之间通过Slack互相通信，公司里没有任何手写代码，所有SQL由模型生成。

### 全员编程

Claude Code团队本身就是实验场：工程经理、产品经理、设计师、数据科学家、财务人员、用户研究员——每个人都在写代码。Boris预判未来的通才是跨学科的：既懂产品工程也懂设计，或兼顾数据科学与工程。

### 印刷机类比

Boris用15世纪印刷机类比当下：印刷机前欧洲约10%识字，之后50年出版物超此前千年总和，书籍成本降100倍，几百年后识字率升至70%。**软件民主化会远快于此**——写会计软件，最合适的人是优秀会计师而非工程师，因为懂领域才是难点。

### 护城河消长

AI削弱两种传统护城河：**转换成本**（模型帮用户轻松迁移）和**流程壁垒**（Claude 4.7能自主迭代优化复杂流程）。网络效应、规模经济、独占资源等护城河不受影响。Boris预言未来十年颠覆性初创公司数量增加10倍——小公司能打造大公司同等量级产品，且没有组织转型阻力。

### Claude Code的未来

Boris预言Claude Code一年后可能只剩100行代码——随着模型自主行动能力增强，prompt注入保护、命令校验、权限模式等安全机制都会变得不重要，因为模型会自己做正确的事。产品层的"脚手架"重要性在下降，重心转向Loop、并行Agent、computer use。

![Boris Cherny at Sequoia AI Ascent](https://wpimg-wscn.awtmt.com/d2b5cbc7-3d9a-4698-9c5b-fb9299b974c3.png)

## 与wiki的连接

- [[org-process-gap]] — 本文核心概念：组织流程代差
- [[loop-scheduling]] — Loop循环调度：Boris最依赖的工作方式
- [[product-overhang]] — 产品过剩：Claude Code诞生的原因
- [[role-convergence]] — 全员编程是角色融合的极端形态
- [[agent-matrix]] — 数百并行Agent的管理方式
- [[software-no-moat]] — 转换成本和流程壁垒被AI削弱
- [[harness-engineering]] — 脚手架重要性随模型增强而下降
- [[architect-operator-model]] — Boris的"手机调度者"角色
- [[product-taste]] — YC哲学："做出人们喜爱的东西"
- [[dogfooding-as-method]] — Anthropic用同样的模型做dogfooding
- [[clarity-before-automation]] — 组织流程清晰化是AI赋能前提
