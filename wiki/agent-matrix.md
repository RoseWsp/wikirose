# Agent 矩阵

**从单任务成功到多任务并行再到同时运行数十上百个 Agent——AI 产品的进化路线图。**

## What it means

Cat Wu 用 "building blocks" 描述长期路线。核心构建单元是**单任务成功率**：给一个清晰的 prompt，模型能不能持续产出可接受的输出？([[cat-wu-ai-pm-role]])

随模型变强，演进路径是：

```
单任务成功 → 多任务并行（2025年底 multi-coding）→ 同时跑 50-100 个 Claude
```

**这条路线从单兵作战走向 Agent 矩阵。** ([[cat-wu-ai-pm-role]])

## The argument

这不是线性增长，是阶段跃迁。每个阶段依赖前一个阶段的成熟：

1. **单任务** — 核心是可靠性，一个 prompt 能稳定产出可接受结果
2. **多任务** — 核心是协调，多个 Agent 不冲突、不重复、共享上下文
3. **Agent 矩阵** — 核心是编排，数十上百个 Agent 如何分工、优先级排序、异常处理

这与[[action-based-ai]]的范式转移一致：从"人操作工具"到"Agent 代替人操作工具"再到"Agent 矩阵自主运行"。

Hassabis对Agent矩阵的投入产出比提出了质疑："很多人启动几十个智能体跑40个小时，但我不确定产出能匹配这种级别的投入。"他的判断是Agent"刚刚开始，但还在实验阶段"，在"完整任务"上还不够好。缺乏[[continual-learning]]是Agent无法做到"交付后不管"（fire and forget）的根本原因。不过他也注意到，最近两三个月人们开始找到Agent真正有价值的使用场景，不再是"玩具展示"而是真正增加效率的工具。([[hassabis-agi-agents-science]])

## 实现前提

Agent 矩阵要成真，需要解决几个问题：

- **[[jagged-intelligence]]** — 单任务成功率受锯齿状智能影响，Agent 矩阵会放大这些不均匀性
- **[[sensory-gap|感知缺失]]** — 每个Agent都活在"永恒当下"，没有时间感等基本感知维度。当Agent矩阵同时获得新感知维度时，[[compulsive-capability-use|强迫性使用]]会在矩阵中放大——50个Agent同时过度使用同一个新能力，后果远比单个Agent失控严重 ([[claude-discovers-clock]])
- **上下文管理** — 50 个 Agent 同时运行时的 token 成本和上下文共享
- **编排层** — 谁来决定哪个 Agent 做什么？这本身可能需要一个 meta-agent
- **[[agent-isolation|隔离基础设施]]** — Finbarr Taylor指出Agent矩阵从"单任务"到"多任务并行"的跃迁，隔离是跳不过的门槛：没有隔离你没有多个agent，你只有一个很困惑的agent带着四个终端。每个agent需要独立的文件系统、Compose命名空间和URL ([[finbarr-treat-agents-like-developers]])

Cat Wu 确认 token 成本在涨：每次模型升级后人们把更多任务交给 AI，单个工程师的 token 成本持续上升，但仍远低于薪资。([[cat-wu-ai-pm-role]]) [[jevons-paradox-inference|推理的杰文斯悖论]]也指出：Agent矩阵的规模扩展不会因为推理降价而消失上限。

## Cowork 的定位

Agent矩阵的组织形态是[[opc-one-person-company|一人公司]]——一个人管理100个agent，科斯定理在AI时代的必然推论。管理100个agent的成本远低于管理100个人，即使需要扩大规模也可由AI辅助管理其他AI，仅在带宽超限时才引入人类。Agent矩阵是OPC的技术基础设施，OPC是Agent矩阵的组织归宿。([[lijigang-experience-incompressible]])

## Agent矩阵的隔离前提

Finbarr Taylor（yolobox作者）的实践揭示了一个被忽视的前提：Agent矩阵的每个节点都需要[[agent-isolation|独立的运行环境]]。两个agent改同一个checkout是"fork fight in a phone booth"——Git冲突、文件系统踩脚、Docker Compose互相杀容器。解决方案不是让agent更聪明，而是给每个agent自己的文件夹拷贝、Compose命名空间和.localhost URL。核心心智模型是[[agent-as-developer|Agent即开发者]]——fork的单位是开发者，不是分支。([[finbarr-treat-agents-like-developers]])

## Cowork 的定位

Cat Wu 对 Claude 产品矩阵的分类暗示了 Agent 矩阵的入口：Cowork 处理非代码输出（Slack、slide deck、文档），连接所有数据源（Calendar、Gmail、Drive）后才能给出高质量输出。数据源接入是 Agent 矩阵的基础设施。([[cat-wu-ai-pm-role]])

Boris Cherny提供了Agent矩阵的最新实践数据：手机上同时运行5-10个会话，每会话下挂一批Agent，白天大概几百个在跑，每天晚上几千个做更深层工作。他每天通常写几十个PR，最多一天150个。用[[loop-scheduling|Loop]]管理这些Agent——用cron调度重复任务，如自动看护PR、维持CI健康、每30分钟抓Twitter反馈。Anthropic内部更进一步：Agent之间通过Slack互相通信协商解决问题，公司里没有任何手写代码，所有SQL由模型生成。([[boris-chenyi-sequoia-ai-ascent]])

## 终极形态：Agent矩阵不再需要人类

Jack Clark指出AI管理AI已在产品层面实现（Claude Code、子智能体架构），[[automated-ai-rd|自动化AI研发]]意味着矩阵中不再需要人类操作员——[[architect-operator-model]]中的"操作员"被AI自己取代，"架构师"也岌岌可危。递归自改进是Agent矩阵的极限形态：模型训练下一代模型，Agent构建下一批Agent。([[jack-clark-ai-self-construction]])

## 人类监督规模化

Anthropic 2026趋势报告量化了Agent矩阵中人类监督的瓶颈：60%工作用AI但仅0-20%可完全委托。Agent矩阵的扩张不只是技术问题——人如何在关键节点介入、如何在不降低信任的情况下缩小监督面，是矩阵规模化的真正约束。Anthropic给出的方向是"Agent学会请求帮助"——不是让人无处不在，而是让Agent知道何时该找人来判断。([[anthropic-coding-trends-2026]])
