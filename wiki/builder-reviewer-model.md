# Builder-Reviewer 模型

**TL;DR** AI-Native团队只有两种角色：Builder（产品直觉+驱动AI+基本设计感）和Reviewer（极强系统思维+极快评审速度）。传统"只写代码"的执行型程序员没有位置，中间地带消失。

## What it means

AI驱动开发流程中，人类的核心价值从"写代码"转移到两个极点：**驱动AI完成工作**（Builder）和**守住最后防线**（Reviewer）。写代码本身不再是稀缺能力，知道该建什么、怎么建、建出来对不对才是 ([[ai-native-hiring-guide]])。

Builder不需要授权就能推动事情发生——从发现问题、写Issue、到出原型、推动落地，一个人驱动一条线。Reviewer在AI高速输出代码的情况下，快速、准确地识别问题，并给出可执行的修改指令。

## The argument

**中间地带为什么消失？** AI承担了大量执行工作后，"只写代码"的人的价值被AI直接替代。要么你比AI更会驾驭AI（Builder），要么你比AI更会判断AI的产出（Reviewer），两者都不是的，不录用 ([[ai-native-hiring-guide]])。

**与[[architect-operator-model]]的映射**：架构师对应Reviewer的核心能力——批判AI、守住防线、把握架构方向。操作员对应Builder的执行力——驱动AI完成工作、快速出原型。但两者有关键区别：架构师-操作员模型是组织层面的两极分化，Builder-Reviewer模型是招聘层面的筛选框架，前者描述"团队怎么运作"，后者描述"招什么样的人"。

**双栖路径**：不是所有人都能归入单一类型。破冰阶段无法判断时，走双栖路径——通用模块正常考，专项模块从Builder和Reviewer各抽一道核心题，最后根据得分分布决定方向 ([[ai-native-hiring-guide]])。

## 评分体系

每人考5个模块（3通用+2专项），每模块10分，总分50分。AI驾驶能力在两个路径中都占25%最高权重。录用线35分（70%），备选30-34分，低于30分淘汰。

| 模块 | Builder权重 | Reviewer权重 |
|------|------------|-------------|
| Issues写作质量 | 20% | 15% |
| 方案Review能力 | 10% | 20% |
| AI驾驶能力 | 25% | 25% |
| 产品直觉 | 25% | — |
| 原型驱动能力 | 20% | — |
| PR Review能力 | — | 20% |
| 系统思维&决策 | — | 20% |

## 关联

- [[architect-operator-model]]——组织层面的两极分化，Builder-Reviewer是招聘层面的映射
- [[role-convergence]]——角色融合的终点不是全栈通才，而是Builder和Reviewer两种极端
- [[agentic-engineering]]——Builder和Reviewer是Agentic Engineering在人才维度的具体化
- [[harness-engineering]]——Builder搭脚手架，Reviewer验证脚手架有效性
- [[ai-piloting]]——AI驾驶能力是Builder和Reviewer的共同基本功
- [[product-taste]]——Builder的核心直觉来源
- [[pm-as-gap-filler]]——PM在Builder-Reviewer模型中的位置：Builder可以覆盖PM职能
- [[ai-native-hiring-guide]]——源文件
- [[ai-readiness-gap]]——Builder-Reviewer模型是AI-ready团队的招聘形态，跨越准备度鸿沟的组织才能有效运作
- [[clarity-before-automation]]——Builder驱动AI的前提是组织已经"配得上"让AI帮忙：能清晰描述目标、工作流和决策机制 ([[companies-not-ready-for-ai]])
