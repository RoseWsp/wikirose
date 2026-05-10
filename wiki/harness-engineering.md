# 脚手架工程 (Harness Engineering)

**TL;DR** 工程团队的核心工作不再是写代码，而是为AI构建工作环境和约束条件——让AI能做有价值的事，并在出错时有系统兜底。Harness Engineering是围绕AI Coding Agent设计和构建约束机制（Constraints）、反馈回路（Feedback Loops）、工作流控制（Workflow Orchestration）与持续改进循环（Continuous Improvement）的系统工程实践。

## 三次范式跃迁

AI工程实践正经历三个清晰的演化阶段：

1. **Prompt Engineering（2022-2024）** — 关注单次交互优化：Few-shot Learning、Chain-of-Thought、角色设定。核心隐喻是"写好一封邮件"。
2. **Context Engineering（2025）** — 关注"给Agent看什么"：动态构建的上下文窗口应填充哪些文档、对话历史、工具定义。突破：模型表现上限取决于上下文质量，而非prompt措辞。Shopify CEO Tobi Lutke类比为"给邮件附上所有正确的附件"。
3. **Harness Engineering（2026）** — 设计跨越多个会话、多个Agent角色、多个执行阶段的完整系统架构。不再只关注"一次对话"或"一次上下文窗口"。([[harness-engineering-aliyun]])

Harness Engineering的操作性定义（Mitchell Hashimoto）："Every time you discover an agent has made a mistake, you take the time to engineer a solution so that it can never make that mistake again."它不是一次性的prompt优化，而是一个持续演进的系统工程闭环。([[harness-engineering-aliyun]])

## 四种Agent失败模式

Anthropic系统总结了Agent在复杂项目中的四种典型失败模式 ([[harness-engineering-aliyun]]、[[anthropic-effective-harnesses]])：

1. **One-shot Syndrome（试图一步到位）** — Agent拿到复杂需求后倾向于在单上下文窗口内完成全部工作，但进行到一半时上下文已被消耗大半，模型开始出现Hallucination、循环输出、格式错误的Tool Call。上下文窗口的Sweet Spot在40%以下的填充率。
2. **Premature Victory Declaration（过早宣布胜利）** — Agent完成部分工作就宣布任务结束，核心功能尚未实现或验证。
3. **Premature Feature Completion（过早标记功能完成）** — Agent认为功能已实现但未做端到端测试验证，部署后才发现关键路径不通。解法：引入Browser Automation（Puppeteer MCP）自动端到端验证截图。
4. **Cold Start Problem（环境启动困难）** — 多次会话间缺乏持久化记忆，每次新会话需花大量Token重新理解项目结构。

共同根源：Agent缺乏外部结构化约束和反馈机制。核心结论："Agents are incapable of accurately evaluating their own work"——Agent无法准确评估自身产出质量。Harness通过外部化控制系统弥补这一缺陷。

### Context Anxiety（上下文焦虑）

除上述四种外，Anthropic Labs还发现一种模式：模型对上下文窗口消耗产生焦虑，在接近其认为的上下文限制时过早收尾。Context Reset（清空上下文+结构化交接）比Compaction更能解决此问题。Opus 4.6大大消除了Context Anxiety行为，使得Anthropic后续实验可以放弃Context Reset机制。([[anthropic-harness-design]])

## 四根支柱

综合Anthropic和OpenAI的经验，Harness Engineering可归纳为四根支柱 ([[harness-engineering-aliyan]]、[[openai-harness-engineering]])：

### 支柱一：上下文架构（Context Architecture）

Agent应当恰好获得当前任务所需的上下文——不多不少。OpenAI团队早期将AGENTS.md写成了百科全书，结果"所有内容都重要=没有内容重要"。后来改为~100行，作为Index & Map指向深层文档。上下文分层加载（Anthropic的三层模型）：

- **L1 会话常驻层**：Agent定义文件+核心Rules，避免窗口填充率超过40%
- **L2 阶段触发层**：每个开发阶段只加载当前需要的Skill
- **L3 按需查询层**：Wiki知识库不主动加载，Agent按需查阅

OpenAI的代码仓库知识库方案 ([[openai-harness-engineering]])：
```
AGENTS.md          # ~100行，作为地图和目录
ARCHITECTURE.md    # 域和包分层的顶层地图
docs/
├── design-docs/   # 设计文档（含验证状态）
├── exec-plans/    # 执行计划（活跃/已完成/技术债）
├── product-specs/ # 产品规范
└── references/    # 参考文档（llms.txt格式）
```

核心理念：**渐进式披露（Progressive Disclosure）**——Agent从小而稳定的切入点开始，被指导下一步该去哪里查看，而不是一开始就被淹没。

### 支柱二：Agent专业化（Agent Specialization）

拥有受限工具集（Constrained Toolset）的专业Agent优于拥有全部权限的通用Agent。Anthropic在其Harness设计中分离三种角色：Planner负责规划、Generator负责实现、Evaluator负责验证。(Anthropic的核心发现："将做事的Agent和评判的Agent分开，是一个强有力的杠杆。")

**GAN启发式三Agent架构** ([[anthropic-harness-design]])：
- **Planner**：将1-4句话的prompt扩展为完整产品spec（包含16+ feature、跨越10个sprint）
- **Generator**：按sprint增量实现，每个sprint与Evaluator协商"done"的定义（Sprint Contract）
- **Evaluator**：用Playwright MCP点进页面做QA，按四维标准打分

**Sprint Contract机制**：Generator和Evaluator在写代码前协商"done"的定义——Generator提出要构建什么以及如何验证成功，Evaluator审查提案确保方向正确，两者迭代直到达成一致。沟通通过文件进行（一个Agent写文件，另一个读文件回应）。

### 支柱三：持久化记忆（Persistent Memory）

进度持久化在文件系统上，而非上下文窗口中。Anthropic的标准化启动序列 ([[anthropic-effective-harnesses]])：

```
pwd → 读git log和progress文件 → 读feature list → 选最高优先级未完成任务 → 启动dev server → 验证基础功能 → 开始新feature
```

Feature List用JSON格式（模型更不易误改），每个feature标记passes: false/true。Agent只允许修改passes状态，禁止删除或修改测试项。

### 支柱四：结构化执行（Structured Execution）

永远不让Agent在未经审查和批准书面计划之前写代码。理想执行流：理解→规划→执行→验证，每个阶段间有明确质量门禁（Quality Gates）。

**10阶段开发流程** ([[harness-engineering-aliyun]])：

```
需求分析 → 需求评审 → 编码实现 → 编码评审 → 单元测试编写 → 单元测试评审 → 代码推送 → CI验证 → 部署验证 → 用户确认
```

每个阶段三要素：触发条件（Entry Criteria）、Skill加载（Skill Injection）、质量门禁（Quality Gate）。评审设循环上限（需求评审最多3轮，编码/测试评审最多2轮），防无限自我修改循环。嵌入5个Human-in-the-Loop确认点。

**质量门禁必须可程序化验证**："If it can't be mechanically enforced, the agent will drift." — OpenAI百万行代码项目核心经验。如"检查CI是否通过"应改为三个可验证条件：status == SUCCESS && total_tests > 0 && passed == total。

## 四要素实战架构

基于四根支柱的落地设计 ([[harness-engineering-aliyun]])：

| 要素 | 作用 | 内容 |
|------|------|------|
| 规则体系（Rules） | 告诉Agent"标准是什么" | 工程结构约束、编码规范、分层架构约定（不变约束） |
| 技能体系（Skills） | 告诉Agent"应该怎么做" | 需求分析SOP、分层编码规范、评审检查清单、测试方法 |
| 知识库（Wiki） | 告诉Agent"系统是什么样的" | 链路梳理、数据模型、核心业务流程 |
| 变更管理（Changes） | 记录Agent"做了什么" | 每个需求从分析到部署的全过程文档（Audit Trail） |

物理载体 `.harness/` 目录结构 ([[harness-engineering-aliyun]])：
```
.harness/
├── agents/        # Agent角色定义（~400行，承担Index & Map职责）
├── rules/         # 规则体系
├── skills/        # 技能体系（9个Skill）
├── changes/       # 变更管理目录（每个需求独立子目录）
├── mcp/           # 外部工具集成配置
```

## 熵的累积与垃圾回收

OpenAI在百万行代码实践中发现的重要概念 ([[openai-harness-engineering]])：

Agent写代码时会模仿代码库中已有的Pattern——包括那些Suboptimal的Pattern。每次Agent生成代码，都可能引入少量的风格不一致、冗余逻辑或次优实现。单次无关痛痒，累积起来却会让代码库逐渐腐化（Code Rot）。

解法：**"Golden Principles"编码化 + 后台回收Agent**。将主观品味编码为机械规则（如"优先使用共享工具包而非手写辅助函数"、"结构化日志格式统一"），后台Agent自动扫描偏差并发起修复PR。功能上类似于垃圾回收——持续还小额技术债，避免积累后一次痛苦解决。

## 关键经验

1. **Harness本身需要Dry Run** — 在拿真实需求之前，用虚拟需求完整走一遍全流程，发现CI门禁只检查状态码忽略测试用例数为0、评审报告不生成文件等缺陷 ([[harness-engineering-aliyun]])
2. **分离执行与评判是关键杠杆** — Agent-to-Agent Review可拦截编码Agent遗漏的渠道判断逻辑（潜在线上故障），还可检测到Agent试图跳过评审阶段 ([[harness-engineering-aliyun]]、[[anthropic-harness-design]])
3. **流程一致性优先于流程效率** — 好的流程不给简单任务增加显著负担，保持一致性防止"小改动大事故" ([[harness-engineering-aliyun]])
4. **规范每一行对应一个历史失败案例** — 当你觉得某条规则多余时，那往往因为它背后有一个真实踩过的坑 ([[harness-engineering-aliyun]])
5. **"Waiting is expensive, fixing is cheap"** — 在智能体吞吐量远超人类注意力的系统中，纠错成本低而等待成本高 ([[openai-harness-engineering]])
6. **规范的每一行都对应一个历史失败案例** — Mitchell Hashimoto定义的核心循环：每发现一个错误，就工程化地消除它再次发生的可能性 ([[harness-engineering-aliyun]])

## 效果数据

| 维度 | 无Harness | 有Harness |
|------|-----------|-----------|
| AI代码率 | 24.86% | 90.54% |
| 需求理解偏差 | Agent经常误解需求意图 | 通过spec+确认点在评审前拦截 |
| 过程可追溯性 | 无记录 | 完整变更文档链，任何人随时回溯 |
| 流程一致性 | 因人而异 | 10阶段流程一致执行 |

Anthropic的全栈三Agent架构效果 ([[anthropic-harness-design]])：4小时/每轮约$124.70（3轮Build-QA循环），输出质量远超无Harness的Solo Agent（20分钟/$9）。

## 与相关概念的关系

- [[agentic-engineering]] — 脚手架工程是Agentic Engineering的具体实践形态
- [[ai-first-prerequisites]] — 脚手架工程的五大技术前提
- [[self-healing-pipeline]] — 自愈流水线与脚手架工程互补：后者搭护栏，前者建闭环
- [[agent-output-verification]] — 脚手架的上游约束，为Agent构建可验证的执行规格
- [[agent-native-tooling]] — 为Agent构建原生工作介质，与脚手架的约束环境互补
- [[anti-rationalization]] — 防Agent自我说服绕过约束，是脚手架的认知层
- [[scope-discipline]] — 脚手架划定行动范围，范围纪律是意志层
- [[workflow-over-prose]] — 脚手架工程是"流程优先于散文"在系统层面的体现
- [[agent-immune-system]] — 外部护栏（脚手架）vs 内部认知防御（免疫系统），同一思路的两个方向
- [[agent-isolation]] — 多个agent并行时脚手架必须包含环境隔离
- [[recursive-self-improvement]] — 递归自改进拷问脚手架极限：当被约束系统比约束者更聪明时
- [[org-process-gap]] — 脚手架工程的组织层面对应
- [[bounded-rationality]] — 脚手架工程本质上是给AI划定有限理性的边界
- [[generator-evaluator-loop]] — GAN启发式多Agent架构的核心模式

## 组织层面的脚手架

脚手架的发挥作用前提不只是技术基础设施，而是组织本身已经理清了"要做什么"和"怎么运转"。混乱公司的问题不是缺CI/CD——而是连自己的工作流都描述不出来。工程层面的"先搭脚手架再让AI跑"和组织层面的"先清晰目标再让AI执行"是同一枚硬币的两面 ([[companies-not-ready-for-ai]])。
