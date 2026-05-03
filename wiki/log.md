# Log

## [2026-05-03 23:30] ingest | 几乎没人答对一个问题：AI 产品经理到底应该干什么
- 源文件：[[cat-wu-ai-pm-role]]
- 创建概念页：
  - [[research-preview]]（Research Preview机制：用"早期实验"标签降低发布门槛）
  - [[agi-pilled]]（恰好正确程度的AGI信仰：太乐观忽略痛点，太保守错失窗口）
  - [[role-convergence]]（角色融合：工程师、PM、设计师界限消失）
  - [[agent-matrix]]（Agent矩阵：从单任务到多Agent并行的进化路线）
- 更新现有概念页：
  - [[product-taste]]：添加AGI信仰校准、角色融合、research preview关联
  - [[action-based-ai]]：添加Agent矩阵、research preview关联
  - [[pm-as-gap-filler]]：添加角色融合、AGI信仰关联
  - [[minimal-product-specs]]：添加research preview关联
  - [[pirate-ship-team]]：添加角色融合关联
  - [[power-user-pull]]：添加AGI信仰关联
  - [[agentic-engineering]]：添加Agent矩阵、角色融合关联
  - [[dual-horizon-planning]]：添加AGI信仰、research preview关联
  - [[anthropic-cat-wu-product-taste]]：添加4个新概念页链接和更详细源文件引用
- 交叉链接：
  - [[product-taste]] → [[agi-pilled]]、[[role-convergence]]、[[research-preview]]
  - [[action-based-ai]] → [[agent-matrix]]、[[research-preview]]
  - [[pm-as-gap-filler]] → [[role-convergence]]、[[agi-pilled]]
  - [[minimal-product-specs]] → [[research-preview]]
  - [[pirate-ship-team]] → [[role-convergence]]
  - [[power-user-pull]] → [[agi-pilled]]
  - [[agentic-engineering]] → [[agent-matrix]]、[[role-convergence]]
  - [[dual-horizon-planning]] → [[agi-pilled]]、[[research-preview]]
  - [[anthropic-cat-wu-product-taste]] → [[research-preview]]、[[agi-pilled]]、[[role-convergence]]、[[agent-matrix]]
- 索引更新：[[index]]添加1源摘要+4概念页
- 门户更新：[[home]]添加AI PM角色重塑主题、概念图扩展、探索路径更新、状态更新

## [2026-05-03 22:30] lint | Wiki健康检查
- 修复3个死端页面（无出站wikilink的源文件）：
  - [[openclaw-hermes-architecture]]：添加6条出站链接
  - [[anthropic-interpretability]]：添加5条出站链接
  - [[ai-agent-comparisons-2026]]：添加6条出站链接
- 修复1个破损链接：home.md中`[[claude-code]]`→移除（无对应页面）
- 添加缺失交叉链接：
  - [[software-3.0]] → [[action-based-ai]]
  - [[agentic-engineering]] → [[knowledge-engineering]]
  - [[jagged-intelligence]] → [[mechanistic-interpretability]]
  - [[mechanistic-interpretability]] → [[jagged-intelligence]]
  - [[anthropic-cat-wu-product-taste]] → [[agentic-engineering]], [[dogfooding-as-method]], [[ai-agent-frameworks]]
- 去重：mechanistic-interpretability.md中重复的交叉链接段合并
- 无孤儿页面、无矛盾、home.md内容最新

## [2026-05-03 20:00] ingest | Codex团队如何用自己的产品构建产品
- 源文件：[[codex-team-dogfooding]]
- 创建概念页：
  - [[dogfooding-as-method]]（用产品建产品：AI团队把dogfooding从质量保证变为认知工具）
  - [[minimal-product-specs]]（极简产品规格：整个产品spec只有10个要点）
  - [[dual-horizon-planning]]（双极规划：只做8周近期和远期方向感，永远不做中期路线图）
  - [[pirate-ship-team]]（海盗船式团队：50-100人长期只有1个PM）
  - [[pm-as-gap-filler]]（PM是填空岗位：人才栈压缩下PM从领导者变为填补空缺者）
  - [[power-user-pull]]（Power User拉你进未来：先做可配置性再做简化）
- 交叉链接：
  - [[agentic-engineering]] → [[dogfooding-as-method]]、[[minimal-product-specs]]、[[pirate-ship-team]]
  - [[vibe-coding]] → [[dogfooding-as-method]]、[[pm-as-gap-filler]]
  - [[product-taste]] → [[dogfooding-as-method]]、[[minimal-product-specs]]、[[power-user-pull]]
  - [[action-based-ai]] → [[dogfooding-as-method]]、[[power-user-pull]]
  - [[software-3.0]] → [[dogfooding-as-method]]、[[dual-horizon-planning]]
- 索引更新：[[index]]添加1源摘要+6概念页
- 门户更新：[[home]]添加AI团队极简运作主题、概念图扩展、探索路径更新、状态更新

## [2026-05-03 19:00] ingest | OpenClaw与Hermes Agent架构深度对比
- 源文件：[[openclaw-hermes-architecture]]
- 创建概念页：[[agent-architecture-patterns]]（Gateway-first vs Agent-first两种架构模式）
- 深度更新现有概念页：
  - [[ai-agent-frameworks]]：用六层对比表（API成本、记忆、执行环境、Session持久化、安全、进化）替换原有简略描述，新增Session持久化/执行环境/多Agent策略对比表
  - [[agentic-engineering]]：添加[[agent-architecture-patterns]]相关概念链接
  - [[action-based-ai]]：添加[[agent-architecture-patterns]]相关概念链接
- 交叉链接：
  - [[ai-agent-frameworks]] → [[agent-architecture-patterns]]、[[openclaw-hermes-architecture]]
  - [[agentic-engineering]] → [[agent-architecture-patterns]]
  - [[action-based-ai]] → [[agent-architecture-patterns]]
  - [[agent-architecture-patterns]] → [[ai-agent-frameworks]]、[[agentic-engineering]]、[[action-based-ai]]、[[product-taste]]、[[openclaw-hermes-architecture]]
- 索引更新：[[index]]添加1源摘要+1概念页
- 门户更新：[[home]]添加架构深度对比链接和概念页，更新实时状态

## [2026-05-03 18:30] digest | 深度整合Karpathy访谈：10x到100x工程师的Agentic Engineering演进
- 源文件：[[karpathy-interview-agentic-engineering]]
- 深度更新现有概念页：
  - [[software-3.0]]：补充MenuGen案例详细分析、商业判断洞察
  - [[jagged-intelligence]]：添加"幽灵vs动物"理解框架、国际象棋案例引用
  - [[agentic-engineering]]：扩展10x到100x工程师分析、效率提升潜力、能力要求转变
  - [[product-taste]]：添加"智能廉价化后的理解溢价"部分，引用Karpathy关键洞察
  - [[action-based-ai]]：添加Agent-first基础设施需求分析
  - [[knowledge-engineering]]：已包含源文件引用，确认交叉链接
- 关键洞察整合：
  - MenuGen案例揭示模型原生能力吞没中间应用层的商业影响
  - "智能变便宜后，最贵的是理解" - 思考可外包，理解必须内化
  - "幽灵vs动物"框架重新定义LLM本质理解
  - Agentic Engineering实现从10x到100x工程师的效率飞跃
  - Agent-first基础设施需求：从人类操作界面到Agent调用接口
- 交叉链接验证：所有概念页均有充分入站链接（5-11个/页面），满足wiki集成要求

## [2026-05-03 18:00] ingest | Karpathy访谈：10x工程师已是常态，真正的Agentic工程师是100x
- 源文件：[[karpathy-interview-agentic-engineering]]
- 创建概念页：[[vibe-coding]]、[[agentic-engineering]]、[[software-3.0]]、[[jagged-intelligence]]、[[neural-computer]]
- 更新现有概念页：
  - [[product-taste]]：添加AI-native工程的新要求，链接到[[vibe-coding]]和[[agentic-engineering]]
  - [[action-based-ai]]：添加[[agentic-engineering]]作为相关概念
  - [[ai-agent-frameworks]]：添加[[agentic-engineering]]作为相关概念
  - [[knowledge-engineering]]：添加源文件引用
- 交叉链接：新概念页与所有相关概念页双向链接
- 反向链接：更新4个现有概念页的相关概念部分，添加指向新页面的[[wikilinks]]
- 索引更新：[[index]]添加1源摘要+5概念页
- 门户更新：[[home]]添加新兴主题"AI-native工程范式"，更新实时状态和查看源文件列表

## [2026-05-03 17:30] digest | 深度整合4个关键源摘要页面
- 源文件：[[karpathy-obsidian-rebuild]]、[[karpathy-knowledge-workflow-guide]]、[[ai-agent-comparisons-2026]]、[[anthropic-interpretability]]
- 深度整合检查：
  - 确认所有4个源摘要页面已有足够入站链接（7-17个/页面）
  - 验证所有相关概念页面包含正确的源引用标注
  - 检查交叉引用网络完整性，确保双向链接
  - 确认[[index]]完整收录所有页面
- 整合质量验证：
  - [[karpathy-obsidian-rebuild]]：在[[obsidian-rebuild-experience]]、[[knowledge-compounding]]等10+页面中被引用
  - [[karpathy-knowledge-workflow-guide]]：在[[knowledge-compilation-workflow]]、[[knowledge-health-check]]等8+页面中被引用
  - [[ai-agent-comparisons-2026]]：在[[ai-agent-frameworks]]、[[action-based-ai]]等7+页面中被引用
  - [[anthropic-interpretability]]：在[[mechanistic-interpretability]]、[[product-taste]]等6+页面中被引用
- 网络健康度：所有源摘要页面有至少6个入站链接，满足wiki集成要求

## [2026-05-03 17:00] ingest | Anthropic AI可解释性研究
- 源文件：[[anthropic-interpretability]]
- 创建概念页：[[mechanistic-interpretability]]
- 更新现有概念页：
  - [[ai-agent-frameworks]]：添加可解释性需求增长趋势，链接到[[mechanistic-interpretability]]
  - [[action-based-ai]]：添加透明度与可审计性需求部分，链接到[[mechanistic-interpretability]]
  - [[product-taste]]：添加安全与可解释性投资部分，链接到[[mechanistic-interpretability]]
- 交叉链接：新概念页与所有相关概念页双向链接
- 反向链接：更新3个现有概念页的相关概念部分，添加指向新页面的[[wikilinks]]
- 索引更新：[[index]]添加1源摘要+1概念页
- 门户更新：[[home]]添加新兴主题部分，更新实时状态和探索路径

## [2026-05-03 16:45] ingest | AI Agent框架对比与分化分析
- 源文件：[[ai-agent-comparisons-2026]]
- 创建概念页：[[ai-agent-frameworks]]
- 更新现有概念页：
  - [[action-based-ai]]：添加AI Agent框架选择部分，链接到[[ai-agent-frameworks]]
  - [[llm-knowledge-management]]：在相关概念部分添加[[ai-agent-frameworks]]链接
  - [[product-taste]]：添加AI Agent框架选型作为产品品味案例
- 交叉链接：新概念页与所有相关概念页双向链接
- 反向链接：更新3个现有概念页的相关概念部分，添加指向新页面的[[wikilinks]]
- 索引更新：[[index]]添加1源摘要+1概念页
- 门户更新：[[home]]添加新兴主题部分，更新实时状态和探索路径

## [2026-05-03 16:00] ingest | 完整知识编译工作流指南
- 源文件：[[karpathy-knowledge-workflow-guide]]
- 创建概念页：[[knowledge-health-check]]、[[incremental-compilation]]、[[knowledge-engineering]]
- 更新现有概念页：
  - [[knowledge-compilation-workflow]]：添加详细工作流指南引用、健康检查、增量编译
  - [[llm-knowledge-management]]：补充详细工作流指南、工程化原则
  - [[compiled-knowledge-base]]：添加工作流指南引用
- 交叉链接：新概念页与所有相关概念页双向链接
- 反向链接：更新7个现有概念页的相关概念部分，添加指向新页面的[[wikilinks]]
- 索引更新：[[index]]添加1源摘要+3概念页
- 门户更新：[[home]]更新实时状态，添加新源文件和进阶概念

## [2026-05-03 15:30] ingest | 个人实践：用Karpathy方法重建Obsidian知识库
- 源文件：[[karpathy-obsidian-rebuild]]
- 创建概念页：[[obsidian-rebuild-experience]]、[[knowledge-compilation-workflow]]
- 更新现有概念页：
  - [[llm-knowledge-management]]：添加个人实践验证、认知转变关键点
  - [[compiled-knowledge-base]]：补充编译效果、交叉节点发现
  - [[knowledge-compounding]]：扩展复利循环体验、实践意义
- 交叉链接：新页面与所有相关概念页双向链接
- 反向链接：现有概念页添加指向新页面的[[wikilinks]]

## [2026-05-03 15:00] digest | Anthropic产品负责人Cat Wu访谈深度整合
- 源文件：[[anthropic-cat-wu-product-taste]]
- 更新现有页面：
  - [[llm-knowledge-management]]：添加Claude Code工具细节、发布速度、产品策略
  - [[knowledge-compounding]]：添加100%自动化标准、避坑指南
  - [[product-taste]]：细化品味构建机制、Evals取代PRD
  - [[action-based-ai]]：补充历史划分、具体案例
- 新增交叉引用：所有概念页相互引用，形成知识网络
- 反向链接：确保每个新页面有至少2个入站链接

## [2026-05-03 14:55] digest | Andrej Karpathy的LLM知识管理方法深度整合
- 源文件：[[karpathy-llm-knowledge-management]]
- 更新现有页面：
  - [[llm-knowledge-management]]：添加具体实践效果、小规模高效交互
  - [[compiled-knowledge-base]]：补充认知转变、gap填补机制
  - [[knowledge-compounding]]：扩展开放验证机制
- 创建新概念页：
  - [[obsidian-optimization]]：Obsidian从收藏夹到编译型知识库的优化
  - [[rag-alternatives]]：小规模知识库的简单索引方案
- 更新索引：[[index]]添加2个新概念页
- 交叉链接：新页面与现有概念页全面互链

## [2026-05-03 14:30] ingest | Andrej Karpathy的LLM知识管理方法
- 源文件：`raw/clips/Andrej Karpathy 的 LLM 知识管理方法显著提升 Obsidian 知识库效率.md`
- 创建源摘要页：[[karpathy-llm-knowledge-management]]
- 创建概念页：[[llm-knowledge-management]]、[[compiled-knowledge-base]]、[[knowledge-compounding]]
- 更新索引：[[index]] 添加5个页面分类
- 更新门户：[[home]] 重写为当前wiki状态概览
- 交叉链接：所有新页面相互链接，并与现有框架集成

## [2026-05-03 14:45] ingest | Anthropic产品负责人Cat Wu访谈
- 源文件：`raw/clips/​​Anthropic 产品负责人 Cat Wu：代码正变得廉价，"产品品味"将成为未来核心壁垒.md`
- 创建源摘要页：[[anthropic-cat-wu-product-taste]]
- 创建概念页：[[product-taste]]、[[action-based-ai]]
- 更新现有概念页：[[llm-knowledge-management]]添加Claude Code工具关联
- 更新索引：[[index]] 添加2个源摘要+2个概念页
- 更新门户：[[home]] 扩展概念网络，添加AI产品开发主题
- 交叉链接：新页面与[[llm-knowledge-management]]、[[compiled-knowledge-base]]、[[knowledge-compounding]]相互链接
- 反向链接：现有页面添加指向新页面的[[wikilinks]]
