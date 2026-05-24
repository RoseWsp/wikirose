---
name: sdd
description: Spec-Driven Development：先规格再开发，把模糊想法逐步转成可执行单元并完整留痕
metadata:
  type: concept
  foundation: [practice-epistemology, clarity-before-automation]
---

# SDD（Spec-Driven Development）

**TL;DR** 先写规格再动手，不是官僚主义，是让AI的每一步都有据可查——留痕不是为了debug，是为了进化。

## 什么是SDD

SDD不是"先写文档再开发"的瀑布模型翻版。在Agent场景里，它的核心作用是：**把一件事从模糊想法逐步转成可执行单元，并且把这个过程完整留下来。**

每个需求走完留下三份文档（[[zhiyuanfu-ai-agent-exploration]]）：

- `spec.md` — 目标、验收标准（"分页有问题"→"切换页码后列表数据未刷新，原因是查询参数未传递page参数"）
- `plan.md` — 技术方案、涉及文件、实现步骤
- `tasks.md` — 任务清单，每步有输入、输出、完成标准

加上 `constitution.md` 编码架构约束（目录结构、模块边界、命名规则），AI在框架内工作而不是自由发挥。

## 为什么不能跳过

[[vibe-coding]]的真实时间线：Day 1-3很爽→Day 7打地鼠→Day 14被迫逐文件排查→Day 15一整天对齐比前两周加起来都累。**Vibe Coding是先易后难，SDD是先难后易。**

跳过spec的代价不是线性增长——前期省掉的设计时间，后期以10倍debug时间还回来。代码越写越多，AI上下文越来越混乱，每次修改都在给系统埋雷。

## SDD使Agent自举成为可能

Agent能自己修自己的bug，不是因为模型多聪明，而是因为SDD+constitution.md建立了三样东西（[[zhiyuanfu-ai-agent-exploration]]）：

1. **设计文档** — AI知道每个模块该做什么、不该做什么
2. **SDD流程** — spec→plan→tasks的标准路径，AI按同样方式处理所有需求
3. **constitution.md** — 架构约束文件，AI在框架内工作

没有这些基础设施，Agent"自己修自己"只是碰运气。有了这些，它才能在框架内工作，而不是自由发挥。

## 与wiki其他概念的关系

- [[harness-engineering]] — SDD是脚手架工程的核心方法论。脚手架搭外部护栏，SDD规定护栏内的标准路径
- [[anti-rationalization]] — SDD是对抗合理化的结构性武器：spec写好了，agent就没有"这次可以跳过"的借口
- [[scope-discipline]] — spec的"不做什么"和验收标准的"怎么算完成"是范围纪律的文档化
- [[workflow-over-prose]] — spec→plan→tasks是可执行流程，不是散文式需求描述
- [[clarity-before-automation]] — SDD是"先清晰"的制度化：在AI动手之前，人先把目标、边界、完成标准想清楚
- [[practice-epistemology]] — SDD的每一步留痕是"实践→认识→再实践"的文档化螺旋
- [[generator-evaluator-loop]] — spec是Evaluator的评判依据，没有spec，Evaluator就是空转
