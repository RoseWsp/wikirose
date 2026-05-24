# 上下文纪律 (Context Discipline)

**TL;DR** Claude犯的错，90%是因为上下文没给够。没有CLAUDE.md时错误率41%，4条基础规则降到11%，12条规则降到3%。上下文纪律不是让模型变聪明，是阻止它"太聪明"。

## 核心论点

Karpathy这句话的分量不在"模型够好"，而在"你的上下文工程够差"。数据很硬：41% → 11% → 3%，纯靠约束规则把错误率压下去。([[karpathy-claude-context-rules]])

12条规则本质上在做同一件事：**减少Agent的自由度**。外科手术式修改收缩行动范围，Token预算收缩认知范围，失败大声喊收缩信息隐藏的空间。LLM的"聪明"恰恰是危险源——它太擅长给跳过纪律找理由了。([[anti-rationalization]])

## CLAUDE.md = 跨会话组织记忆

把CLAUDE.md当作跨会话的组织记忆来维护。改进要基于eval的结果，别凭感觉。一个仓库，一个规则文件，没有例外。([[karpathy-claude-context-rules]])

这是[[harness-engineering]]最轻量的实现——不用三Agent架构，不用Feature List JSON，一个规则文件就够了。但也最脆弱——纯靠规则文本约束，没有代码级别的强制执行。

## 12条规则与现有概念映射

| 规则 | 核心动作 | 对应概念 |
|------|---------|---------|
| 1. 写代码前先把假设说清楚 | 收缩认知自由度 | [[clarity-before-automation]] |
| 2. 简单优先，最少代码 | 收缩行动自由度 | [[scope-discipline]] |
| 3. 外科手术式修改 | 收缩修改范围 | [[scope-discipline]] |
| 4. 先定义成功标准 | 收缩终止条件 | [[sdd]] |
| 5. 模型只做判断型任务 | 收缩适用范围 | [[decision-hierarchy]] |
| 6. Token预算是硬约束 | 收缩认知窗口 | [[bounded-rationality]] |
| 7. 两种模式选一种别折中 | 消除歧义 | [[anti-rationalization]] |
| 8. 先读再写 | 收缩信息自由度 | [[scope-discipline]] |
| 9. 测试验证意图不验证行为 | 收缩验证自由度 | [[agent-output-verification]] |
| 10. 每步checkpoint | 收缩错误传播 | [[agent-observability]] |
| 11. 匹配代码库约定 | 收缩风格自由度 | [[anti-rationalization]] |
| 12. 失败要大声喊 | 收缩信息隐藏 | [[agent-observability]] |

## 两个被低估的规则

**第10条（Checkpoint）**：Agent会在坏状态上继续跑，而且跑得很自信。错误像滚雪球在后继步骤中被当作前提。这与[[agent-observability|可观测性]]的"步骤可见性"是同一个问题——没有checkpoint，错误会像滚雪球一样在后继步骤中被当作前提。这和[[harness-engineering]]里的Premature Victory Declaration是同源的：Agent不知道自己坏了，因为没人检查。

**第7条（别折中）**：两种模式选一种别折中——Claude把两种混在一起写，错误被吞两次。歧义是Agent的毒药。人对歧义有体感，能直觉判断"这里应该用哪种"，但Agent会在歧义里随机游走。这本质上是[[incompressible-judgment|判断不可压缩]]的工程后果——人类开发者对"该用哪种模式"有体感但说不清，CLAUDE.md必须替他说清。

## 反论："90%是上下文"可能被过度解读

有些错误确实是模型能力边界——长程推理中遗忘、对隐含约束的钝感。把所有锅都甩给上下文工程，容易让人误以为只要CLAUDE.md写得够长就能解决一切。第6条自己就说了：调试到第40条消息时Claude会忘掉第5条否掉的方案——这是上下文窗口的物理限制，不是你规则写得不够。([[bounded-rationality]])

"90%是上下文"的正确解读不是"所有问题都能靠加上下文解决"，而是"在你砸更多算力之前，先把上下文工程做到位"。

## 关联

- [[harness-engineering]] — 上下文纪律是脚手架工程的操作手册版：脚手架搭系统，上下文纪律管输入
- [[clarity-before-automation]] — 先清晰是原则，上下文纪律是实践
- [[scope-discipline]] — 范围纪律管行动边界，上下文纪律管认知边界
- [[anti-rationalization]] — 12条规则中的7、9、11、12全是反合理化的具体实现
- [[decision-hierarchy]] — 规则5的直接来源：判断型任务给Agent，确定性任务给代码
- [[agent-observability]] — Checkpoint和失败大声喊是可观测性的最低实现
- [[bounded-rationality]] — Token预算是有限理性在上下文窗口中的精确投影
- [[sdd]] — 先规格再开发（规则4）是SDD的简化版
- [[agent-output-verification]] — 测试验证意图（规则9）是输出验证的具体操作
- [[incompressible-judgment]] — 12条规则是资深工程师的判断编码，但编码后还是不如体感灵活——判断不可压缩的工程验证

来源：[[karpathy-claude-context-rules]]
