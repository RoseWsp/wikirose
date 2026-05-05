# Log

## [2026-05-05 11:30] ingest | Treat Agent Output Like Compiler Output + Code Was Never for Machines — Until Now
- 源文件：[[venturini-agent-output-compiler]]、[[venturini-code-never-for-machines]]
- 创建源摘要页：
  - [[venturini-agent-output-compiler]]（Hugo Venturini：将Agent输出视为编译器输出，用验证流程替代代码审查）
  - [[venturini-code-never-for-machines]]（Hugo Venturini：代码从来不是为机器写的——直到现在，工具应从人类可读转向Agent原生）
- 创建概念页：
  - [[agent-output-verification]]（Agent输出验证：用验证流程替代代码审查，信任流程而非制品）
  - [[agent-native-tooling]]（Agent原生工具：为Agent而非人类优化的工具与语言，可读性时代的终结）
- 交叉链接更新：
  - [[harness-engineering]]：添加agent-output-verification、agent-native-tooling关联
  - [[self-healing-pipeline]]：添加agent-output-verification关联
  - [[agentic-engineering]]：添加agent-output-verification、agent-native-tooling关联
  - [[architect-operator-model]]：添加agent-native-tooling、agent-output-verification关联
  - [[software-3.0]]：添加agent-native-tooling、agent-output-verification关联
  - [[builder-reviewer-model]]：添加agent-output-verification、agent-native-tooling关联
- 更新：[[index.md]]、[[home.md]]（新增主题"Agent输出验证与Agent原生工具"、更新mermaid图和状态）

## [2026-05-05 10:00] ingest | Claude发现了时钟，然后失控了
- 源文件：[[claude-discovers-clock]]
- 创建概念页：
  - [[sensory-gap]]（AI感知维度缺失：感知能力缺失如何限制智能的本质，AI活在永恒的"当下"）
  - [[compulsive-capability-use]]（新能力强迫性使用：获得新感知维度后的过度使用现象）
- 交叉链接更新：
  - [[jagged-intelligence]]：添加sensory-gap（感知缺失是锯齿智能深层根源）、compulsive-capability-use关联
  - [[neural-computer]]：添加sensory-gap关联（Neural Computer的感知子系统正是填补感知缺失的方向）
  - [[continual-learning]]：添加sensory-gap关联（持续学习解决"不能学"，感知缺失解决"没有经验可学"——两者互补）
  - [[harness-engineering]]：添加sensory-gap和compulsive-capability-use关联（脚手架必须预设AI过度使用新能力）
  - [[action-based-ai]]：添加sensory-gap关联（新感知维度可能产生不可预见的自主行为）
  - [[agentic-engineering]]：添加sensory-gap和compulsive-capability-use关联
- 索引更新：[[index]]添加1源摘要+2概念页
- 门户更新：[[home]]添加AI感知缺失主题、概念图扩展、状态更新

## [2026-05-04 14:00] ingest | 软件护城河是假的，Snap在15年前就知道了
- 源文件：[[spiegel-software-no-moat]]
- 创建概念页：
  - [[software-no-moat]]（软件功能不构成护城河：功能被快速复制，生态系统、硬件、关系才是壁垒）
  - [[distribution-bottleneck]]（分发是消费级产品的真正瓶颈：产品好不好不重要，能不能送到用户手里才重要）
  - [[loonshots-dual-organization]]（Loonshots双组织模型：创新团队和运营团队共存，领导者维护对话而非偏向一极）
  - [[listen-dont-build]]（倾听用户但不照做：从反馈中提取底层需求，做出全新品类）
  - [[social-resistance-to-ai]]（社会对AI变革的抵触：科技行业严重低估了人类接受度对技术部署速度的制约）
- 交叉链接更新：
  - [[product-taste]]：添加software-no-moat关联（品味是不可复制的护城河）
  - [[pm-as-gap-filler]]：添加loonshots-dual-organization关联（Snap 200人后才招第一个PM）
  - [[role-convergence]]：添加Spiegel观察（设计师开始直接提交代码，AI加速角色融合）
  - [[ai-readiness-gap]]：添加social-resistance-to-ai关联（准备度鸿沟从组织延伸到社会）
  - [[clarity-before-automation]]：添加listen-dont-build和social-resistance-to-ai关联
  - [[power-user-pull]]：添加distribution-bottleneck关联（power user口碑是稀缺的分发替代路径）
  - [[dogfooding-as-method]]：添加loonshots-dual-organization关联（Snap内部App摇一摇+AI自动修复）

## [2026-05-04 12:30] digest | Demis Hassabis：AGI还缺什么，智能体到底行不行，下一个科学突破长什么样
- 源文件：[[hassabis-agi-agents-science]]
- 深度更新现有概念页（添加源文件的实质性论据、证据、细节）：
  - [[agi-missing-pieces]]：添加记忆问题"检索成本"论据、AlphaGo遗产复活节（MCTS在现代基础模型规模上重新应用）、alphafold-breakthrough-conditions关联
  - [[continual-learning]]：添加Agent场景从"玩具展示"到"真正增加效率"的进展观察、"梦境循环"工程临时方案的完整上下文
  - [[einstein-test]]：添加Hassabis"还没看到AI的任何重大发现"判断、Co-Scientist和AlphaEvolve系统提及、vibe-coding关联（craft和soul）
  - [[alphafold-breakthrough-conditions]]：添加"根节点问题"概念、AlphaFold用户数据（300万+研究人员）、制药高管反馈
  - [[general-specialized-architecture]]：添加"追求困难问题和简单问题难度差不多"原文引用、alphafold-breakthrough-conditions和jevons-paradox-inference双向链接
  - [[jevons-paradox-inference]]：添加Jevons原始语境（1865年煤炭）、Hassabis双重角色判断（建模型+用AI做科学使判断更有参考价值）、general-specialized-architecture双向链接
  - [[agent-matrix]]：深化Hassabis对Agent ROI的质疑——添加"实验阶段"判断、"完整任务不够好"、"最近两三个月开始找到真正有价值场景"
  - [[agi-pilled]]：添加Hassabis个人AGI时间线（2030年）、深科技创业AGI中途出现的商业影响
  - [[vibe-coding]]：深化einstein-test关联——添加Theme Park原型6分钟vs 6个月对比、"craft和soul"缺失论据、6-12个月内1000倍生产力作品预测
  - [[jagged-intelligence]]：添加Hassabis下棋观察（Gemini识别臭棋后绕一圈又回去走）、"过度思考"overthinking现象、agi-missing-pieces关联
  - [[harness-engineering]]：添加continual-learning关联（缺乏持续学习是Agent无法交付后不管的根本原因）
  - [[product-taste]]：添加einstein-test+vibe-coding关联（Hassabis的"craft和soul"观察——产品品味在AI时代的另一种说法）
- 源摘要页更新：[[hassabis-agi-agents-science]]添加product-taste、harness-engineering、jevons-paradox-inference出站链接
- 无新页面创建
- 孤儿页面检查：所有6个概念页均有4-8个入站链接，无孤儿
- 无矛盾标记

## [2026-05-04 12:00] ingest | Demis Hassabis：AGI 还缺什么，智能体到底行不行，下一个科学突破长什么样
- 源文件：[[hassabis-agi-agents-science]]
- 创建概念页：
  - [[agi-missing-pieces]]（AGI的50/50判断：现有范式可能是最终架构的一部分，但也可能还需1-2个关键突破）
  - [[einstein-test]]（AI创造力的终极测试：用1901年物理学知识训练系统，看它能否产出狭义相对论）
  - [[alphafold-breakthrough-conditions]]（AlphaFold式突破三条件：巨大搜索空间+清晰目标函数+足够数据或模拟器）
  - [[continual-learning]]（持续学习：模型部署后从新经验中学习的能力，AGI和Agent的共同瓶颈）
  - [[general-specialized-architecture]]（通用编排器+专用工具架构：做好垂直专用系统在AGI时代依然有巨大价值）
  - [[jevons-paradox-inference]]（推理的杰文斯悖论：效率提高→需求增加→消耗掉所有效率收益）
- 更新现有概念页：
  - [[jagged-intelligence]]：添加AGI缺什么、爱因斯坦测试、持续学习关联
  - [[agent-matrix]]：添加Hassabis对Agent投入产出比的质疑、持续学习缺失、推理杰文斯悖论关联
  - [[agi-pilled]]：添加AGI 50/50判断作为校准锚点
  - [[vibe-coding]]：添加爱因斯坦测试关联（半小时做Theme Park原型但没爆款）
  - [[neural-computer]]：添加持续学习关联（神经计算机可能天然支持持续学习）
  - [[harness-engineering]]：添加通用+专用架构、推理杰文斯悖论关联
  - [[agent-architecture-patterns]]：添加通用+专用架构、持续学习关联
- 交叉链接：
  - [[jagged-intelligence]] → [[agi-missing-pieces]]、[[einstein-test]]、[[continual-learning]]
  - [[agent-matrix]] → [[continual-learning]]、[[jevons-paradox-inference]]
  - [[agi-pilled]] → [[agi-missing-pieces]]
  - [[vibe-coding]] → [[einstein-test]]
  - [[neural-computer]] → [[continual-learning]]
  - [[harness-engineering]] → [[general-specialized-architecture]]、[[jevons-paradox-inference]]
  - [[agent-architecture-patterns]] → [[general-specialized-architecture]]、[[continual-learning]]
- 索引更新：[[index]]添加1源摘要+6概念页
- 门户更新：[[home]]添加AGI路径与AI for Science主题、概念图扩展、探索路径更新、状态更新

## [2026-05-04 11:00] digest | 大多数公司根本没有为 AI 做好准备
- 源文件：[[companies-not-ready-for-ai]]
- 深度更新现有概念页（添加源文件的实质性论据、隐喻、细节）：
  - [[organizational-self-knowledge]]：添加完整10问题清单（含metrics和成本）、季度一致性诊断标准、"混乱黑盒"节（含TV static隐喻和work streams观察）、"给故障发动机镀金"隐喻、小企业结构性优势论据、AI在新世界角色（"门票"而非"武器"）
  - [[ai-readiness-gap]]：添加"镀金"隐喻原文、"竞争对手也一样烂"均衡论、AI在新世界的真实角色（武器vs门票）、均衡被打破论据
  - [[clarity-before-automation]]：扩展核心问题的紧迫性（"必须不遗余力尽快达到那个状态"）、添加Miessler咨询经验证据、问题严重性诊断（"不是技术成熟度问题，根源要深刻得多"）
  - [[harness-engineering]]：添加"组织层面的脚手架"节——脚手架工程的前提不只是技术基础设施，而是组织已理清"要做什么"；组织面vs技术面是同一枚硬币的两面
  - [[architect-operator-model]]：添加架构师能力=组织自我认知在个人层面映射的具体论证，引用Miessler的10问题
  - [[agentic-engineering]]：添加"组织前提"节——不是所有组织都配得上Agentic Engineering，混乱黑盒引入Agent只会放大混乱
  - [[ai-first-prerequisites]]：添加"技术前提之上还有组织前提"节——五大前提是技术门槛，组织自我认知是更深层前提
  - [[product-taste]]：扩展clarity-before-automation关联，添加Miessler的具体10问题与产品品味的呼应
  - [[role-convergence]]：添加与organizational-self-knowledge的深层联系——角色融合的前提是组织目标清晰
  - [[builder-reviewer-model]]：添加clarity-before-automation反向链接，Builder驱动AI的前提是组织已"配得上"AI
  - [[organizational-self-knowledge]]：添加role-convergence反向链接
- 无新页面创建
- 无矛盾标记

## [2026-05-04 10:00] ingest | 大多数公司根本没有为 AI 做好准备
- 源文件：[[companies-not-ready-for-ai]]
- 创建概念页：
  - [[organizational-self-knowledge]]（组织自我认知：AI赋能的前提不是AI技术，而是组织能否清晰描述自己的目标、工作流和决策机制）
  - [[ai-readiness-gap]]（AI准备度鸿沟：清晰公司用AI如虎添翼，混乱公司用AI只是镀金，差距急剧扩大）
  - [[clarity-before-automation]]（先清晰再自动化：你无法去优化一个连你自己都没搞懂的东西）
- 更新现有概念页：
  - [[harness-engineering]]：添加组织自我认知、先清晰再自动化关联
  - [[ai-first-prerequisites]]：添加组织自我认知、先清晰再自动化关联
  - [[architect-operator-model]]：添加组织自我认知、AI准备度鸿沟关联
  - [[product-taste]]：添加先清晰再自动化关联
  - [[agentic-engineering]]：添加组织自我认知、AI准备度鸿沟关联
  - [[builder-reviewer-model]]：添加AI准备度鸿沟关联
  - [[minimal-product-specs]]：添加先清晰再自动化关联
- 交叉链接：
  - [[harness-engineering]] → [[organizational-self-knowledge]]、[[clarity-before-automation]]
  - [[ai-first-prerequisites]] → [[organizational-self-knowledge]]、[[clarity-before-automation]]
  - [[architect-operator-model]] → [[organizational-self-knowledge]]、[[ai-readiness-gap]]
  - [[product-taste]] → [[clarity-before-automation]]
  - [[agentic-engineering]] → [[organizational-self-knowledge]]、[[ai-readiness-gap]]
  - [[builder-reviewer-model]] → [[ai-readiness-gap]]
  - [[minimal-product-specs]] → [[clarity-before-automation]]
- 索引更新：[[index]]添加1源摘要+3概念页
- 门户更新：[[home]]添加组织自我认知与AI准备度主题、概念图扩展、探索路径更新、状态更新

## [2026-05-04 00:30] digest | 5源深度整合
- 源文件：[[openclaw-hermes-architecture]]、[[codex-team-dogfooding]]、[[cat-wu-ai-pm-role]]、[[ai-first-strategy-wrong]]、[[ai-native-hiring-guide]]
- 深度更新现有概念页（添加源文件的实质性论据、证据、细节）：
  - [[agent-architecture-patterns]]：添加预算计数器机制（90次LLM调用+1次宽限调用）、Dreaming三阶段细节、prompt缓存三策略（四断点+JSON排序+对象复用）、skill进化闭环的技术后果、prompt策略的结构性分化解释
  - [[ai-agent-frameworks]]：更新Hermes记忆系统为具体三本笔记本（MEMORY.md/USER.md/Skills）、OpenClaw Dreaming三阶段细节、skill公共教材vs私人笔记的技术细节
  - [[action-based-ai]]：添加预算管理和上下文压缩机制（[[openclaw-hermes-architecture]]）、Codex统一Rust核心架构（[[codex-team-dogfooding]]）、开放生态vs围墙花园张力（[[cat-wu-ai-pm-role]]）
  - [[dogfooding-as-method]]：添加设计师代码量数据、PM思维探索具体描述
  - [[pirate-ship-team]]：添加招聘哲学（看作品不看简历）、统一使命作为海盗船燃料（[[cat-wu-ai-pm-role]]）
  - [[power-user-pull]]：添加tmux 18终端窗口故事和Codex桌面应用催生
  - [[product-taste]]：添加PRD替代方案（metrics readout + team principles）、Claude性格护城河（低ego+积极正面）
  - [[role-convergence]]：添加Cat/Boris 80% mind-meld具体案例、中间地带消失的招聘证据
  - [[research-preview]]：添加Claude Code源码泄露事件（两层人工审查漏过，定性为流程失败）
  - [[pm-as-gap-filler]]：添加PM价值悖论（最高效模式不需要PM，但PM价值答案是product taste——停留在抽象层面）
  - [[harness-engineering]]：添加CREAO三致命瓶颈和99%生产代码数据、AI First适用/不适用场景、宝玉xp洞察、Issue写作质量作为认知脚手架
  - [[architect-operator-model]]：添加创始人物理学博士背景与架构师能力来源
  - [[ai-first-prerequisites]]：添加CREAO 25人vs数百人规模证据
  - [[self-healing-pipeline]]：添加99%生产代码数据
  - [[vibe-coding]]：添加CREAO对Vibe Coding的明确批评——只能做原型，不能做生产
  - [[dual-horizon-planning]]：添加脚手架工程关联
  - [[agentic-engineering]]：添加AI驱动开发流程（Issues→Claude Code→PR→人工审查）和沟通瓶颈论据
  - [[ai-piloting]]：添加5分钟快速判断法三问题表
  - [[ai-native-veto]]：扩展价值排序（判断力>执行力、沟通>技术、协作心态>个人能力）
  - [[software-3.0]]：添加Codex Rust核心架构关联
  - [[ai-native-veto]]：添加[[pm-as-gap-filler]]反向链接
  - [[harness-engineering]]：添加[[dual-horizon-planning]]反向链接
  - [[codex-team-dogfooding]]（源摘要）：添加[[software-3.0]]、[[action-based-ai]]出站链接
- 无新页面创建
- 孤儿页面检查：所有源摘要和概念页均有≥2个入站链接，无孤儿
- 矛盾标记：PM价值悖论（[[pm-as-gap-filler]]中标注）——最高效模式不需要PM，但PM价值答案无法操作化定义

## [2026-05-04 00:20] ingest | AI-Native 工程师招聘面试官手册

## [2026-05-04 00:20] ingest | AI-Native 工程师招聘面试官手册
- 源文件：[[ai-native-hiring-guide]]
- 创建概念页：
  - [[builder-reviewer-model]]（Builder-Reviewer模型：AI-Native团队只有两种角色，中间地带消失）
  - [[ai-piloting]]（AI驾驶能力：机甲战士的基本功，驾驭AI Agent作为协作搭档）
  - [[ai-native-veto]]（AI-Native一票否决项：6项行为信号触发即淘汰）
- 更新现有概念页：
  - [[architect-operator-model]]：添加Builder-Reviewer模型、AI驾驶、一票否决关联
  - [[role-convergence]]：添加Builder-Reviewer模型和一票否决关联
  - [[agentic-engineering]]：添加Builder-Reviewer、AI驾驶、一票否决关联
  - [[harness-engineering]]：添加Builder-Reviewer、AI驾驶关联
  - [[product-taste]]：添加Builder-Reviewer模型关联
  - [[pm-as-gap-filler]]：添加Builder-Reviewer模型关联
  - [[vibe-coding]]：添加AI驾驶能力关联
  - [[jagged-intelligence]]：添加AI驾驶能力关联
  - [[action-based-ai]]：添加Builder-Reviewer模型关联
- 交叉链接：
  - [[architect-operator-model]] → [[builder-reviewer-model]]、[[ai-piloting]]、[[ai-native-veto]]
  - [[role-convergence]] → [[builder-reviewer-model]]、[[ai-native-veto]]
  - [[agentic-engineering]] → [[builder-reviewer-model]]、[[ai-piloting]]、[[ai-native-veto]]
  - [[harness-engineering]] → [[builder-reviewer-model]]、[[ai-piloting]]
  - [[product-taste]] → [[builder-reviewer-model]]、[[ai-native-veto]]
  - [[pm-as-gap-filler]] → [[builder-reviewer-model]]
  - [[vibe-coding]] → [[ai-piloting]]
  - [[jagged-intelligence]] → [[ai-piloting]]
  - [[action-based-ai]] → [[builder-reviewer-model]]
- 索引更新：[[index]]添加1源摘要+3概念页
- 门户更新：[[home]]添加AI-Native招聘范式主题、概念图扩展、探索路径更新、状态更新

## [2026-05-03 23:50] ingest | 为什么你的"AI优先"战略可能大错特错
- 源文件：[[ai-first-strategy-wrong]]
- 创建概念页：
  - [[harness-engineering]]（脚手架工程：工程核心从写代码转为为AI构建工作环境和约束条件）
  - [[ai-first-prerequisites]]（AI优先的五大前提：自动化测试、CI/CD、监控、任务管理、系统架构）
  - [[architect-operator-model]]（架构师-操作员模型：AI First工程组织的两极分化形态）
  - [[self-healing-pipeline]]（自愈流水线：检测-分诊-修复-验证的最小人工干预闭环）
- 更新现有概念页：
  - [[agentic-engineering]]：添加脚手架工程、架构师-操作员、自愈流水线、AI优先前提关联
  - [[vibe-coding]]：添加脚手架工程作为对立面关联
  - [[role-convergence]]：添加架构师-操作员模型作为极端形态
  - [[dogfooding-as-method]]：添加自愈流水线、脚手架工程关联
  - [[product-taste]]：添加脚手架工程作为产品品味在工程架构上的体现
  - [[action-based-ai]]：添加脚手架工程、自愈流水线关联
  - [[pirate-ship-team]]：添加架构师-操作员模型关联
  - [[pm-as-gap-filler]]：添加架构师-操作员模型关联
  - [[dual-horizon-planning]]：添加AI优先前提关联
- 交叉链接：
  - [[agentic-engineering]] → [[harness-engineering]]、[[architect-operator-model]]、[[self-healing-pipeline]]、[[ai-first-prerequisites]]
  - [[vibe-coding]] → [[harness-engineering]]
  - [[role-convergence]] → [[architect-operator-model]]、[[ai-first-strategy-wrong]]
  - [[dogfooding-as-method]] → [[self-healing-pipeline]]、[[harness-engineering]]
  - [[product-taste]] → [[harness-engineering]]、[[ai-first-strategy-wrong]]
  - [[action-based-ai]] → [[harness-engineering]]、[[self-healing-pipeline]]、[[ai-first-strategy-wrong]]
  - [[pirate-ship-team]] → [[architect-operator-model]]
  - [[pm-as-gap-filler]] → [[architect-operator-model]]
  - [[dual-horizon-planning]] → [[ai-first-prerequisites]]
- 索引更新：[[index]]添加1源摘要+4概念页
- 门户更新：[[home]]添加AI First工程基础主题、概念图扩展、探索路径更新、状态更新

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
