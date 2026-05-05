---
type: article
date: 2026-03-09
author: Hugo Venturini
url: https://skiplabs.io/blog/codegen_as_compiler
raw: raw/blog/Treat Agent Output Like Compiler Output.md
---

# Treat Agent Output Like Compiler Output

**TL;DR** — 无人审查编译器输出的汇编代码，因为有类型系统、测试、监控让审查变得不必要。Agent生成的代码也应该如此——问题不是"要不要信任Agent输出"，而是"我们有没有建好让信任变得合理的设施"。

## 为什么Lights-out让人害怕

Philip Su提出"灭灯代码库"（无人值守的AI代码生成），Michael Novati一天合入417个PR。Volumetric impossible——代码审查在量上已不可行。但Venturini指出：**量不是问题，量暴露了问题**。真正的问题是，我们仍把Agent输出当"初级开发者输出"——需要人眼过一遍才算数。

## 编译器类比的核心洞察

没有人审查编译后的二进制。不是因为盲目信任，而是构建了一整套让审查变得不必要的装置：

- **上游**：类型系统、linter、形式化规约——约束输出能做什么
- **中游**：测试套件——验证可观测行为
- **下游**：灰度发布、特性开关、可观测性——出问题快速回滚

我们信任的是**流程**，不是**制品**。

## Agent还缺什么

对Agent而言，这套装置几乎不存在：

- **上游**：提示词和脚手架是原始的，没有健壮的形式化规约让Agent可验证地执行
- **验证层**：Agent不具确定性，同源可能产生不同输出。用于捕获人类错误的测试套件，对50倍速率生产"看起来对但微妙错误"代码的Agent来说，需要大幅加强
- **下游**：生产监控和回滚文化已经成熟，但尚未习惯性地应用于Agent生成的变更

## 关键论点

- 抵抗灭灯代码库的工程师，如果穿越回编译器时代，可能也会反对不审查链接器输出——不是理性判断，是对信任迁移位置的不熟悉
- 硬件芯片公司已经用验收测试替代人工审查来验证黑盒组件——但芯片验证是一个有工具、有形式化方法、有专职团队的**学科**
- 可怕的不是灭灯代码库，是有多少团队没把"替代代码审查的东西"当成严肃工程来做

## What To Build

1. 形式化规约层——Agent执行的约束不是提示词，而是可验证的规格
2. 足够强大的测试基础设施——替代代码审查提供的理解力
3. AI检查AI流水线——一级CI基础设施，不是外挂实验
4. 足够好的生产仪表——坏Agent行为被快速捕获和更快回滚

## 关联

- 编译器类比映射到[[agent-output-verification]]：Agent输出的验证体系设计
- 上游规约与[[harness-engineering]]脚手架工程深度呼应——为Agent构建约束环境
- AI检查AI与[[self-healing-pipeline]]自愈流水线共享同一闭环逻辑
- 形式化规约与[[agent-native-tooling]]中"精确胜过可读"的理念一致
- 与[[agentic-engineering]]互补：Venturini从验证体系角度，Karpathy从工程纪律角度

> 来源：[[venturini-agent-output-compiler]] | 续篇：[[venturini-code-never-for-machines]]
