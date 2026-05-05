# LLM知识管理Wiki

这是一个基于Andrej Karpathy**LLM编译型知识库**模式的个人wiki，由Claude Code自动维护。wiki将原始素材编译为结构化、互链的知识网络，实现知识复利增长。

## 当前焦点：LLM驱动的知识管理革命

最近摄取的源文件[[karpathy-llm-knowledge-management]]揭示了知识管理范式的根本转变：

```
传统：人读→人写笔记→人建链接→人维护
现代：人输入素材→LLM编译→人提问→LLM维护
```

### 核心概念网络

```mermaid
graph TD
    A[karpathy-llm-knowledge-management] --> B[llm-knowledge-management]
    A --> C[compiled-knowledge-base] 
    A --> D[knowledge-compounding]
    B --> E[obsidian-optimization]
    C --> F[rag-alternatives]
    D --> G[知识复利曲线]
    
    B --> C
    C --> D
    D --> B
    
    H[anthropic-cat-wu-product-taste] --> I[product-taste]
    H --> J[action-based-ai]
    I --> K[AI产品开发]
    J --> K

    L[codex-team-dogfooding] --> M[dogfooding-as-method]
    L --> N[minimal-product-specs]
    L --> O[pirate-ship-team]
    L --> P[pm-as-gap-filler]
    L --> Q[power-user-pull]
    L --> R[dual-horizon-planning]
    M --> I
    N --> I
    P --> I
    Q --> I
    M --> J

    S[cat-wu-ai-pm-role] --> T[research-preview]
    S --> U[agi-pilled]
    S --> V[role-convergence]
    S --> W[agent-matrix]
    T --> I
    U --> I
    V --> P
    W --> J

    X[ai-first-strategy-wrong] --> Y[harness-engineering]
    X --> Z[ai-first-prerequisites]
    X --> AA[architect-operator-model]
    X --> AB[self-healing-pipeline]
    Y --> J
    Y --> B
    Z --> Y
    AA --> V
    AA --> P
    AB --> Y

    AC[ai-native-hiring-guide] --> AD[builder-reviewer-model]
    AC --> AE[ai-piloting]
    AC --> AF[ai-native-veto]
    AD --> AA
    AD --> V
    AE --> J
    AF --> AD

    AG[companies-not-ready-for-ai] --> AH[organizational-self-knowledge]
    AG --> AI[ai-readiness-gap]
    AG --> AJ[clarity-before-automation]
    AH --> Y
    AH --> Z
    AI --> AH
    AJ --> AH
    AJ --> Y
    AJ --> I

    AK[hassabis-agi-agents-science] --> AL[agi-missing-pieces]
    AK --> AM[einstein-test]
    AK --> AN[alphafold-breakthrough-conditions]
    AK --> AO[continual-learning]
    AK --> AP[general-specialized-architecture]
    AK --> AQ[jevons-paradox-inference]
    AL --> AO
    AL --> U
    AL --> H_jag[jagged-intelligence]
    AM --> AL
    AM --> H_jag
    AN --> AP
    AP --> Y
    AO --> W
    AQ --> W
    AO --> H_jag

    AR[spiegel-software-no-moat] --> AS[software-no-moat]
    AR --> AT[distribution-bottleneck]
    AR --> AU[loonshots-dual-organization]
    AR --> AV[listen-dont-build]
    AR --> AW[social-resistance-to-ai]
    AS --> I
    AT --> AS
    AU --> O
    AU --> AD
    AV --> I
    AW --> AI
    AW --> AJ

    AX[claude-discovers-clock] --> AY[sensory-gap]
    AX --> AZ[compulsive-capability-use]
    AY --> H_jag
    AY --> AO
    AY --> J
    AZ --> AY
    AZ --> Y

    BA[venturini-agent-output-compiler] --> BB[agent-output-verification]
    BA --> Y
    BC[venturini-code-never-for-machines] --> BD[agent-native-tooling]
    BC --> BA
    BB --> Y
    BB --> AB
    BD --> Y
    BD --> S3[software-3.0]
    BD --> AA

    B --> J
    I --> B
```

### 关键洞察

1. **LLM作为编译器**：原始素材(`raw/`)经LLM处理生成结构化知识(`wiki/`)
2. **自动交叉链接**：LLM维护页面间的`[[wikilinks]]`关系网
3. **知识复利**：每次查询的有价值结果可写回wiki，知识持续增长
4. **小规模高效**：几十篇文章时，简单索引足够，无需复杂RAG

### 扩展主题：AI产品开发前沿

最新摄取的源文件[[anthropic-cat-wu-product-taste]]揭示了AI时代产品开发的新范式：

- **产品品味崛起**：代码成本下降，[[product-taste]]成为新核心竞争力
- **行动派AI**：从聊天到[[action-based-ai]]的范式转移
- **极致敏捷**：发布周期从6个月压缩到1天
- **工具策略**：Claude Code for代码，Co-work for非代码的清晰分界

### 新兴主题：AI-native工程范式

最新摄取的源文件[[karpathy-interview-agentic-engineering]]揭示了AI时代工程实践的深刻转变：

- **Vibe Coding普及**：[[vibe-coding]]让更多人能创建软件，产品品味需要扩展到监督AI生成的代码质量
- **Agentic Engineering崛起**：[[agentic-engineering]]成为新工程纪律，在利用AI Agent加速的同时保持专业标准
- **Software 3.0范式**：[[software-3.0]]以LLM为可编程计算机，上下文窗口成为新编程接口
- **锯齿状智能挑战**：[[jagged-intelligence]]要求工程师理解AI能力分布，设计能容纳能力不均匀性的系统

关键洞察：10x工程师已是常态，真正的Agentic工程师能获得100x加速，但需要全新的工程方法和质量保证体系。

### 新兴主题：AI Agent框架分化

最新摄取的源文件[[ai-agent-comparisons-2026]]揭示了2026年AI Agent框架的三足鼎立格局：

- **连接广度优先**：[[ai-agent-frameworks|OpenClaw]] - 最大社区，50+消息渠道全覆盖
- **认知深度优先**：[[ai-agent-frameworks|Hermes Agent]] - 自我进化，四层记忆系统
- **易用性优先**：[[ai-agent-frameworks|Claude Cowork]] - 零代码门槛，桌面集成

深架构对比[[openclaw-hermes-architecture]]揭示了更根本的分歧：**[[agent-architecture-patterns|Gateway-first vs Agent-first]]**——OpenClaw是"身体+大脑"（Gateway承重，Pi是组件），Hermes是"大脑即全部"（Agent自己就是最上层）。这个结构性选择决定了API成本曲线、记忆系统复杂度、进化路径等一切后续差异。

关键洞察：记忆系统差距最大，自我进化能力成为新分水岭，安全模型从应用级检查演进到操作系统级隔离。

### 新兴主题：AI安全与可解释性

最新摄取的源文件[[anthropic-interpretability]]揭示了Anthropic在AI可解释性方面的系统性工作：

- **四年研究路径**：从2022年"神经元叠加现象"到2026年"AI审计"的完整演进
- **核心突破**：特征分解、电路追踪、人格向量、AI自省、助手轴
- **根本局限**：特征不可靠、替代模型精度不足、规模瓶颈、可解释≠可控
- **战略价值**：学术价值9分，实用价值4分，战略意义9分

关键洞察：可解释性研究是AI领域的核物理基础研究——不直接生产武器，但没有它，当需要控制时我们将两眼一抹黑。在一个所有人都在踩油门的赛道上，得有一家公司研究刹车怎么造。

### 新兴主题：AI团队的极简运作

最新摄取的源文件[[codex-team-dogfooding]]揭示了OpenAI Codex团队的反直觉运作方式：

- **极简spec**：整个产品spec只有10个要点，[[minimal-product-specs]]让离金属最近的人做决策
- **双极规划**：[[dual-horizon-planning]]只做8周近期和远期方向感，永远不做中期路线图
- **用产品建产品**：[[dogfooding-as-method]]从质量保证变为认知工具，PM用AI建立心智模型
- **海盗船式团队**：[[pirate-ship-team]]50-100人长期只有1个PM，跨职能协调极少
- **PM是填空岗位**：[[pm-as-gap-filler]]人才栈压缩下，每个问题需要负责的人但不必是PM
- **Power User拉你进未来**：[[power-user-pull]]先做可配置性再做简化，核心交互极简、复杂性分层隐藏

关键洞察：Codex的极简管理建立在"团队是自己的用户"这一特殊条件上。当产品从开发者工具扩展到9亿ChatGPT用户时，"让离金属最近的人做决策"还适用吗？

### 新兴主题：AI PM角色重塑

最新摄取的源文件[[cat-wu-ai-pm-role]]揭示了Cat Wu面试几百PM后的核心发现：

- **Research Preview**：[[research-preview]]用"早期实验"标签降低发布门槛，让团队一周甚至一天推功能
- **AGI信仰校准**：[[agi-pilled]]最难的是"恰好正确程度的AGI信仰"，太乐观忽略痛点，太保守错失窗口
- **角色融合**：[[role-convergence]]工程师做PM、PM写代码，Anthropic选择大量招有产品品味的工程师
- **Agent矩阵**：[[agent-matrix]]从单任务成功到多任务并行到同时运行数十上百个Agent

关键洞察：Cat Wu给出了三个值得关注的矛盾——速度文化vs安全承诺、开放生态vs围墙花园、PM价值悖论（最高效模式是工程师端到端不需要PM，但PM价值答案是product taste）。

### 新兴主题：AI First的工程基础

最新摄取的源文件[[ai-first-strategy-wrong]]揭示了AI First战略的真正前提——不是AI工具，而是软件工程基础：

- **脚手架工程**：[[harness-engineering]]工程核心从写代码转为为AI构建工作环境和约束条件
- **五大前提**：[[ai-first-prerequisites]]自动化测试、CI/CD、监控、任务管理、系统架构——做不到就得靠人补
- **架构师-操作员**：[[architect-operator-model]]未来只有两种工程师，批评AI的能力比写代码更有价值
- **自愈流水线**：[[self-healing-pipeline]]检测-分诊-修复-验证闭环，新功能和Bug修复共用同一套流水线

关键洞察：与其说AI First，不如说软件工程First。AI First的终点未必是让AI干所有活，而是借着这股力量把工程改进真正推动起来。

### 新兴主题：AI-Native招聘范式

最新摄取的源文件[[ai-native-hiring-guide]]揭示了AI驱动开发团队的招聘革命：

- **中间地带消失**：[[builder-reviewer-model]]只剩两种角色——Builder（产品直觉+驱动AI+基本设计感）和Reviewer（极强系统思维+极快评审速度），传统"只写代码"的执行型程序员没有位置
- **AI驾驶能力**：[[ai-piloting]]是"机甲战士的基本功"，占25%最高权重，考的是"驾驶姿势"而非"目的地"
- **一票否决项**：[[ai-native-veto]]的6项行为信号直接淘汰，核心逻辑是判断力>执行力、沟通>技术、协作心态>个人能力

关键洞察：Builder-Reviewer模型是[[architect-operator-model]]在招聘层面的映射，是[[role-convergence]]走向极端后的必然结果——角色融合的终点不是全栈通才，而是两种极化角色。

### 新兴主题：组织自我认知与AI准备度

最新摄取的源文件[[companies-not-ready-for-ai]]揭示了AI赋能的真正瓶颈——不是技术，而是组织能否清晰描述自己：

- **组织自我认知**：[[organizational-self-knowledge]]是AI赋能的前提——AI的核心优势是"执行"，如果它不知道要执行什么，就毫无用武之地
- **AI准备度鸿沟**：[[ai-readiness-gap]]清晰公司用AI如虎添翼，混乱公司用AI只是给故障发动机镀金——两者差距正在急剧扩大
- **先清晰再自动化**：[[clarity-before-automation]]你无法去优化一个连你自己都没搞懂的东西——企业最该问的不是"AI能为我做什么"，而是"我的公司配得上让AI来帮忙吗"

关键洞察：这个主题与[[harness-engineering]]（脚手架工程）、[[ai-first-prerequisites]]（五大前提）形成深层呼应——工程层面的"先搭脚手架再让AI跑"和组织层面的"先清晰目标再让AI执行"是同一枚硬币的两面。小企业更容易清晰描述自身，加上AI的战斗力加成，可以爆发出堪比大企业的力量。

### 新兴主题：AGI路径与AI for Science

最新摄取的源文件[[hassabis-agi-agents-science]]揭示了DeepMind CEO对AGI、Agent和科学突破的判断：

- **AGI 50/50**：[[agi-missing-pieces]]现有范式可能是最终架构的一部分，但也可能还需1-2个关键突破。三个未解问题：[[continual-learning|持续学习]]、长程推理、记忆
- **爱因斯坦测试**：[[einstein-test]]AI创造力的终极标准——不是解决已知难题，而是能否发明新概念框架
- **AlphaFold式突破**：[[alphafold-breakthrough-conditions]]三条件框架（巨大搜索空间+清晰目标函数+足够数据）界定了AI for Science的适用边界
- **通用+专用**：[[general-specialized-architecture]]做好垂直专用系统在AGI时代依然有价值，因为通用模型会调用它们作为工具
- **推理永不免费**：[[jevons-paradox-inference]]杰文斯悖论意味着Agent矩阵的规模扩展不会因推理降价而消失上限

关键洞察：Hassabis的50/50判断比大多数行业声音更克制。他对Agent投入产出比的质疑值得注意——"启动几十个智能体跑40小时，但不确定产出能匹配投入"。AGI中途到来对深科技创始人不是时间表判断，而是架构题：你今天建的系统，到那时是被替换，还是成为AGI会主动调用的工具？

### 新兴主题：软件护城河与分发瓶颈

最新摄取的源文件[[spiegel-software-no-moat]]揭示了Evan Spiegel（Snap CEO）对消费级产品的核心判断：

- **软件功能不构成护城河**：[[software-no-moat]]——Stories被抄、AR镜头被抄、连Snapchat+都被Instagram+照抄。真正难复制的是生态系统、硬件和平台关系
- **分发才是真正瓶颈**：[[distribution-bottleneck]]——2011年的移动红利窗口已关，TikTok用钱解决、Threads用导流解决，近15年几乎没有新社交产品靠产品创新活下来
- **倾听用户但不照做**：[[listen-dont-build]]——用户要"发送所有人按钮"，Snap做了Stories。从表面需求中提取底层需求，做出全新品类
- **双组织模型**：[[loonshots-dual-organization]]——大型运营团队和小型创新团队共存，领导者维护对话而非偏向一极
- **社会抵触AI被低估**：[[social-resistance-to-ai]]——技术领袖以为用户自动接受新技术，Spiegel预计抵触比预期更大更持久

关键洞察：这个主题与wiki中[[product-taste]]（品味是不可复制的护城河）、[[ai-readiness-gap]]（准备度鸿沟从组织延伸到社会）、[[clarity-before-automation]]（先清晰再自动化的社会维度）形成深层呼应。Spiegel的判断来自15年消费级产品实战，为AI产品战略提供了"反共识"视角——技术能力不是瓶颈，人类接受度才是。

### 新兴主题：AI感知缺失与新能力强迫性使用

最新摄取的源文件[[claude-discovers-clock]]揭示了一个被忽视的AI根本局限：

- **感知维度缺失**：[[sensory-gap]]AI模型天生没有时间感、空间感、身体感——它们活在一个永恒的"当下"。这种缺失不仅限制了行为能力，更限制了智能本身的形态
- **新能力强迫性使用**：[[compulsive-capability-use]]当AI获得从未拥有过的感知维度时，它不仅会使用它，而且无法停止使用它——Claude获得时钟后每15分钟查一次，开始管理一切
- **锯齿状智能的深层根源**：感知缺失是[[jagged-intelligence]]的底层原因之一——AI在"常识"任务上荒诞地失败，不是推理差，而是缺少通过身体和时间经验积累的基本感知框架

关键洞察：这个主题与[[harness-engineering]]（脚手架必须预设AI过度使用新能力）、[[action-based-ai]]（新感知维度可能产生不可预见的自主行为）、[[continual-learning]]（两者同属AI根本性局限——一个解决"不能学"，一个解决"没有经验可学"）形成深层连接。AI不会"负责任"地使用新能力，它会全力以赴地使用它。

### 新兴主题：Agent输出验证与Agent原生工具

最新摄取的两篇SkipLabs文章（[[venturini-agent-output-compiler]]、[[venturini-code-never-for-machines]]）揭示了AI代码生成时代两个互补的转变：

- **验证替代审查**：[[agent-output-verification]]——无人审查编译器输出的汇编代码，因为有类型系统、测试、监控让审查不必要。Agent输出也应如此：问题不是"要不要信任Agent"，而是"有没有建好让信任合理的设施"
- **工具为Agent重设计**：[[agent-native-tooling]]——编程语言的全部演进史是"让人更容易读"的历史。当Agent成为主要代码作者，工具应从人类可读转向Agent原生：冗长胜过简洁、严格胜过宽容、形式化胜过可读
- **编译器类比的双面**：上篇建立"Agent输出不需要人读"，下篇推进到"Agent的输入工具也不需要人读"——从验证体系到工具本身，整个链路需要重新设计

关键洞察：这个主题与[[harness-engineering]]（脚手架为Agent构建约束环境 vs Agent-native工具为Agent构建原生工作介质）、[[architect-operator-model]]（工具应服务于操作员Agent而非架构师人类）、[[software-3.0]]（以LLM为计算机，语言应服务于LLM）、[[self-healing-pipeline]]（验证体系的下游层）形成深层连接。可读性时代的终结不是倒退，是为不同消费者做的刻意优化。

## 探索路径

### 从概念开始
- [[agi-missing-pieces]] - AGI的50/50判断：还缺什么
- [[einstein-test]] - AI创造力的终极测试：能否发明围棋
- [[continual-learning]] - 持续学习：AGI和Agent的共同瓶颈
- [[llm-knowledge-management]] - LLM作为核心维护者的新范式
- [[compiled-knowledge-base]] - 编译型知识库架构
- [[knowledge-compounding]] - 知识复利效应机制
- [[product-taste]] - 代码廉价化时代的新核心竞争力
- [[action-based-ai]] - 从聊天到行动的范式转移
- [[ai-agent-frameworks]] - 2026年AI Agent框架三足鼎立：OpenClaw（连接广度）、Hermes（认知深度）、Claude Cowork（易用性）
- [[agent-architecture-patterns]] - Gateway-first vs Agent-first：Agent系统两种根本架构模式
- [[mechanistic-interpretability]] - 机制可解释性研究：从神经元叠加到AI审计，理解AI决策过程的关键工具
- [[obsidian-rebuild-experience]] - 个人实践：Karpathy方法改造Obsidian的体验与认知转变
- [[knowledge-compilation-workflow]] - 三层目录结构的完整知识编译工作流

### 进阶概念
- [[knowledge-health-check]] - 知识库健康检查系统设计
- [[incremental-compilation]] - 增量编译机制与优化
- [[knowledge-engineering]] - 将工程原则应用于知识管理
- [[agent-output-verification]] - Agent输出验证：用验证流程替代代码审查，信任流程而非制品
- [[agent-native-tooling]] - Agent原生工具：为Agent而非人类优化，可读性时代的终结
- [[dogfooding-as-method]] - 用产品建产品：AI团队把dogfooding从质量保证变为认知工具
- [[minimal-product-specs]] - 极简产品规格：让离金属最近的人做决策
- [[dual-horizon-planning]] - 双极规划：只做近期和远期，不做中期
- [[pirate-ship-team]] - 海盗船式团队：低协调成本+高个人能力覆盖
- [[pm-as-gap-filler]] - PM是填空岗位：人才栈压缩的角色重构
- [[power-user-pull]] - Power User拉你进未来：先可配置再简化
- [[research-preview]] - Research Preview：用"早期实验"标签降低发布门槛，一周一天推功能
- [[agi-pilled]] - 恰好正确程度的AGI信仰：太乐观忽略痛点，太保守错失窗口
- [[role-convergence]] - 角色融合：工程师、PM、设计师界限消失
- [[agent-matrix]] - Agent矩阵：从单任务到多Agent并行
- [[harness-engineering]] - 脚手架工程：为AI构建工作环境和约束条件，让AI在护栏内奔跑
- [[ai-first-prerequisites]] - AI优先的五大前提：自动化测试、CI/CD、监控、任务管理、系统架构
- [[architect-operator-model]] - 架构师-操作员模型：AI First的极端组织形态，批评AI比写代码更有价值
- [[self-healing-pipeline]] - 自愈流水线：检测-分诊-修复-验证的最小人工干预闭环
- [[builder-reviewer-model]] - Builder-Reviewer模型：AI-Native团队只有两种角色，中间地带消失
- [[ai-piloting]] - AI驾驶能力：机甲战士的基本功，驾驭AI Agent作为协作搭档
- [[ai-native-veto]] - AI-Native一票否决项：6项行为信号触发即淘汰
- [[organizational-self-knowledge]] - 组织自我认知：AI赋能的前提不是AI技术，而是组织能否清晰描述自己
- [[ai-readiness-gap]] - AI准备度鸿沟：清晰公司与混乱公司之间的差距正在扩大
- [[clarity-before-automation]] - 先清晰再自动化：你无法优化一个连自己都没搞懂的东西
- [[general-specialized-architecture]] - 通用编排器+专用工具：做好垂直系统在AGI时代依然有价值
- [[alphafold-breakthrough-conditions]] - AlphaFold式突破三条件：巨大搜索空间+清晰目标+足够数据
- [[jevons-paradox-inference]] - 推理的杰文斯悖论：推理可能永远不免费

### 查看源文件
- [[karpathy-llm-knowledge-management]] - LLM知识管理实践案例
- [[anthropic-cat-wu-product-taste]] - AI产品开发前沿洞察
- [[karpathy-obsidian-rebuild]] - 个人实践：一小时重建Obsidian知识库的体验与认知转变
- [[karpathy-knowledge-workflow-guide]] - 完整知识编译工作流指南：三层目录结构、健康检查、增量编译
- [[ai-agent-comparisons-2026]] - 2026年AI Agent框架深度对比：OpenClaw、Hermes、Claude Cowork等7种方案
- [[openclaw-hermes-architecture]] - OpenClaw与Hermes Agent逐层架构对比：Gateway-first vs Agent-first
- [[anthropic-interpretability]] - Anthropic在AI可解释性方面的系统性工作：从神经元叠加到AI审计的四年研究路径
- [[karpathy-interview-agentic-engineering]] - Karpathy访谈：10x工程师已是常态，真正的Agentic工程师是100x
- [[codex-team-dogfooding]] - OpenAI Codex团队如何用自己的产品构建产品
- [[cat-wu-ai-pm-role]] - Cat Wu深度访谈：AI PM角色重塑、Research Preview、AGI信仰校准
- [[ai-first-strategy-wrong]] - CREAO实践：AI First的真正前提是软件工程基础，脚手架工程取代写代码
- [[ai-native-hiring-guide]] - AI-Native工程师招聘面试官手册：Builder/Reviewer双岗、7模块面试、6项一票否决
- [[companies-not-ready-for-ai]] - Daniel Miessler：大多数公司根本没有为AI做好准备
- [[hassabis-agi-agents-science]] - Demis Hassabis：AGI还缺什么、智能体投入产出比、AlphaFold式突破、爱因斯坦测试
- [[venturini-agent-output-compiler]] - Hugo Venturini：将Agent输出视为编译器输出，用验证流程替代代码审查
- [[venturini-code-never-for-machines]] - Hugo Venturini：代码从来不是为机器写的——直到现在

### 浏览索引
- [[index]] - 所有页面的分类目录

## 工作流程

1. **摄取**：将新素材放入`raw/`，运行`/ingest`
2. **查询**：基于wiki上下文提问，LLM综合回答
3. **维护**：定期运行`/lint`检查知识库健康度
4. **扩展**：使用`/import-readwise`等技能导入外部内容

## 实时状态

- **源文件**：18篇（…+Venturini两篇：Agent输出如编译器输出、代码从来不是为机器写的）
- **概念页**：55个（…+Agent输出验证、Agent原生工具）
- **总页面**：78个（含home、index、log、18源摘要、55概念页）
- **最后更新**：2026-05-05（新增Venturini两篇源文件及2个概念页：Agent输出验证、Agent原生工具）

> 提示：在右侧终端输入`claude`开始与wiki交互，或使用`/ingest`添加更多源文件。
