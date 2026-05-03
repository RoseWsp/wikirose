---
type: 实践手册
date: 2026-05-03
author: 易哈佛医疗 ehafo.com
url: https://vorojar.github.io/ai-native-hiring-guide/
raw: raw/clips/AI-Native 工程师 招聘面试官手册.md
---

# AI-Native 工程师招聘面试官手册

**TL;DR** AI驱动开发团队的招聘只剩两种角色：Builder（产品直觉+驱动AI+基本设计感）和Reviewer（极强系统思维+极快评审速度）。传统"只写代码"的执行型程序员没有位置。60分钟面试覆盖7个模块，AI驾驶能力占25%权重，6项一票否决项直接淘汰。

## 核心流程变了什么

团队的核心开发流程：提交Issues → Claude Code审核确认 → 自动建分支/askuser补充 → 人类确认方案 → Claude Code写代码 → PR由Claude Code Review → 人工最终审查合并。

这意味着：
- **PRD没死，但顺序变了**：先出原型，再配文档说明意图
- **前后端分工淡化**：通才比三人团队还快
- **沟通是最大瓶颈**：Issues写得好不好直接决定AI能走多远
- **人类价值转移**：从"写代码"转为"提出正确问题"和"做好Review"
- **中间地带消失**：传统"只写代码"的执行型程序员没有位置

## Builder vs Reviewer

**Builder型**：产品直觉 + 驱动AI + 基本设计感。写高质量Issues，快速出原型，跨角色作战，从用户视角关注业务价值，不需要授权就能推动事情发生。

**Reviewer型**：极强系统思维 + 极快评审速度。快速识别AI代码风险与缺陷，给出AI能直接执行的修改指令，把握整体架构方向，高压下快速做取舍决策，从单次Review上升到流程优化。

**双栖候选人**：如果破冰阶段无法判断，走双栖路径——通用模块正常考，专项模块从Builder和Reviewer各抽一道核心题。

## 60分钟面试流程

| 时间 | 模块 | 说明 |
|------|------|------|
| 00-05min | 破冰&定型 | 判断Builder/Reviewer/双栖倾向 |
| 05-20min | 通用A+B | Issues写作质量 + 方案Review能力 |
| 20-30min | 通用G | AI驾驶实操（机甲战士的基本功） |
| 30-45min | 专项模块 | Builder: 产品直觉+原型实操 / Reviewer: PR Review+系统决策 |
| 45-55min | 开放讨论 | 最能暴露思维层次的环节 |
| 55-60min | 当场评分 | 30分钟内提交结论 |

## 评分体系

每人考5个模块（3通用+2专项），每模块10分，总分50分。35分及以上（≥70%）且无否决项，录用；30-34分备选；低于30分淘汰。

AI驾驶能力在Builder和Reviewer两个路径中都占25%最高权重。

## 一票否决项

1. 不能接受AI比自己写得好
2. Issues写得像工单，没有上下文
3. Review时只说"感觉不对"，说不出具体问题
4. 只关注技术实现，从不问"为什么要做这个"
5. 沟通需要多轮才能说清一件事
6. 面试结束时没有提出任何有质量的问题

## 与wiki的关联

- Builder-Reviewer模型是[[architect-operator-model]]在招聘层面的映射——架构师对应Reviewer的核心能力（批判AI、守住防线），操作员对应Builder的执行力（驱动AI完成工作）
- "中间地带消失"是[[role-convergence]]的必然结果——当角色融合，要么成为全能Builder，要么成为极致Reviewer，中间的纯执行者没有位置
- AI驾驶能力是[[agentic-engineering]]的个人技能维度——不只是会用工具，而是能驾驭Agent作为协作搭档
- Issue写作质量是[[harness-engineering]]在沟通层面的体现——给AI提供清晰上下文就是搭建认知脚手架
