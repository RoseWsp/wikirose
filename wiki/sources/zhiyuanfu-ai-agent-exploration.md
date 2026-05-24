---
type: article
date: 2026-05-07
author: zhiyuanfu（腾讯）
url: https://mp.weixin.qq.com/s/r__2l_u6oXwzWHyD3wu_ZQ
raw: raw/blog/十年老技术开发的 AI Agent 探索之路.md
---

10年经验的前端开发者从手动管4-6个AI终端到造出24h无人值守Agent系统的完整手记。不是理论推演，是被实践逼出来的认知转折。

## 核心论点

1. **人是瓶颈**——但解决方式不是让AI替代人，而是让系统不再依赖人的实时在场
2. **80%的AI需求不需要AI**——决策层级：目标→代码→CLI→Prompt→Agent，能在下层解决的绝不上推
3. **Vibe Coding翻车 → SDD是解药**——先易后难 vs 先难后易，"大道如夷，而民好径"
4. **脚手架>模型**——模型升级成本+300%效果+20%，脚手架升级成本+50%效果+200%
5. **从Task-Driven到Goal-Driven**——Task-Driven解决执行问题，Goal-Driven解决迭代问题

## 关键实践

- **24h打工人系统**：文件+轮询调度层，CLI Agent（codex/gemini-cli/claude）为执行单元，SDD流程驱动
- **SDD（Spec-Driven Development）**：spec.md→plan.md→tasks.md逐层细化，constitution.md编码架构约束
- **Agent自举**：通过自己的反馈系统提交bug，系统自动走SDD流程修复——前提是SDD+constitution.md+设计文档
- **智能并发**：组间并发（前端/后端不同目录），组内串行（同项目可能改同一文件），失败隔离
- **可观测性6维度**：目标、步骤、工具、失败原因、恢复策略、成本

## 协议层判断

Agent开发从"框架之争"转向"协议+runtime+control plane之争"。MCP标准化工具接入，A2A解决多Agent协作，Responses API收敛runtime。未来做Agent越来越像搭操作系统。

## 金句

> 垃圾的思考乘以强大的模型，等于精美的垃圾。
> 捷径的尽头是弯路，大道的尽头是自由。
> 增强自我，而非取代自我。
