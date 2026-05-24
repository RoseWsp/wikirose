---
type: blog
date: 2026-05-24
author: 匿名资深工程师（以Karpathy语录为引）
url:
raw: raw/blog/Andrej Karpathy 说过一句话：Claude 犯的错，90% 是因为上下文没给够，跟模型本身的能力没关系.md
---

# Karpathy语录引出的12条上下文纪律规则

核心论点：Claude犯的错，90%是因为上下文没给够，跟模型本身的能力没关系。

**量化数据**：没有CLAUDE.md时错误率41%，4条基础规则降到11%，12条规则降到3%。

12条规则：
1. 写代码前先把假设说清楚
2. 简单优先，最少代码
3. 外科手术式修改，只动必须动的地方
4. 先定义成功标准，再让它执行
5. 模型只用来做判断型任务
6. Token预算是硬约束（单任务4000，单会话30000）
7. 两种模式？选一种，别折中
8. 先读再写
9. 测试要验证意图，不只是验证行为
10. 每个重要步骤都要checkpoint
11. 匹配代码库约定
12. 失败要大声喊出来

**关键结论**：把CLAUDE.md当作跨会话的组织记忆来维护。改进要基于eval的结果，别凭感觉。重视checkpoint，别一味追求速度。冲突要明确暴露出来，别静默混合。纪律永远比框架重要。

**与wiki已有概念的映射**：这12条是[[harness-engineering]]的操作手册版，是[[clarity-before-automation]]、[[scope-discipline]]、[[anti-rationalization]]、[[decision-hierarchy]]、[[agent-observability]]的量化验证和具体实现。详见[[context-discipline]]。
