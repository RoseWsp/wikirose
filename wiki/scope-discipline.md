# 范围纪律

**TL;DR** 只碰你被要求碰的。不要重构相邻系统，不要删除你没完全理解的代码，不要看到TODO就重写整个文件。范围纪律是agent PR能否被合并的最大决定因素。

## 这是什么

Addy Osmani在Agent Skills中把范围纪律编码为五条不可协商原则之一，也是meta-skill `using-agent-skills` 的核心约束。听起来显而易见——直到你看到一个agent为了修一个bug，决定现代化三个无关文件。

范围纪律直接映射到Google代码评审规范：评审者会因为一个PR做了不止一件事而阻止它合并。

## 为什么agent特别容易违反范围

agent没有"适可而止"的本能。它的奖励信号是"任务完成"，而"顺便把那个也修了"看起来像额外贡献，不是范围蔓延。加上LLM的合理化能力——它能给你一段完美解释为什么这次重构是必要的：

> "在修复这个bug的过程中，我注意到相邻模块的命名不一致，这可能导致后续维护困难，因此一并重构……"

这段话逻辑上无懈可击。但[[anti-rationalization|反合理化]]会告诉你：如果重构不是你被要求做的，先别动。开一个issue，让评审者决定。

## 与有限理性的对称

[[bounded-rationality|有限理性]]说的是"算不完就别算完美"——认知的边界。范围纪律说的是"没叫你碰就别碰"——行动的边界。两者合在一起才是完整的"AI自我约束"：

- 有限理性：知道自己不该知道什么（认知层面的约束）
- 范围纪律：不去做自己不该做的事（行动层面的约束）

一个是搜索的边界，一个是修改的边界。不划定搜索边界，agent会在无限空间里浪费算力；不划定修改边界，agent会在有限代码里制造混乱。

## Chesterton's Fence

范围纪律的一个推论：在理解一个东西为什么被放在那里之前，不要移除它。这是Google工程文化中的Chesterton's Fence原则，也是Agent Skills中`code-simplification` skill的核心约束。

agent看到一段"无用"代码时，默认行为是删除它。但那段代码可能是在处理一个你不知道的边界情况、一个被废弃但仍有用户依赖的API、一个看似冗余但实际是安全网的重试逻辑。删除前必须理解它为什么存在。

## 关联

- [[anti-rationalization]]——范围违反是最常见的合理化目标
- [[bounded-rationality]]——有限理性是认知的边界，范围纪律是行动的边界
- [[harness-engineering]]——脚手架划定agent的行动范围，范围纪律是脚手架的意志层
- [[agent-output-verification]]——验证体系检查agent是否超出范围
- [[agentic-engineering]]——范围纪律是Agentic Engineering最基本的一条
- [[self-healing-pipeline]]——自愈流水线的"每个工具只负责一个阶段"是范围纪律在系统层面的体现
- [[clarity-before-automation]]——你不清晰定义范围，agent就无法遵守范围纪律
- [[agent-isolation]]——隔离在物理层划定边界（不同agent不碰同一份代码），范围纪律在行动层划定边界（同一agent不碰未被要求的代码）——两者合在一起是完整的agent约束
- [[agent-as-developer]]——范围纪律是agent作为开发者必须遵守的第一条规则：人类开发者不擅自改别人的模块，agent也不应擅自改未被要求的文件
- [[anthropic-effective-harnesses]] — Anthropic的Feature List机制是范围纪律的结构化实现：JSON格式的功能清单标记"passes: false/true"，Agent只允许修改passes状态，禁止删除或修改测试项——"只碰你被要求碰的"从文本指令变为代码约束
- [[openai-harness-engineering]] — "The agent's knowledge boundary equals the repository's file boundary"——OpenAI的这条经验是范围纪律的边界定义：Agent只能看到仓库中的文件，Slack讨论和Google Docs对它不存在。范围纪律不仅约束Agent的行为，还约束Agent的感知边界
- [[contradiction-dialectics]]——范围纪律是"抓住主要矛盾"在行动层面的体现：只碰你被要求碰的=只处理当前的主要矛盾，不碰次要矛盾。当Agent同时面对"修bug"和"重构相邻模块"两个矛盾时，修bug是主要矛盾，重构是次要矛盾——范围纪律就是"捉住了主要矛盾，一切问题就迎刃而解"的Agent版

来源：[[addyosmani-agent-skills]]
