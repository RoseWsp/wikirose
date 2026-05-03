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

## 实现前提

Agent 矩阵要成真，需要解决几个问题：

- **[[jagged-intelligence]]** — 单任务成功率受锯齿状智能影响，Agent 矩阵会放大这些不均匀性
- **上下文管理** — 50 个 Agent 同时运行时的 token 成本和上下文共享
- **编排层** — 谁来决定哪个 Agent 做什么？这本身可能需要一个 meta-agent

Cat Wu 确认 token 成本在涨：每次模型升级后人们把更多任务交给 AI，单个工程师的 token 成本持续上升，但仍远低于薪资。([[cat-wu-ai-pm-role]])

## Cowork 的定位

Cat Wu 对 Claude 产品矩阵的分类暗示了 Agent 矩阵的入口：Cowork 处理非代码输出（Slack、slide deck、文档），连接所有数据源（Calendar、Gmail、Drive）后才能给出高质量输出。数据源接入是 Agent 矩阵的基础设施。([[cat-wu-ai-pm-role]])
