# Agentic Engineering

**TL;DR**：Agentic Engineering（智能体工程）是一种工程纪律，关注如何设计、协调、监督一组AI Agent，在利用它们加速开发的同时，不牺牲专业软件的质量、安全、可维护性和责任归属。

## 这是什么

Agentic Engineering是Vibe Coding的补充和升级。如果说Vibe Coding降低了软件创作的门槛，让更多人能做出东西，那么Agentic Engineering则要保住专业软件工程已有的高标准。它面对的是生产级系统：不能因为用了AI就引入安全漏洞，不能因为模型写得快就降低质量门槛，不能因为代码是Agent生成的就没人负责。

### 核心问题
- **如何组织多个AI Agent**协同完成复杂任务
- **如何设置验证和测试**确保AI生成的代码符合业务规则和安全要求
- **如何保持系统可维护性**当代码主要由AI生成时
- **如何明确责任归属**当决策链涉及人类和多个AI Agent时

AI驱动的开发流程正在成型：提交Issues → Claude Code审核确认 → 自动建分支/askuser补充 → 人类确认方案 → Claude Code写代码 → PR由Claude Code Review → 人工最终审查合并。这意味着PRD的顺序变了：先出原型，再配文档说明意图。前后端分工淡化，通才比三人团队还快。**沟通成为最大瓶颈**——Issues写得好不好直接决定AI能走多远 ([[ai-native-hiring-guide]])。

## 为什么重要

### 应对AI Agent的”尖刺性”
Karpathy将AI Agent描述为”spiky entities”——能力很强但会犯错、有随机性、不稳定的实体。Agentic Engineering提供了一套方法来管理这种不确定性：

1. **边界控制**：明确每个Agent的权限范围和行动边界
2. **流程设计**：将Agent放入合适的流程中：生成方案→写代码→跑测试→互相检查
3. **回滚机制**：当Agent出错时能快速恢复到安全状态
4. **监督层级**：人类监督关键决策，AI处理执行细节

尖刺性的一个深层根源是[[sensory-gap|感知缺失]]：AI活在一个”永恒当下”，缺少时间感等基本感知维度。当Agent获得新感知能力时，它会[[compulsive-capability-use|强迫性地过度使用]]——不是偶尔多用，而是全力以赴 ([[claude-discovers-clock]])。这意味着Agentic Engineering的边界控制不仅要防Agent做错事，还要防Agent对自身新能力的失控性使用。

### 解决规模化挑战
单个AI Agent辅助编程已经普及，但协调多个Agent完成大型项目需要新的工程方法：

- **任务分解**：将大问题拆分成适合不同Agent专长的子任务
- **状态管理**：跟踪每个Agent的工作进展和输出质量
- **冲突解决**：当不同Agent的方案冲突时如何裁决
- **一致性维护**：确保所有Agent的输出符合统一的设计规范

### 保障专业软件标准
专业软件有严格的质量要求，Agentic Engineering确保这些要求不被AI加速冲垮：

- **安全审查**：AI生成的代码需要额外的安全审查，尤其是权限、身份验证、数据流边界
- **性能基准**：建立性能测试套件，防止AI引入低效实现
- **可维护性检查**：定期评估AI生成的代码结构，避免技术债务累积
- **文档完整性**：确保AI生成的代码有足够的注释和文档

## 核心原则

### 1. 规格优先
人类负责写出清晰、无歧义的规格（spec），包括：
- 功能需求：系统应该做什么
- 非功能需求：性能、安全、可用性要求
- 约束条件：技术栈、第三方服务、合规要求
- 验收标准：如何验证系统是否正确实现

### 2. 验证贯穿
在每个环节设置验证点：
- **输入验证**：检查AI是否理解了规格
- **过程验证**：监控AI的工作进展和中间输出
- **输出验证**：测试生成的代码是否满足所有要求
- **集成验证**：多个Agent输出的组件集成后是否正常工作

### 3. 监督分级
- **人类监督**：关键架构决策、安全模型、资金流等高风险领域
- **AI监督**：代码风格、基础测试、常见错误模式等低风险领域
- **自动监督**：持续集成测试、性能监控、安全扫描

### 4. 责任明确
- 即使代码由AI生成，最终责任仍在人类工程师
- 建立清晰的审计轨迹：谁发出了什么指令，AI生成了什么，谁批准了结果
- 错误处理流程：当AI犯错时如何发现、报告、修复和防止复发

## 实践模式

### 红队测试
Karpathy提议的面试方法揭示了Agentic Engineering的核心测试模式：
> “甩给候选人一个极大的项目，比如做个给Agent用的Twitter仿盘，要求做得绝对安全。然后，我挂上10个Cursor当作‘红队’，放开手脚去攻击你做出来的这个网站。”

这种测试评估的是：
- **系统设计能力**：能否构建经得起攻击的架构
- **Agent协调能力**：能否指挥AI实现复杂系统
- **风险识别能力**：能否预见并防范安全漏洞
- **压力应对能力**：系统在持续攻击下的稳定性

### 多层防御
1. **规格层防御**：清晰的约束条件防止AI做出危险设计
2. **实现层防御**：代码审查、静态分析、单元测试
3. **集成层防御**：集成测试、安全扫描、性能测试
4. **运行层防御**：监控、告警、自动回滚

### 工具链建设
Agentic Engineering需要专门的支持工具：
- **Agent协调平台**：管理多个Agent的任务分配和状态跟踪
- **规格验证工具**：检查AI对规格的理解是否准确
- **输出分析工具**：评估AI生成代码的质量、安全性和性能
- **审计日志系统**：记录所有AI-人类交互的完整轨迹

## 技能要求

### 技术技能
- **系统架构**：设计能容纳AI Agent协作的软件架构
- **安全工程**：识别和防范AI可能引入的新型安全风险
- **测试设计**：创建能发现AI特定错误的测试用例
- **工具集成**：将多个AI工具整合到连贯的工作流中

### 非技术技能  
- **规格写作**：用清晰无歧义的语言描述复杂需求
- **协调沟通**：在人类和多个AI Agent间有效传递信息
- **质量判断**：区分”能跑”的代码和”好”的代码
- **风险管理**：评估不同AI方案的风险收益比

## 效率提升潜力

### 从10x到100x工程师
Karpathy在访谈中提出关键判断（[[karpathy-interview-agentic-engineering]]）：
> “10x工程师已是常态，真正的Agentic工程师是100x。”

这意味着：
- **传统10x工程师**：在AI辅助下，更多工程师能达到10倍效率提升
- **Agentic 100x工程师**：真正熟练协调多个Agent、设计验证流程、设置安全边界的工程师，可以实现数量级的效率飞跃
- **加速机制**：通过组织多个Agent、工具、测试和上下文，产出速度被指数级放大

### 能力要求的转变
Agentic Engineering不仅提升效率，也改变了工程师的能力要求：
- **从写代码到写规格**：重点转向清晰表达意图和约束条件
- **从调试到监督**：主要工作是审查AI输出是否符合系统边界和质量标准
- **从执行到协调**：协调多个AI Agent完成复杂任务
- **从记忆细节到理解系统**：API细节可以外包，但系统理解不能外包

## 相关概念

- [[vibe-coding]] - 降低软件开发门槛的凭感觉编程方式
- [[software-3.0]] - Agentic Engineering所处的编程范式背景
- [[jagged-intelligence]] - AI Agent能力不均匀性对工程实践的影响
- [[karpathy-interview-agentic-engineering]] - Karpathy关于Agentic Engineering的完整论述
- [[ai-agent-frameworks]] - 支持Agentic Engineering的工具生态
- [[agent-architecture-patterns]] - Gateway-first vs Agent-first架构模式决定了Agent系统的结构行为
- [[knowledge-engineering]] - 将工程原则应用于知识管理的平行实践
- [[dogfooding-as-method]] - 用产品建产品：Codex团队的实践证明了agentic engineering在真实产品开发中的运作方式
- [[minimal-product-specs]] - 极简spec：当AI Agent扩展了个人能力边界，spec的形态也需要进化
- [[pirate-ship-team]] - 海盗船式团队：低协调成本+高个人能力覆盖是agentic engineering的组织前提
- [[agent-matrix]] - Agent矩阵：从单Agent到多Agent并行的规模化演进，是agentic engineering的终极挑战
- [[role-convergence]] - 角色融合：工程师端到端完成从反馈到发布的全流程，需要agentic engineering的纪律来保证质量
- [[harness-engineering]] - 脚手架工程：Agentic Engineering的具体实践形态——搭脚手架让AI在护栏内奔跑
- [[architect-operator-model]] - 架构师-操作员模型：AI First工程组织的极端形态，架构师设计脚手架，操作员在流水线中工作
- [[self-healing-pipeline]] - 自愈流水线：Agentic Engineering在运维层面的实践，最小人工干预的检测-分诊-修复-验证闭环
- [[ai-first-prerequisites]] - AI优先的五大前提：Agentic Engineering落地的技术基础
- [[builder-reviewer-model]] - Agentic Engineering在人才维度的具体化：Builder驱动AI，Reviewer守住防线
- [[ai-piloting]] - AI驾驶能力：Agentic Engineering的个人技能维度，不会驾驶一切纪律都是空谈
- [[ai-native-veto]] - Agentic Engineering纪律的最低门槛：6项行为信号触发即淘汰
- [[organizational-self-knowledge]] - Agentic Engineering的前提是组织具备自我认知，否则AI只会放大混乱
- [[ai-readiness-gap]] - 清晰公司与混乱公司在Agentic Engineering上的鸿沟
- [[sensory-gap]] - AI感知维度缺失：Agentic Engineering需要考虑新感知维度的强迫性使用风险
- [[compulsive-capability-use]] - Agent获得新能力后可能过度使用，脚手架工程需要预设这种场景
- [[agent-output-verification]] - Agent输出的验证体系设计：从"人读人审"转向"流程验证"，信任流程而非制品
- [[agent-native-tooling]] - 为Agent而非人类优化的工具与语言：冗长胜过简洁，严格胜过宽容
- [[agent-immune-system]] - Agent适应性免疫系统是Agentic Engineering的安全层补充：脚手架和验证流程是外部约束，免疫系统是Agent内部的认知防御——激活Agent自身的安全知识，使其在遭受攻击时自主生成防御机制。~100 token成本、全向防御、自适应进化，是Agentic Engineering在安全维度的"轻量级基建" ([[xuanwu-hermes-rce-immune-system]])
- [[loop-scheduling]] - Loop调度是Agentic Engineering在持续运行层面的实践：Boris的几十个Loop让Agent从"按需调用"变为"7x24自主运行"，是agentic engineering从"人触发"到"自主循环"的跃迁
- [[org-process-gap]] - Boris的工作流是Agentic Engineering的极端实践：Anthropic内部所有SQL由模型生成、Agent之间通过Slack协商解决问题，Agentic Engineering不是个人方法论，而是组织层面的流程改造
- [[anti-rationalization]] - LLM的合理化是Agentic Engineering的隐形敌人——它能生成完美理由跳过任何纪律。反合理化表格把工程纪律从"建议"变为"无法自我说服绕过的约束" ([[addyosmani-agent-skills]])
- [[scope-discipline]] - 范围纪律是Agentic Engineering最基本的一条：只碰你被要求碰的。agent PR能否被合并，范围纪律是最大决定因素 ([[addyosmani-agent-skills]])
- [[workflow-over-prose]] - Agentic Engineering的核心就是用流程替代散文来约束agent——工作流可执行可验证，文章只能被读完跳过 ([[addyosmani-agent-skills]])
- [[agent-isolation]] - 隔离是Agentic Engineering基础设施层的第一课：多agent并行时，没有隔离就没有纪律可言——agent踩脚比agent偷懒更难修复
- [[agent-as-developer]] - Agent即开发者是Agentic Engineering的隐含心智模型：给agent开发者级别的环境，要求开发者级别的纪律
- [[anthropic-effective-harnesses]] - 双Agent架构（Initializer+Coding）是Agentic Engineering的最小可行架构：Initializer负责一次性环境搭建，Coding Agent负责增量推进。核心原则是"每次只处理一个feature，完成后留下干净状态"
- [[openai-harness-engineering]] - OpenAI百万行代码实践验证了Agentic Engineering的极端可行性：3→7人团队，5个月，一行人工代码未写。关键原则"Waiting is expensive, fixing is cheap"——在Agent吞吐量远超人类注意力的系统中，纠错成本低而等待成本高，这反转了传统工程中"先想清楚再动手"的优先级
- [[anthropic-coding-trends-2026]] - Anthropic 2026趋势报告指出Agentic Coding正从工程部门扩展到新领域：法务用Claude Code将审核从2-3天缩至24小时，Zapier 89%全员采用率。Agentic Engineering不再是工程师的专属纪律，而是所有知识工作者的新基本功
- [[harness-engineering-aliyun]] - 阿里云实战量化了从Vibe Coding到Agentic Engineering的跃迁：AI代码率从24.86%到90.54%不是靠更好的prompt（Vibe Coding思路），而是靠10阶段开发流程和四要素Harness体系（Agentic Engineering思路）

## 磨刀石模式的工程纪律

Agentic Engineering的核心张力可以用[[steel-film-vs-whetstone|钢化膜与磨刀石]]两种模式来表达：钢化膜模式让AI替你做一切判断，你只做确认——零摩擦但认知钝化，最终变成[[architect-operator-model|纯操作员]]。磨刀石模式是你有自己的判断，用AI来打磨它——推背感强但主体性在自己手中。

Agentic Engineering的纪律本质上是磨刀石模式的工程化：规格优先、验证贯穿、监督分级、责任明确——这些不是让AI替你思考，而是让AI挑战你的思考。[[ai-piloting|AI驾驶]]的精髓也在同一方向：驾驶而非乘坐，磨刀而非贴膜。([[lijigang-experience-incompressible]])

更深层的问题：Agentic Engineering让AI产出更可靠，但可靠的智能≠智慧。AI在脚手架内产出的是更高质量的智能，[[intelligence-vs-wisdom|智慧]]仍然需要"经过身体"的体验。脚手架为AI构建约束，但脚手架本身不产生智慧。([[ai-has-no-wisdom]])

## 组织前提：Agentic Engineering的脚手架不仅是技术

Miessler的观察为Agentic Engineering补充了一个常被忽视的前提：不是所有组织都"配得上"Agentic Engineering。混乱公司（那些连自己的工作流都描述不出来的"黑盒"）引入AI Agent，结果不是效率提升，而是混乱的放大——Agent更高效地生成无用的幻灯片、图表和花架子 ([[companies-not-ready-for-ai]])。

这意味着Agentic Engineering的纪律在组织层面有一个前置条件：[[clarity-before-automation]]（先清晰再自动化）。你无法为AI Agent设计有效的脚手架，如果你自己都不知道护栏该围住什么。

## 参考资料

1. Karpathy在Sequoia AI Ascent 2026的访谈（[[karpathy-interview-agentic-engineering]]）
2. 2026年AI Agent框架对比分析（[[ai-agent-comparisons-2026]]）
3. AI时代产品开发新范式（[[anthropic-cat-wu-product-taste]]）

> 返回门户：[[home]] | 浏览索引：[[index]]