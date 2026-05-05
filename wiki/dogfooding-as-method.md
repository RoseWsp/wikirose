# 用产品建产品

AI团队不只是"吃自己的狗粮"（用自己开发的产品），而是把dogfooding变成核心工作方法——用产品来思考，用产品来沟通，用产品来决策。

## 这意味着什么

传统dogfooding是质量保证：用自己的产品发现bug。AI时代的dogfooding是**认知工具**：PM用AI Agent在代码库里探索方案，不是为了产出代码，而是为了建立心智模型，然后把这份理解（而非计划本身）分享给工程师。([[codex-team-dogfooding]])

这个转变有具体的数据支撑：Codex团队的设计师写的代码量超过了6个月前的工程师。这不是设计师"顺便写两行"，而是AI工具让非编程角色真的能直接参与构建。PM用Codex做"思维探索"——在代码库里游走、试方案、建立直觉，然后把认知传递出去 ([[codex-team-dogfooding]])。

这个转变的根本原因是AI让每个人的能力边界扩大了。以前工程师没时间做任务分类是因为要集中精力写代码，现在代码可以委派给Agent，工程师有了更多时间做"PM的事"。设计师也是——Codex团队的设计师写的代码量超过了6个月前的工程师。([[pm-as-gap-filler]])

## 为什么有效

关键前提：**你是自己产品的用户**。Codex团队构建开发者工具，团队成员全是开发者。Stripe在250人时零PM，原因一样——他们全都是工程师，构建自己想要的API，每个人都知道一个优雅的API长什么样。([[pirate-ship-team]])

当这个前提不成立时——比如Codex要面向ChatGPT的9亿非技术用户——dogfooding的方法还能不能延续，是个开放问题。

## 关联

- [[loonshots-dual-organization]] — Snap的双组织模型中，内部App"摇一摇报告bug+AI自动诊断修复"是dogfooding在AI时代的新形态：不只是团队自己用产品，而是用AI把dogfooding的反馈闭环自动化 ([[spiegel-software-no-moat]])

- [[product-taste]] — dogfooding的前提是你有品味判断"应该构建什么"
- [[agentic-engineering]] — 用产品建产品需要新的工程纪律来保证质量
- [[vibe-coding]] — Codex团队明确区分自己不是"凭感觉编程"，而是在系统思考和质量把控上大量投入
- [[action-based-ai]] — Codex的plan mode让人和AI一起在代码层面探索可能性
- [[self-healing-pipeline]] — CREAO用智能体平台重建智能体平台的极致dogfooding，同时构建了自愈流水线
- [[harness-engineering]] — 用产品建产品的高级形态：不只是用产品，而是围绕AI重新设计整个工程脚手架

Boris Cherny强调了dogfooding的战略意义：Anthropic之所以坚持用和外部完全一样的模型，是因为他们在构建一个平台——开发者用的东西必须和自己用的一样。这解释了为什么[[org-process-gap|组织流程代差]]比技术差距更关键——同样的技术，不同组织渗透程度天差地别。([[boris-chenyi-sequoia-ai-ascent]])
