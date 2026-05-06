---
type: article
date: 2026-05-03
author: Addy Osmani
url: addyosmani.com/blog/agent-skills/
raw: raw/blog/Agent Skill.md
---

# Agent Skills

**TL;DR** AI编码智能体默认跳过高级工程师做的"隐形工作"——规格、测试、评审、范围控制、验证证据。Addy Osmani用20个skill把这些工程纪律编码成agent无法自我说服绕过的流程，核心武器是反合理化表格和"流程优先于散文"。

## 这篇文章说了什么

Addy Osmani（Google Cloud AI director）指出一个根本问题：任何AI编码智能体的默认行为都是走向"完成"的最短路径。它不会问你要不要规格说明，不会先写测试，不会考虑这个改动是否跨越信任边界。这和初级工程师跳过步骤的原因一样——这些步骤是不可见的，奖励信号指向"任务完成"而非"任务完成且设计文档也存在"。

Agent Skills是他把高级工程师的脚手架重新加回去的尝试。20个skill围绕6个SDLC阶段组织（Define→Plan→Build→Verify→Review→Ship），上面有7个slash commands。关键是这些skill不是参考文档，而是带检查点和退出标准的工作流。

## 五个承重原则

1. **流程优先于散文**——工作流可以被智能体执行，文章不行。2000字测试最佳实践放进去，模型读完跳过；"先写失败测试→运行确认失败→写最小代码通过→确认通过→重构"这种流程，模型有东西可执行，你有东西可验证。

2. **反合理化表格**——每个skill列出agent可能用来跳过工作流的常见借口，配上预先写好的反驳。LLM极其擅长合理化，会生成听起来无懈可击的文字解释为什么这次不需要规格。反合理化表格是对agent还没说出口的谎言提前写好的反驳。

3. **验证不可协商**——每个skill以具体证据结束：测试通过、构建输出干净、运行时trace展示预期行为、评审者签字确认。"看起来对"永远不够。

4. **渐进式披露**——不在会话开始时加载全部20个skill，根据阶段激活。meta-skill `using-agent-skills` 充当路由器。每个加载进上下文的token都会在某个地方降低性能。

5. **范围纪律**——只碰你被要求碰的。不要重构相邻系统，不要删除你没完全理解的代码，不要看到TODO就重写整个文件。范围纪律是agent PR能否被合并的最大决定因素。

## Google基因

Skills充满了来自《Software Engineering at Google》和Google公开工程文化的实践：Hyrum's Law（api-and-interface-design）、测试金字塔和Beyoncé Rule（test-driven-development）、~100行PR大小（code-review-and-quality）、Chesterton's Fence（code-simplification）、trunk-based development（git-workflow）、Shift Left和feature flags（ci-cd）、code-as-liability（deprecation）。

这些不是新想法。重点是，它们默认不存在于智能体里。模型训练数据里读过"Hyrum's Law"，但不会在凌晨3点为你设计API时自动应用它。

## 五条不可协商原则

1. 构建之前先揭示假设——沉默持有的错误假设是最常见的失败模式
2. 需求冲突时停下来并提问——不要猜
3. 有必要时要反驳——智能体不是只会说"是"的机器
4. 偏好朴素、明显的解决方案——聪明技巧很昂贵
5. 只碰你被要求碰的——不要扩大范围

## 三个使用模式

1. **通过marketplace安装**（Claude Code `/plugin`）
2. **把markdown放进你选择的工具**（Cursor rules、Gemini CLI等）
3. **把它们当成规格来读**——即使不安装，反合理化表格、五条原则、渐进式披露这些模式也值得偷走

## 与wiki的深层连接

- [[harness-engineering]]——Agent Skills是脚手架工程在skill层面的具体化：不是写规则，而是编码可执行的工作流
- [[agent-immune-system]]——反合理化表格和免疫系统是同一思路的两个应用：认知激活，不是规则叠加。安全场景激活安全知识，工程场景激活工程纪律
- [[system-zero]]——LLM的合理化是系统0的工程版：它不只替你做决策，还替跳过决策找理由，而且理由听起来完全正确
- [[agentic-engineering]]——Agent Skills给出了Agentic Engineering"怎么做到"的答案：20个skill编码了高级工程师流程
- [[agent-output-verification]]——"验证不可协商"原则与验证体系设计完全同构：证据是退出标准，"看起来对"永远不够
- [[bounded-rationality]]——范围纪律是有限理性在行动层面的应用：知道自己不该碰什么，和不去做自己不该做的事
- [[ai-first-prerequisites]]——Agent Skills的skill集可以视为五大前提在agent工作流层面的展开
- [[self-healing-pipeline]]——Agent Skills的验证退出标准与自愈流水线的检测-验证闭环逻辑一致
