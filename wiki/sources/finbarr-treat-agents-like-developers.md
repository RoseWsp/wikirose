# Finbarr Taylor：把你的Coding Agent当开发者对待

---
type: source
date: 2026-05-05
author: Finbarr Taylor
url: https://finbarr.site/2026/05/05/treat-your-coding-agents-like-developers.html
raw: raw/blog/Treat Your Coding Agents Like Developers.md
---

![两个agent在同一个分支上冲突](https://finbarr.site/assets/images/posts/duelling-agents-branch-commit.png)

## TL;DR

让多个coding agent并行工作的关键不是让agent更聪明，而是给它们和人类开发者一样的基础设施——独立的工作空间、独立的运行时、独立的分支。**Fork的单位是开发者，不是分支。**

## 核心论点

### 单agent工作流不扩展

两个agent改同一个checkout是"fork fight in a phone booth"。三个东西会依次崩塌：

1. **Git先崩** — 两个agent改同checkout，重新发明了分支和代码评审
2. **文件系统第二崩** — node_modules、.env、SQLite、lockfiles、build artifacts全不在git status里，但全互相踩
3. **Docker Compose第三崩（最惨）** — 每个agent要同样的端口、同样的容器名、同样的网络，互相杀Postgres容器

### Worktree是"技术正确但最危险"的答案

Worktree共享.git但不共享node_modules、.env、build artifacts、SQLite文件、运行中的Postgres容器。每个新worktree是干净checkout，需要手动重装一切。**Git被要求建模"另一个开发者的机器"，但它只知道如何建模"另一个分支"。**

> 如果我雇了Alice，我不会说"Alice，请作为我当前checkout的Git worktree操作"。我会说"Alice，clone repo，装依赖，跑app，做完push branch。"

### 全量拷贝胜过精巧方案

`yolobox fork --name alice codex` 创建整个项目文件夹的完整拷贝——不是干净checkout，不是过滤视图，是全部。.git、.env、ignored files、node_modules、local caches、那个你不敢删的tmp/目录。全量拷贝三个胜出属性：

1. 保留项目运行所需的全部脏状态
2. 挂载到原始路径，path-dependent的东西全继续工作
3. 心智模型简单：每个fork = 另一个开发者的机器

### 运行时隔离

每个fork有独立的`COMPOSE_PROJECT_NAME`，Alice的Postgres volume不会杀Bob的。退出时自动`docker compose down --volumes`。硬编码端口、显式container_name、外部网络仍可能冲突，但它们变成例外而非默认。

![agent工作流演进](https://finbarr.site/assets/images/posts/agent-workflow-evolution.png)

### URL即身份

用本地反代（Traefik/Caddy）给每个fork分配友好URL：`https://alice.myapp.localhost`。用户端URL来自开发者名字，不是Compose哈希或随机端口。

### 关键发现

> "让我惊讶的是，多少摩擦是*协调*摩擦，不是能力摩擦。Agent已经够用了，缺的是让多个agent同时干活而不互相踩脚的无聊基础设施。"

## 与Addy Osmani的互补

本文解决agent的"身体"问题（环境隔离），[[addyosmani-agent-skills|Agent Skills]]解决"纪律"问题（流程约束）。合在一起：agent不仅需要一台电脑，还需要有人盯着走完SDLC。两者共同指向——**通向AI-native的路不是让agent更魔法，而是让它更不特殊。**

## 关联

- [[agent-isolation]] — 本文提炼的核心概念：并行需要隔离
- [[agent-as-developer]] — 本文的核心心智模型：Fork开发者不是分支
- [[harness-engineering]] — yolobox是脚手架工程在运行时隔离层的具体实现
- [[agent-matrix]] — 多agent并行是Agent矩阵的前提条件
- [[agentic-engineering]] — 隔离是Agentic Engineering在基础设施层的基础
- [[addyosmani-agent-skills]] — 互补篇：纪律vs身体
- [[loop-scheduling]] — Boris的几百个Loop需要同样的隔离基础设施
