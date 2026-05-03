讲讲 OpenClaw 和 Hermes Agent 到底是怎么分别构建的（出处见图）

这一次，我想回答一个在我脑子里盘旋了很久的问题。OpenClaw 和 Hermes Agent 解决的是同一个问题：它们都是持久化、自托管的 AI agent，运行在你的机器上，通过你已经在用的应用和你交流。

我带你把这两套架构过一下。

一、核心

在 OpenClaw 里，Gateway 是老大。AI 大脑作为一个独立运行时存在于它之下，叫作 Pi。Gateway 决定会发生什么、消息该流向哪里、哪个 agent 处理哪件事。AI 只是一个更大编排系统中的一个组成部分。

而在 Hermes Agent 里，AI 大脑本身就是主要决策者。它上面没有再套一个 Gateway。Agent 直接掌握对话循环，其他一切，比如消息平台、工具、记忆，都是挂在 agent 身上的，而不是挂在控制平面之上。

OpenClaw 是身体，Pi 是大脑。但在 Hermes 里，没有“身体”这个独立层。大脑就是全部。这种差异，几乎解释了这两个代码库的一切不同。

二、OpenClaw 的架构：

第 1 层是 Channels，也就是通道层。这里有 25 个以上的消息平台适配器，它们会把收到的消息归一化成统一格式。消息平台包括 WhatsApp、Telegram、Discord、Slack、iMessage、Signal 等等等等。

第 2 层是 Gateway。它是一个 WebSocket 服务器，充当中央神经系统，基本上会处理五类输入：人类消息、heartbeat、cron job、内部状态变更 hook，以及外部 webhook。一切都只是事件。

第 3 层是 agent 运行时，也就是 Pi 所在的地方。agentic loop 在这里运行。模型会收到一个 prompt，决定该怎么处理，调用工具，拿到结果，再决定下一步做什么。

第 4 层是记忆层。这里有一个 SOUL.md 文件，用来保存人格与行为规则；还有一个 MEMORY.md 文件，用来记录关于你和你偏好的事实。

Gateway 负责整体协调，而 agent runtime 则是刻意被分离出来、作为一个嵌入式进程存在。状态保存在 JSON 文件中，并通过原子写入来维护一致性。Gateway 是那面真正承重的墙。

三、Hermes Agent 的架构：

Hermes 没有一个压在最上面的 Gateway 层。Agent 自己就是最上层。所有东西都直接挂在一个名为 AIAgent 的 Python 类下面。

第 1 层：对话循环

这是一个带预算计数器的同步 while 循环。模型收到消息之后，要么返回工具调用，要么返回最终答复，然后循环继续或者停止。

让这个简单循环变得有意思的，有三件事。

预算：每一轮最多只能调用 90 次 LLM，就像一张预付费卡。用完之后，agent 还会得到最后一次“宽限调用”，用来总结它已经完成了什么。OpenClaw 没有这个上限，它的循环会一直跑，直到模型提供方把它停下来。

打断：每一次迭代都会检查用户是不是发来了新消息。如果是，就会优雅退出。

压缩：如果对话变得太长，Hermes 会裁剪旧的工具结果，保护最近的消息，并把中间部分总结掉。如果这样做三轮之后还是太长，它就会把当前会话拆开，并把新的会话和父会话关联起来。

第 2 层：Prompt 系统

这一层关注的是，agent 在开始思考之前，怎样构建自己的指令。

所以，在循环开始之前，Hermes 会先构造 system prompt，并把它缓存到整个 session 生命周期里。OpenClaw 则会在每一轮都重新构造 prompt，因此每次只加载和这一轮相关的技能。Hermes 采取的是相反路线：一次性全部加载，然后不再改变，尽量最大化缓存命中。

这很重要，因为 Anthropic 的 API 最多支持四个缓存断点。如果你的 prompt 开头在多次调用之间保持一致，模型提供方就可以跳过这些 token 的重复处理。Hermes 放了四个断点：system prompt 加上最近 3 条消息，并且让 system prompt 保持稳定，所以从第二轮开始，每一轮都会命中缓存。

Hermes 里还有两个缓存优化。第一，它会在把 JSON 工具调用参数发给 API 之前，先按字母顺序排序。这样，即便是同一个调用，只是 key 的顺序不同，也仍然能命中缓存。第二，Gateway 会在同一个 session 中复用同一个 AIAgent 对象，所以缓存过的 prompt 能跨轮次继续存在，而不需要重新构建。

OpenClaw 的方法，是让 prompt 更精瘦；Hermes 的方法，是让 prompt 更容易缓存。取舍不同，但目标是一样的：控制你的 API 开销。

第 3 层：工具系统

工具，是 agent 与世界交互的方式，比如读文件、运行终端命令、搜索网页、控制浏览器、发送消息。没有工具，agent 只能说话；有了工具，它才真的能行动。

Hermes 内置了 46 个工具。每个工具在代码启动时都会自动注册，不需要配置文件。有些工具还带快速可用性检查，比如你没有某个 API key，那这个工具就会悄悄隐藏自己，而不是直接崩掉。

更有意思的是，这些工具到底在哪里执行。OpenClaw 可以在你的机器上执行命令，或者放在 Docker 容器里执行，用户有两种选择；Hermes 则提供六种：你的本机、Docker、通过 SSH 连接的远程服务器、通过 Singularity 接入的高校 HPC 集群、Modal 上的 serverless cloud function，或者 Daytona 的开发环境。也就是说，agent 真可以“住”在这些地方并在那里运行。

并行处理方面也是如此。当模型一次要求做多件事，比如同时读三个文件、写一个文件时，Hermes 会先判断哪些任务可以安全并行。读取操作总是并行执行。写入操作也会并行，除非它们碰的是同一个文件。

第 4 层：记忆系统（三本笔记本）

这也是两套架构分歧最大的地方。

OpenClaw 有两个文件：SOUL.md 负责人格，MEMORY.md 负责事实，另外还有一个夜间运行的 Dreaming 系统。Dreaming 分为三个阶段：Light、REM 和 Deep。它会用六个带权重的因素给记忆打分并做提升。只有 Deep 阶段才会把内容真正写入 MEMORY.md。这意味着它每天都会额外消耗一些 API 调用。

而 Hermes 不是两个文件，而是三个。

MEMORY.md：记录你明确告诉它的事实，比如你的时区、语言、项目约定。这些内容会在 session 开始时被快照并冻结进 system prompt 里。文件本身可以更新，但 session 中途不会改 prompt。

USER.md：这里放的是“你是谁”这类信息，主要是你的风格、偏好、什么会让你烦躁。它可以是一个内置本地文件，也可以额外接入外部提供方，比如 Honcho、Mem0 或 Hindsight。

Skills：这是 agent 在完成复杂任务后写下来的文档。通过扫描文件系统来检索。下一次 agent 再次用到它们时，这些文档还会继续被打磨。

它没有后台进程，也没有额外的 LLM 调用。初始对话结束之后，这套记忆系统的维护几乎是“免费”的。

第 5 层：学习循环

在 OpenClaw 里，skills 是带 YAML frontmatter 的 Markdown 文件。一个 SKILL.md 会写上技能名、触发条件、所需权限，然后才是具体说明。它们由用户编写，发布到 ClawHub，别人可以安装。一旦写好，这个 skill 以后基本就保持不变。

Hermes 在架构上走了另一条路。用户当然也可以手写 skill，但系统本身也被设计成允许 agent 自己创建和改进它们。完成一个复杂任务后，agent 可能会问你，要不要把这套做法保存成 skill。如果你同意，它就会把一个 SKILL.md 写进 ~/.hermes/skills/。下一次遇到类似任务，它就会找到这个 skill，并照着执行。

这就是大家反复提到的那个著名的闭环学习机制。

做事 -> 反思 -> 生成 skill -> 持久化 -> 回忆 -> 精炼。

OpenClaw 的方法，给你的是一个庞大的社区市场，里面有成千上万的 skills。Hermes 的方法，给你的则是贴合你自己工作流、并且越用越好的 skills。

但这里有一个重要的技术后果。因为 Hermes 的 skill 是系统自己生成、并随着时间不断打磨的，所以当它积累了经验之后，再去完成类似任务时，所需的工具调用会更少。skill 文档里已经写好了哪些步骤是有效的，它不需要再重新摸索一遍。这会在 API 成本上随着时间推移体现出可测量的差异。

四、Session 持久化是怎么工作的

OpenClaw 用 JSON / JSONL 文件来存 session，并通过原子写入保证安全。跨 session 的召回依赖 LanceDB 的向量检索，这种方式很擅长语义相似，比如“找出关于部署的对话”，但对精确关键词没那么强。

Hermes 则把一切都存在 SQLite 里，开启 WAL 模式，并使用 FTS5。数据库 schema 现在已经是第 6 版，并带有迁移机制。所以当 agent 需要调出之前的 session 时，它会先对整个对话历史做全文关键词检索，再把结果总结出来。不需要单独再上一个向量数据库。

它还支持 session 分叉。/branch 命令会复制当前 session，让你可以沿着一条独立支线去探索。它的数据模型原生支持树状结构，通过 parent_session_id 这个外键来表达，而不只是线性历史。

五、适配器对比

在 OpenClaw 里，Gateway 是一个 WebSocket 服务器，负责路由、session、事件、heartbeat、cron 和 webhook 这些事情。这里的 agent 是一个子进程。你只要按 Gateway 的接口规范接入一个平台，就能自动获得 session 路由和事件排队这些能力。

在 Hermes 里，AI Agent 是主进程。GatewayRunner 只是一个很薄的适配层。每个平台——包括 WhatsApp、Telegram、Discord、Slack、Signal、通过 BlueBubbles 接入的 iMessage、WeChat、Email、SMS 等等——都有一个 BasePlatformAdapter 子类，用来把消息归一化，然后直接交给 agent。agent 自己内部还内置了 cron 调度器。

六、多 Agent 的故事

两者都支持 sub-agent。OpenClaw 给你的是灵活性。Hermes 给你的是护栏。

OpenClaw 的 Gateway 里有一棵 supervisor tree。agent 之间可以互相传消息，并且深度是可配置的。Task Flows 又在这之上增加了一层崩溃安全的编排能力。

Hermes 则会为每一个子任务新建一个 AIAgent。子 agent 只能使用父 agent 已经拥有的工具，而且不能用那些被禁掉的工具，比如 delegation、clarify、memory、code_execution。最大深度默认是 2。每个子 agent 还会获得一个独立的 IterationBudget，默认上限是 50。这些默认设置的目的，是在保持可配置性的同时，避免成本呈指数级增长。

把两个代码库完整读完之后，我认为它们真正的架构差异，其实不只是功能或能力层面的差异，而是那些结构性的选择——正是这些选择，决定了后面一切是如何运作的。