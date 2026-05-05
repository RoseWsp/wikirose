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

脚手架工程不是[[vibe-coding]]、[[ai-native-veto]]——Vibe Coding是凭感觉调prompt直到跑通，脚手架工程是构建让AI稳定产出的系统。Vibe Coding只能做原型，脚手架工程才能做生产 ([[ai-first-strategy-wrong]])。

脚手架工程是[[agentic-engineering]]的具体实践形态——Agentic Engineering定义了"在使用Agent加速的同时保持专业质量"的纪律，脚手架工程给出了"怎么做到"的答案：搭脚手架，让AI在护栏内奔跑。

## 为什么现在重要

模型能力进化极快。CREAO的创始人说，所有质变都归功于过去两个月——Claude Opus 4.5做不到的，Opus 4.6做到了。下一代模型只会让脚手架工程更加必要：AI越强，没有护栏的灾难越大，有护栏的收益也越大。

但AI First不是万能的。即使五大前提都做到，也只适合一部分场景：后端逻辑为主、内部工具、早期产品快速试错。不适合的场景包括UI密集产品、功能质量敏感产品、安全性要求高场景。值得注意的是，Anthropic和OpenAI自己都不敢在Claude Code和Codex上全自动迭代——这就是最好的反面证据 ([[ai-first-strategy-wrong]])。

Boris Cherny的判断指向了脚手架工程的消亡方向：他预言Claude Code一年后可能只剩100行代码。随着模型自主行动能力增强，prompt注入保护、命令校验、权限模式等安全机制都会变得不重要——因为模型会自己做正确的事。他解释了重心的转移："随着模型越来越强，工具本身的'脚手架'的重要性在下降。我们现在在想的是：如何让循环任务变成一等公民？如何让并行运行大量智能体变得更简单？"——脚手架让位于[[loop-scheduling|Loop]]和[[agent-matrix|并行Agent]]编排。([[boris-chenyi-sequoia-ai-ascent]])

宝玉xp的关键洞察：AI First的真正终点未必是让AI干所有活，而是借着这股力量，把一直想做但没动力做的工程改进真正推动起来。仰望星空，脚踏实地。

## 关联

- [[agentic-engineering]]——脚手架工程是Agentic Engineering的具体实践
- [[ai-first-prerequisites]]——脚手架工程的五大技术前提
- [[self-healing-pipeline]]——脚手架工程的核心产出：自愈闭环
- [[architect-operator-model]]——脚手架工程催生的新组织结构
- [[vibe-coding]]、[[ai-native-veto]]——脚手架工程的对立面：一个靠系统，一个靠感觉
- [[product-taste]]——架构师的核心能力是批判AI的品味
- [[action-based-ai]]——脚手架工程是行动派AI在工程层面的落地
- [[ai-first-strategy-wrong]]——源文件
- [[builder-reviewer-model]]——Builder搭脚手架，Reviewer验证脚手架有效性
- [[ai-piloting]]——驾驭AI Agent是搭脚手架的前提：不会驾驶，搭再好的脚手架也没用
- [[dual-horizon-planning]]——CREAO每天3-8次部署的极端速度，靠的是脚手架工程而不是规划本身
- [[organizational-self-knowledge]]——脚手架工程的前提是组织具备自我认知，能清晰描述目标和工作流
- [[clarity-before-automation]]——先清晰再自动化：脚手架工程是"先想清楚做什么"的工程方法论
- [[general-specialized-architecture]]——脚手架工程为AI构建的"工作环境"本质上就是通用+专用的分工：通用模型编排，专用系统执行
- [[jevons-paradox-inference]]——推理配额是脚手架的长期约束，Agent预算管理不只是成本优化
- [[continual-learning]]——Hassabis指出缺乏持续学习是Agent无法"交付后不管"的根本原因，脚手架工程在持续学习突破前只能用上下文窗口等"胶带方案"应急
- [[sensory-gap]]——AI对新感知维度的强迫性使用意味着脚手架必须预设过度使用场景并设置约束
- [[compulsive-capability-use]]——给AI新工具时，预设它会过度使用，在脚手架中设置适当约束
- [[agent-output-verification]]——脚手架的上游约束是Agent输出验证的"上游层"，为Agent构建可验证的执行规格
- [[agent-native-tooling]]——脚手架工程为Agent构建约束环境，Agent-native工具为Agent构建原生工作介质——两者是同一转变的两面
- [[loop-scheduling]]——Loop调度减少了对脚手架的依赖：模型自主决定何时循环运行，脚手架的重要性随模型增强而下降
- [[org-process-gap]]——组织流程代差是脚手架工程的组织层面对应：工程面搭脚手架+组织面改造流程=AI最大化嵌入
- [[intelligence-vs-wisdom]]——脚手架为AI构建约束，但脚手架本身不产生智慧——AI有智能无智慧，约束的是行为不是认知
- [[experience-incompressible]]——脚手架压缩了AI出错的概率，但无法压缩人类体验——两者是不同维度的防线
- [[agent-immune-system]]——脚手架为Agent建外部护栏，免疫系统为Agent建内部认知防御——同一思路的两个方向
- [[recursive-self-improvement]]——递归自改进拷问脚手架的极限：对齐技术99.9%准确率，500代后只剩60.5%。当被约束的系统比约束它的系统更聪明时，脚手架还撑得住吗？（[[jack-clark-ai-self-construction]]）
- [[automated-ai-rd]]——自动化AI研发意味着脚手架本身也变成AI的制品——不只代码是AI写的，验证代码的流程也是AI设计的
- [[bounded-rationality]]——脚手架工程本质上就是给AI划定有限理性的边界——不追求全局最优，在约束范围内做局部满意决策
- [[curse-of-dimensionality]]——维度灾难让全局最优不可达，脚手架是在不可达前提下的务实策略：划定搜索边界，在边界内求满意解

## 组织层面的脚手架

Miessler的观察揭示了一个更深的前提：脚手架工程能发挥作用的前提不只是技术基础设施，而是组织本身已经理清了"要做什么"和"怎么运转"。混乱公司的问题不是缺CI/CD——而是连自己的工作流(work streams)都描述不出来。对这种公司，脚手架工程无从搭起，因为你不知道要为AI搭建什么约束 ([[companies-not-ready-for-ai]])。

工程层面的"先搭脚手架再让AI跑"和组织层面的"先清晰目标再让AI执行"是同一枚硬币的两面——[[harness-engineering]]管的是工程面的脚手架，[[organizational-self-knowledge]]管的是组织面的脚手架。两者缺一不可。
