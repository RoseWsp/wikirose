# Research Preview

**用"这是早期实验"的标签降低发布门槛，让团队一周甚至一天就能把功能推到用户手里。**

## What it means

传统软件发布需要承诺：功能稳定、永远支持、文档齐全。这个承诺本身就让团队不敢发——怕撤回丢面子，怕维护成本撑不住。Research preview 反过来：明确告诉用户"这只是个想法，可能不会永远支持"，把承诺降到最低，发布门槛随之降到最低。

Claude Code 几乎所有功能都先以 research preview 形式发布。一两周就能把东西推出去，而不是等打磨完美才上线。([[cat-wu-ai-pm-role]])

## The argument

Research preview 不是一个标签，是一套完整机制：

1. **降承诺** — 用户预期管理前置，"可能不支持"不是bug是feature
2. **收反馈** — 真实用户用真实场景告诉你方向对不对，比内部讨论高效得多
3. **快迭代** — 因为不承诺长期支持，改方向或砍掉都没有包袱

这套机制能运作，前提是团队有快速反应的发布流水线。Anthropic 有"evergreen launch room"：工程师觉得功能准备好了就发到频道，文档/营销/DevRel 第二天完成对外宣传。([[cat-wu-ai-pm-role]])

## Trade-offs

代价是**产品一致性**。多个 research preview 同时存在可能功能重叠，新用户不知道最佳路径。Anthropic 的做法是用重叠功能做市场实验，让用户选择赢家，再整合。([[cat-wu-ai-pm-role]])

这和[[minimal-product-specs]]互补：极简spec决定"做什么"，research preview决定"怎么发布"，两者叠加实现极短交付周期。

"永久 beta"能持续多久？用户的忍耐度有上限。Cat Wu 承认需要做更多教育工作帮用户理解核心功能和最佳实践。([[cat-wu-ai-pm-role]])

速度文化的风险也有真实案例：Claude Code 源代码通过 npm 包泄露，经过两层人工审查仍漏过。Cat 定性为**流程失败**，相关人员未被开除——"最重要的是学习教训、加强防护"。这揭示了速度文化的内在张力：越快发布，流程审查越容易出漏洞 ([[cat-wu-ai-pm-role]])。
