# 脚手架工程 (Harness Engineering)

**TL;DR** 工程团队的核心工作不再是写代码，而是为AI构建工作环境和约束条件——让AI能做有价值的事，并在出错时有系统兜底。

## 这意味着什么

OpenAI在2026年2月提出"脚手架工程"这个概念，但CREAO在实践中已经先行摸索出了同一路径。核心理念：当系统出错时，不是"再试一次"或"再努力点"，而是问——AI缺失了什么能力？如何让这个能力对智能体变得清晰可见？

三个致命瓶颈驱动了CREAO的变革：PM花几周做需求vs AI两小时实现、QA测三天vs AI写代码两小时、25人vs对手数百人。解决方案不是加人，而是把人从链条里拿掉，让AI端到端负责。结果：99%生产代码由AI编写，每天3-8次部署，功能当天上当天撤 ([[ai-first-strategy-wrong]])。

脚手架工程把传统工程从"人写代码、人审查、人部署"翻转为"人设计约束、AI执行、人判断方向"。工程师的角色从建造者变成脚手架搭建者——你搭好框架，AI在框架内安全高效地工作。

## 关键实践

- **统一代码库(Monorepo)**：碎片化代码库对AI是隐形的，统一代码库让AI纵览全局、推理跨服务连锁反应 ([[ai-first-strategy-wrong]])
- **确定性流水线**：每个阶段都自动化且不可跳过，AI能预测结果并推理失败原因
- **结构化可观测性**：所有日志和指标必须结构化、可查询，如果AI读不懂日志就无法诊断问题
- **自动分诊**：错误自动聚类、自动评估严重度、自动创建工单，工程师只做验证
- **Issue写作质量**：在AI驱动流程中，给AI提供清晰上下文就是搭建认知脚手架。模糊的Issue（如"修复搜索bug"）让AI反复askuser，拖慢所有人；高质量的Issue（背景+复现路径+预期行为+边界条件）让AI可以直接行动。Issue写作能力已成为工程师的核心基本功 ([[ai-native-hiring-guide]])

## 与相关概念的区别

脚手架工程不是[[vibe-coding]]——Vibe Coding是凭感觉调prompt直到跑通，脚手架工程是构建让AI稳定产出的系统。Vibe Coding只能做原型，脚手架工程才能做生产 ([[ai-first-strategy-wrong]])。

脚手架工程是[[agentic-engineering]]的具体实践形态——Agentic Engineering定义了"在使用Agent加速的同时保持专业质量"的纪律，脚手架工程给出了"怎么做到"的答案：搭脚手架，让AI在护栏内奔跑。

## 为什么现在重要

模型能力进化极快。CREAO的创始人说，所有质变都归功于过去两个月——Claude Opus 4.5做不到的，Opus 4.6做到了。下一代模型只会让脚手架工程更加必要：AI越强，没有护栏的灾难越大，有护栏的收益也越大。

但AI First不是万能的。即使五大前提都做到，也只适合一部分场景：后端逻辑为主、内部工具、早期产品快速试错。不适合的场景包括UI密集产品、功能质量敏感产品、安全性要求高场景。值得注意的是，Anthropic和OpenAI自己都不敢在Claude Code和Codex上全自动迭代——这就是最好的反面证据 ([[ai-first-strategy-wrong]])。

宝玉xp的关键洞察：AI First的真正终点未必是让AI干所有活，而是借着这股力量，把一直想做但没动力做的工程改进真正推动起来。仰望星空，脚踏实地。

## 关联

- [[agentic-engineering]]——脚手架工程是Agentic Engineering的具体实践
- [[ai-first-prerequisites]]——脚手架工程的五大技术前提
- [[self-healing-pipeline]]——脚手架工程的核心产出：自愈闭环
- [[architect-operator-model]]——脚手架工程催生的新组织结构
- [[vibe-coding]]——脚手架工程的对立面：一个靠系统，一个靠感觉
- [[product-taste]]——架构师的核心能力是批判AI的品味
- [[action-based-ai]]——脚手架工程是行动派AI在工程层面的落地
- [[ai-first-strategy-wrong]]——源文件
- [[builder-reviewer-model]]——Builder搭脚手架，Reviewer验证脚手架有效性
- [[ai-piloting]]——驾驭AI Agent是搭脚手架的前提：不会驾驶，搭再好的脚手架也没用
- [[dual-horizon-planning]]——CREAO每天3-8次部署的极端速度，靠的是脚手架工程而不是规划本身
- [[organizational-self-knowledge]]——脚手架工程的前提是组织具备自我认知，能清晰描述目标和工作流
- [[clarity-before-automation]]——先清晰再自动化：脚手架工程是"先想清楚做什么"的工程方法论
