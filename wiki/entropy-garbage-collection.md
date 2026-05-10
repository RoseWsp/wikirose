# 熵的垃圾回收 (Entropy Garbage Collection)

**TL;DR** Agent写代码时会复制已有Pattern（包括次优的），微小不一致逐步累积导致代码腐化。定期用后台Agent扫描偏差并自动修复，让技术债像垃圾回收一样被持续清理。

## 这意味着什么

OpenAI在百万行代码实践中发现 ([[openai-harness-engineering]])：当代码库完全由Agent生成时，Agent会模仿代码库中已有的Pattern——包括那些Suboptimal的Pattern。每次Agent生成代码，都可能引入少量风格不一致、冗余逻辑或次优实现。单次无关痛痒，累积起来却会让代码库逐渐腐化（Code Rot）。

这本质上是热力学第二定律在软件工程中的体现：**一个封闭系统的熵只能增加**。Agent代码库是一个偏向熵增的系统——如果不主动干预，代码质量只会随时间下降。

## 手动清理不可持续

OpenAI早期尝试每周五手动清理"AI残渣"，占团队20%的时间。但很快发现这不可持续——Agent的产出速度远超人类清理速度，积压只会越来越大。

## Golden Principles编码化

解法是将主观品味编码为可机械执行的规则：

1. **优先使用共享工具包而非手写辅助函数** — 将不变量集中管理
2. **结构化日志格式统一** — 确保可观测性工具可解析
3. **不在边界处猜测数据结构** — 验证边界或依赖类型化SDK

这些"Golden Principles"不是文档层面的建议，而是：
- 通过Custom Linter静态强制执行
- 写入CI门禁
- 由后台Agent定期扫描偏差

## 后台回收流程

定期运行一组后台Codex任务：(1) 扫描偏差和质量等级 (2) 发起针对性的重构Pull Request (3) 大多数可在1分钟内审查并自动合并。这类似于垃圾回收——不断以小额偿还技术债，比让债务积累再一次性痛苦解决要好得多。

核心收益：**人类的品味一旦被捕捉，就会持续应用于每一行代码**。也能每天发现并解决不良模式，而不是让它们在代码库中传播数天或数周。

## 关联

- [[harness-engineering]] — 熵的垃圾回收是脚手架工程的持续维护机制
- [[organizational-self-knowledge]] — Golden Principles就是组织自我认知在工程层的编码
- [[anti-rationalization]] — 两者都防AI走捷径：一个防跳过代码规范，一个防跳过工程纪律
- [[agent-output-verification]] — 为回收Agent提供判断标准
- [[agent-native-tooling]] — 两者都是"Agent时代的工程纪律"的一部分
- [[self-healing-pipeline]] — 熵回收Agent是自愈流水线在代码质量维度的实例
