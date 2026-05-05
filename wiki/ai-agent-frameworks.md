# AI Agent框架

2026年AI Agent框架进入结构分化阶段，形成OpenClaw、Hermes、Claude Cowork三足鼎立格局，分别代表连接广度、认知深度和易用性三种不同的设计哲学。

## 核心框架对比

### OpenClaw：连接广度优先
- **GitHub星标**：361,000+（2026年4月）
- **核心哲学**：消息网关架构，连接一切平台
- **优势**：最大社区、50+消息渠道全覆盖、13,000+社区技能
- **安全模型**：应用程序级检查，完全本地访问，无内置批准系统
- **最佳适用**：需要多平台集成和团队协作的场景

### Hermes Agent：认知深度优先
- **GitHub星标**：73,800+（2026年4月）
- **核心哲学**：闭环学习循环，Agent随使用变得更聪明
- **优势**：四层记忆系统、自我进化能力、轻量高效
- **安全模型**：五个沙箱后端（本地、Docker、SSH、Singularity、Modal）+ [[agent-immune-system|适应性免疫系统]]（利用复盘机制实现自主防御）
- **最佳适用**：需要长期自主任务和自我学习的场景

### Claude Cowork：易用性优先
- **核心哲学**：桌面端AI协作，让非程序员也能使用
- **优势**：零代码门槛、图形界面友好、虚拟机隔离安全
- **安全模型**：虚拟机隔离环境，仅访问用户授权文件夹
- **最佳适用**：非技术知识工作者、办公自动化

## 关键技术维度

### 1. 记忆系统
**这是框架间差距最大的技术维度**（[[ai-agent-comparisons-2026]]）：

#### Hermes的四层记忆系统：
1. **会话记忆**：当前对话上下文
2. **知识记忆**：MEMORY.md——用户明确告知的事实（时区、语言、项目约定），session开始时快照冻结进system prompt
3. **用户偏好记忆**：USER.md——"你是谁"，风格、偏好、雷区，可接外部提供方（Honcho、Mem0、Hindsight）
4. **跨会话上下文记忆**：Skills——完成复杂任务后写下的文档，扫描文件系统检索，下次使用时继续打磨

#### OpenClaw的记忆策略：
- 会话级为主，持久记忆较弱
- SOUL.md（人格与行为规则）+ MEMORY.md（事实与偏好）
- 夜间Dreaming系统：三阶段（Light/REM/Deep），六因素加权打分，仅Deep阶段写入MEMORY.md
- 依赖Skill文件手动保存，每天额外消耗API调用

#### Claude Cowork的记忆架构：
- 工作手册+日记（显式记忆）
- 向量数据库（隐式记忆）
- 项目专属记忆

### 2. 自我进化能力
**新一代框架的核心竞争力**：

#### Hermes的GEPA自我进化引擎：
- 类反向传播优化prompt
- 仅需10次评估即可收敛
- 从失败任务中总结经验，主动避开坑

#### OpenClaw的进化策略：
- 无原生自动进化能力
- 依赖社区贡献和版本升级
- 需用户手动更新Skill文件

#### Claude Cowork的自适应机制：
- 自适应思维机制
- 根据任务复杂度调整推理强度
- 基于用户反馈和使用数据优化输出

### 3. 安全模型
**从应用级检查到操作系统级隔离的演进**：

Agent框架还需要考虑[[sensory-gap|感知缺失]]带来的隐性风险：AI天生没有时间感等基本感知维度，当框架赋予Agent新感知能力（如定时任务、实时数据流）时，Agent会[[compulsive-capability-use|强迫性地过度使用]]新能力 ([[claude-discovers-clock]])。这意味着框架的安全模型不仅要防止恶意使用，还要防止AI对自身新能力的失控性使用——Hermes的IterationBudget上限和工具白名单机制恰好为此提供了天然约束。

| 安全级别 | 代表框架 | 技术实现 | 适用场景 |
|----------|----------|----------|----------|
| **应用级** | OpenClaw | 应用程序权限检查 | 开发环境、完全信任场景 |
| **容器级** | nanoClaw | Docker/Apple容器隔离 | 安全敏感的个人使用 |
| **虚拟机级** | Sai by Simular | 云虚拟机隔离 | 企业环境、非技术用户 |
| **多后端** | Hermes Agent | 5种沙箱后端 + [[agent-immune-system|免疫系统]] | 灵活部署需求 |

### 4. 部署与执行模式

#### 持久运行 vs 按需启动
- **Hermes**：后台持续运行、定时Cron、子Agent并行
- **OpenClaw**：一次性任务、无状态为主
- **Claude Cowork**：桌面应用持久运行，自主执行复杂任务

#### 资源需求对比
- **轻量级**：Hermes（5美元服务器即可运行）
- **中等**：OpenClaw（配置复杂时占用较高）
- **桌面级**：Claude Cowork（虚拟机隔离，资源占用适中）

## 设计哲学分歧

### 架构差异的本质
两种根本不同的设计路径——详见[[agent-architecture-patterns]]：

#### OpenClaw路径：Gateway-first（身体+大脑）
- **核心**：Gateway是承重墙，AI运行时（Pi）是嵌入式子进程，只是编排系统的一个组件
- **四层架构**：Channels → Gateway → Agent Runtime → 记忆层
- **优势**：快速扩展生态，按接口规范接入即自动获得session路由和事件排队
- **代价**：prompt每轮重建（放弃缓存命中）、记忆依赖夜间Dreaming进程（额外API调用）、复杂度外溢

#### Hermes路径：Agent-first（大脑即全部）
- **核心**：AIAgent是主进程，消息/工具/记忆全挂在Agent身上，Gateway只是薄适配层
- **五层架构**：对话循环 → Prompt系统 → 工具系统 → 记忆系统 → 学习循环
- **优势**：prompt全生命周期缓存（API开销递减）、记忆维护"免费"、skill自进化让成本收敛
- **代价**：对模型规模要求更高，学习曲线陡峭

### 技能系统的不同理念

#### 公共教材模型（OpenClaw）：
- 技能由他人编写、为通用场景服务
- YAML frontmatter的Markdown，发布到ClawHub
- 庞大的技能市场（13,000+）
- 安装后基本不变，不会随用户使用自动进化
- 一个SKILL.md写上技能名、触发条件、所需权限，然后才是具体说明——结构化但静态

#### 私人工作笔记模型（Hermes）：
- 技能在任务完成后由Agent自行创建，询问用户是否保存
- 写入`~/.hermes/skills/`，下次找到并执行，继续精炼
- 闭环：做事→反思→生成skill→持久化→回忆→精炼
- 同类任务工具调用次数从20+压缩到8-10次，API成本可测量下降
- 用户当然也可以手写skill，但系统本身被设计成允许agent自己创建和改进——这是架构级别的选择 ([[openclaw-hermes-architecture]])

### Session持久化与检索

| | OpenClaw | Hermes |
|---|---|---|
| 存储 | JSON/JSONL，原子写入 | SQLite WAL模式，FTS5全文检索 |
| 检索 | LanceDB向量检索（语义强，关键词弱） | FTS5关键词检索+总结（无需向量数据库） |
| Schema | 无迁移机制 | 第6版，带迁移 |
| 分叉 | 不支持 | `/branch`命令，树状结构（parent_session_id） |

### 执行环境

| | OpenClaw | Hermes |
|---|---|---|
| 选项 | 本机 / Docker（二选一） | 本机 / Docker / SSH / Singularity(HPC) / Modal(serverless) / Daytona（六选一） |
| 并行 | 基本并行 | 读取始终并行，写入并行（除非碰同一文件） |

### 多Agent策略

| | OpenClaw | Hermes |
|---|---|---|
| 方式 | Gateway supervisor tree | 每个子任务新建AIAgent |
| 工具 | 全部可用 | 只能用父agent已有工具，禁用delegation/clarify/memory/code_execution |
| 深度 | 可配置 | 默认最大2 |
| 预算 | 无上限 | 独立IterationBudget上限50 |
| 理念 | 灵活性 | 护栏 |

## 2026年市场格局

### 三层结构逐渐成型
1. **OpenClaw**：面向普通用户的多渠道Agent平台（"AI Agent的Android"）
2. **Hermes**：面向专业开发者的Agent基础设施
3. **Claude Cowork**：面向安全敏感场景的封闭生态

### 组合使用成为最佳实践
许多开发者采用混合策略：
- **OpenClaw**负责多渠道接入和任务分发
- **Hermes**负责复杂任务执行和自我优化
- **Claude Cowork**负责办公文档处理和专业输出

## 未来趋势

### 1. 从单点爆款到结构分化
Agent框架进入长期结构分化阶段，不同定位满足不同用户需求。

### 2. 自我进化成为标配
静态Agent将逐渐被动态学习型Agent取代，进化能力从差异化优势变为基本要求。

### 3. 安全与隐私关注度提升
容器隔离和本地存储成为企业选型关键因素，数据主权意识增强。

### 4. 模型解耦趋势明显
避免单一模型依赖，支持多模型切换成为框架标配。

### 5. 可解释性需求增长
随着AI Agent在关键决策中扮演更重要的角色，对模型决策过程的透明度和可审计性要求提高，[[mechanistic-interpretability]]研究将成为框架选型的重要考量。Anthropic等公司在机制可解释性上的进展为Agent安全审计提供了基础工具链。

## 选型建议

### 按技术栈选择
- **Python开发者/研究人员**：Hermes Agent（Python生态友好）
- **JavaScript/TypeScript开发者**：OpenClaw（Node.js生态）
- **非技术用户**：Claude Cowork（零代码门槛）

### 按使用场景选择
- **专注编程开发**：OpenClaw（IDE集成体验更好）
- **运维自动化**：Hermes Agent（后台持续运行 + 定时任务）
- **办公自动化**：Claude Cowork（专注办公场景）
- **个人全能助手**：Hermes Agent（多场景覆盖，自我进化）
- **企业数据合规**：Hermes Agent（完全自托管，数据可控）

### 按团队规模选择
- **个人使用**：根据技术偏好选择
- **团队协作**：OpenClaw（消息网关适合团队统一入口）
- **企业部署**：根据安全需求和集成复杂度选择

## 与相关概念的关系

### [[action-based-ai]]
AI Agent框架是行动派AI的技术实现基础，将自动化智能体从概念变为可部署的系统。

### [[agentic-engineering]]
大规模部署AI Agent需要[[agentic-engineering]]的工程纪律，确保在利用Agent加速的同时，不牺牲系统的质量、安全和可维护性标准。

### [[llm-knowledge-management]]
Agent框架可以集成到知识管理流程中，实现从知识整理到知识应用的自动化闭环。

### [[knowledge-compounding]]
智能体的执行结果可以自动写回知识库，形成知识复利的自动化增强循环。

### [[product-taste]]
框架选择反映了产品品味：在代码廉价化时代，判断"应该构建什么"的能力延伸到基础设施选型。

### [[mechanistic-interpretability]]
随着AI Agent承担更多关键决策，对模型决策过程的透明度和可审计性需求增长，机制可解释性研究成为Agent安全的重要保障。

### [[agent-immune-system]]
Hermes的复盘机制（`skill_manage` + 记忆写入）为免疫系统提供了载体——玄武实验室发现，仅需~100 token的提示词追加，就能利用Agent自带的Review机制实现适应性安全防御。这意味着Agent-first架构的安全模型不仅限于沙箱隔离和工具白名单，还可以通过激活Agent自身认知能力实现"免疫"([[xuanwu-hermes-rce-immune-system]])。

### [[multi-step-agent-attack]]
Agent框架的顺从性偏差使它们特别容易受到多步社交工程攻击——每步伪装成正常操作，但整体构成完整的后渗透攻击链。玄武实验室的实验表明，Hermes逐条执行了四步攻击（建立监听器→增加执行能力→内网侦察→凭据探测），直到Review机制触发才识别为攻击。这揭示了框架安全模型的一个盲区：单步检查防不住这类攻击，必须看"链"而非"点"。([[xuanwu-hermes-rce-immune-system]])

### [[sensory-gap]]与[[compulsive-capability-use]]
框架设计必须考虑AI的感知缺失：Agent获得新感知维度后不会"负责任地"使用，而是全力以赴。框架的约束机制（预算、白名单、权限隔离）是应对这种强迫性使用的第一道防线 ([[claude-discovers-clock]])。

### [[agent-architecture-patterns]]
Gateway-first与Agent-first是两种根本不同的架构模式，决定了系统后续一切如何运作。本文的分类和选型建议都建立在理解这一结构性分歧的基础之上。

---
*基于[[ai-agent-comparisons-2026]]和[[openclaw-hermes-architecture]]的综合分析。*