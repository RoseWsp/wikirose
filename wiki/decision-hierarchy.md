---
name: decision-hierarchy
description: 决策层级：目标→代码→CLI→Prompt→Agent，不确定性逐层递增，能在下层解决的绝不上推
metadata:
  type: concept
  foundation: [bounded-rationality]
---

# 决策层级

**TL;DR** 目标→代码→CLI→Prompt→Agent。每往上一层，不确定性增加一个量级，成本也增加一个量级。能在下层解决的，绝不上推。

## 五层模型

| 层级 | 适用场景 | 示例 | 不确定性 |
|------|---------|------|---------|
| 目标层 | 想清楚到底要解决什么 | 想清楚后发现不需要写代码 | 最低 |
| 代码层 | 确定性逻辑 | if/else、正则、模板引擎 | 低 |
| CLI层 | 组合现有工具 | `grep + jq + curl`串流程 | 中低 |
| Prompt层 | 需要语义理解和判断 | 需求翻译、文案生成 | 中高 |
| Agent层 | 多步推理、动态决策、循环执行 | 自动修bug、端到端流程 | 最高 |

## 核心原则

**80%的"AI需求"根本不需要AI。** 自动拉代码跑测试？Bash。定时检查服务健康？`cron + curl`。JSON日志格式化成报表？`jq + awk`。文件变更触发构建？`inotifywait + shell`。10行脚本就搞定，不需要任何模型。

市面上多少项目，一个`cron + curl`就能搞定的定时数据采集，非要套一层LangChain，加个Agent循环，搞个tool calling，最后效果还不如写死的脚本稳定（[[zhiyuanfu-ai-agent-exploration]]）。

## 这不是反AI，是尊重工程

拿到需求时从表格最底行往上看——先问"10行Bash能搞定吗？"，再问"一次LLM调用够吗？"，最后才考虑Agent。这个习惯帮你省掉80%的过度工程。

## 与wiki其他概念的关系

- [[bounded-rationality]] — 决策层级是有限理性在工程实践中的分层策略：不确定性越高，控制成本越高，越应该避免
- [[harness-engineering]] — 脚手架工程的核心洞察之一：把Agent限制在真正需要它的层级，其余用确定性方案
- [[scope-discipline]] — 层级边界就是范围纪律的工程化：不该用Agent的地方用了，就是范围蔓延
- [[vibe-coding]] — Vibe Coding的常见错误是默认跳到Agent层，跳过代码/CLI/Prompt三层的确定性方案
- [[clarity-before-automation]] — 目标层在最底层：先想清楚要不要做，再想怎么做
- [[ai-first-prerequisites]] — 五大前提中自动化测试/CI/CD属于代码层和CLI层，不需要AI
- [[context-discipline]] — "模型只做判断型任务"是决策层级规则5的直接表达：分类、草稿、总结、抽取适合模型，路由、重试、状态码处理让代码来。代码能回答的问题，别问模型
