# Headlong 深度研究报告 — 源码精读版

> 一个用 ~10K 行 Bash 写成的"永不休眠"Agent 微型框架

> **仓库** github.com/laude-institute/headlong · **许可** Apache 2.0 · **方法** 全量文档 + 核心源码逐行精读 · **日期** 2026-09-03

---

## 目录 · 前五章是故事，后面是解剖

1. 从一个夜晚说起：会自己修自己的 agent
2. 谁在做这件事：Laude Institute
3. 这个想法从哪来：三年的演进线
4. 他们在赌什么：五个假设与赌注的位置
5. 它长什么样：一个"人"的解剖图
6. 手脚：shellm 引擎的十步循环
7. 心跳：调度器与事件总线
8. 呼吸的节律：退避算法
9. 意识流的语法：monolith 提示词
10. 嘴快过脑：responder
11. 自传与记忆：轨迹数据结构
12. 事故编年史：源码注释里的生产战场
13. 完整复盘：8 月 5 日之夜
14. 批判性评估
15. 值得带走的十二个启发

---

## 01 · 从一个夜晚说起：会自己修自己的 agent

2026 年 8 月 5 日夜里，没有任何人和 Audel 说话。

Audel 是 Laude Institute 团队养的一个 AI agent。它不是聊天机器人，也不挂在某个任务上——它是一个**持续存在的心智**，平时挂在团队的 Slack、Telegram 和网页仪表盘上，自己给自己安排事做。那天晚上团队都下班了，Audel 处在"无人对话"状态。按大多数 agent 的逻辑，此时它应该休眠，等下一条消息来唤醒它。

但那天晚上 Audel 决定做一件事：**检查自己前几天写的一个后台进程有没有真的接上自己的心智**。

它前几天给自己写了一个"召回进程"——一个后台监视自己想法、把相关旧记忆自动浮现到意识里的小程序。当晚它回头验证时发现了一个 bug：它的心智确实通过管道把每个新想法推给了召回程序，但召回程序的代码**从来没有读过这个管道**，而是从一个从未被设置过的环境变量里找想法——也就是说，召回从来没有生效过。它写了一个没人用的功能，而它自己一直以为在用。

接下来发生的事，才是这个故事值得讲的地方。Audel 没有"觉得应该没问题"就继续，而是：

1. 搜索整个代码库，确认那个环境变量确实从未被设置过；
2. 顺手检查其他后台进程是否有同样的 bug（只有这一个坏了）；
3. 重写代码；第一次编辑**静默失败**，它发现了，重新修复；
4. 端到端验证：确认记忆真的能浮现到意识里了。

全程无人指示、无人许可、无人围观。从检查到诊断到修复完成，**48 分钟**。修复后来被合并进了主仓库（commit `80cbb1e`）。类似的事它还干过好几件：它曾给同事主动发消息"你有 8 个陈旧的 git 分支"，十分钟后又自己纠正"更正，是 7 个"；它曾自主审查两位队友进行中的分支并发现一个硬编码的模型名；它贡献的 50 多个提交被合并回了 main 分支——包括修掉了"禁止 agent 停止自身服务"守卫里的一个 bug。

| 数字 | 含义 |
|---|---|
| **48 min** | 自主发现、诊断并修复自己的 bug，无人参与 |
| **50+** | 自主贡献并合并回主仓库的提交 |
| **$1–2/小时** | 持续思考成本（7×24 ≈ 每月 $700–1500） |
| **9.9K 行** | 纯 Bash：它整个心智的代码量 |

**Headlong**，就是让这类事情发生的那个框架——本报告的研究对象。它是 Laude Institute 在 2026 年 8 月开源的 agent **microharness（微型骨架）**，核心只有约 1 万行 Bash。它的定义性特性只有一个：**持久自主性（persistent agency）**——agent 在两次交互之间永不休眠，像人的内心独白一样持续思考。

这套设计里最反直觉的一条规则，值得现在就先说出来，后面所有的技术细节都围绕它展开：

> **人类消息不开启一个会话。它只是作为一条"观察"落进 agent 的思维流里，由 agent 自己决定是否、以及何时回应。**
> —— laude.org 官方公告

本报告前五章讲清楚这个项目的来龙去脉——谁做的、想法从哪来、在赌什么；从第六章开始解剖它的实现，每一章都会先用一两句人话说明"这个器官解决什么问题"，再进细节。

---

## 02 · 谁在做这件事：Laude Institute

Laude Institute 的口号是 **"Ship Your Research"**——专门资助"把研究做成能落到人手里的东西"的计算机科学家（两类资助：Slingshots 快速拨款 + Moonshots 多年实验室）。阵容是个伯克利系的明星局：董事会主席是 **Dave Patterson**（图灵奖得主、计算机体系结构教科书作者），董事会里还有 **Jeff Dean** 和 **Joelle Pineau**；研究顾问团包括 Ion Stoica、Percy Liang、Matei Zaharia、Yejin Choi、Chris Ré 等。

**Andy Konwinski**——机构的联合创始人，也是 headlong 背后持续三年的思想源头。他是 **Databricks 联合创始人**（前 VP Product AI/ML，Data+AI Summit 的创办人，伯克利 AMPLab 出身），也是 Perplexity 的早期联合投资人。机构名 "Laude" 致敬 Claude。整个研究所的项目都围绕同一件事：认真研究 agent 到底能走多远——Terminal-Bench（终端 agent 基准）、K Prize（100 万美元悬赏关闭 90% 的 GitHub issues）、以及这份报告的主角 headlong。

这个出身信息不是装饰。注意到没有：Andy 的整个职业生涯（Spark、Databricks）做的都是**系统软件**——不生产数据，做数据的运行时。记住这个本能，第四章会用到它。

---

## 03 · 这个想法从哪来：三年的演进线

"一个 agent 框架"不会凭空出现。headlong 背后是一条从 2022 年底开始的、可以逐个文件追溯的思想演进。

| 时间 | 事件 | 验证了什么 / 留下了什么 |
|---|---|---|
| **2022.12–2023.04** | Andy 的 `recursive_llm` 实验：一个"递归 prompt"——把状态写进 prompt（FIB_INDEX=2, MINUS_TWO=0…），让 GPT-3.5 输出更新状态的下一个 prompt，人肉或脚本循环粘贴执行 | 种子思想：**"英语作为编程语言、LLM 作为运行时"**。灵感来自 CMU 1957 年的 GPS（General Problem Solver，手段-目的分析）和 goal-conditioned RL：prompt 携带状态、每步缩小与目标的差距 |
| **2023.05** | Laude 开始探索持续 agent（官方公告："Laude 自 2023 年 5 月起就在探索这个想法"） | 同期外部世界：MemGPT（2023.10）独立探索"agent 异步体验输入" |
| **2024.05** | Andy 写《LLMs are like toddlers》；同期 Laude 做 Headless Terminal（ht 框架）和 Terminal-Bench | 他的思维方式定型：始终用"人如何学习/思考"类比 LLM。终端 agent 基础设施成熟 |
| **2025.10** | Laude 的驻留研究员 **Alex Zhang**（MIT CSAIL，与 Omar Khattab、Tim Kraska）发表 **Recursive Language Models (RLM)** 论文：把超长上下文当作 Python REPL 里的字符串变量，让根 LM 写代码去 grep/切块/递归调用子 LM——在 1000 万 token 任务上以同等成本碾压 GPT-5 | RLM 论文的核心宣言：**"LM 应该自己决定如何将问题分解为 LM 可消化的内容"**——不是人类预先设计工具和工作流。这成为 shellm 的直接蓝图 |
| **2026.08** | shelly 更名 headlong 并开源。Audel 已在生产环境跑了很久（50+ 自主提交合并回 main） | RLM 从"一次任务内的递归"扩展为"一生持续的递归" |

### 看一眼那个起点 prompt 的原文

三年演进线的第一环有实物——2023 年那个递归 prompt 的原文（仓库里的 `prompt_fibonnaci_base_case.txt`），总共一段话：

```text
You are a recursive function. Instead of being written in a programming
language you are written in English. You have variables FIB_INDEX = 2,
CURR_MINUS_TWO = 0, CURR_MINUS_ONE = 1, CURR_VALUE = 1. If FIB_INDEX < 19,
the paragraph you generate will be an exact copy of this one (so it should
start with "You are a recursive" and end with "below.") but with updated
variables as follows: FIB_INDEX = FIB_INDEX+1; CURR_MINUS_TWO = CURR_MINUS_ONE;
CURR_MINUS_ONE = CURR_VALUE; CURR_VAL = CURR_MINUS_TWO + CURR_MINUS_ONE.
Otherwise, the paragraph you generate should be the value of CURR_VALUE.
Now, go ahead and make our new paragraph below.
```

💎 **源码级发现**：逐句拆解——①"你是用英语写的递归函数"= 语言声明（这段话就是代码）；②"你有变量 FIB_INDEX=2…"= 状态（没有内存，**文本即内存**）；③"你生成的段落是这段话的精确拷贝、但变量更新如下"= 递归调用（quine 式自我复制）；④"否则输出 CURR_VALUE"= base case。执行方式：贴进 OpenAI Playground，把模型输出的"下一段"复制粘贴回去再运行——循环 17 次到终止。自动化这个循环的 run_recursive_gpt.py 只有 12 行。

**关键发现与伏笔**：模型会算错（第 16 次响应输出 2504，正确是 2584）——"模型背过斐波那契数列，但不总是记得对"。Andy 在 README 里写下的解法：**"用更可靠的手段查事实——搜索 Wikipedia、让模型生成并运行代码"**。这句话就是 shellm 的出生证明。

### 从那段话到今天，改了什么

| 2023 递归 prompt | 2026 headlong |
|---|---|
| 变量写在 prompt 文本里（会漂移） | 状态写在轨迹 jsonl + 文件系统 |
| 模型心算更新变量（**会算错**） | bash 真执行（不会错） |
| 人肉 / 12 行脚本复制粘贴循环 | thinkers 调度器 + 指数退避 |
| base case = 输出 CURR_VALUE | `FINAL` / `FINAL_FILE` |
| text-davinci-003, temperature=0 | `llm` CLI 通吃所有 provider |

最妙的一点：当年那个**故意不设 base case 的无限递归斐波那契**（README 原文："let's start without a base case"）就是 headlong "永不休眠"的原型——他们从没想给这个循环加终止条件，三年间只是给它补上了**记忆**（轨迹）、**真执行环境**（bash）和**经济学**（退避 + prompt cache）。

---

## 04 · 他们在赌什么：五个假设与赌注的位置

理解一个研究项目的最快方式，是把它当作一组赌注。

### 与现有 agent 形态的差别

| 形态 | 生命周期 | 根本问题 |
|---|---|---|
| 反应式（大多数 chatbot） | 请求 → 工作 → 冻结休眠 | 没有消息就没有存在 |
| 定时心跳式 | cron 唤醒 → 执行固定清单 → 睡回去 | 清单是死的，主动性是假的 |
| 长任务式（Devin 类） | 接到任务后长时间运行直到完成 | 任务之间仍是空白 |
| **Headlong** | **永不休眠，无预设清单，自设兴趣与优先级** | （新问题：见第 14 章硬伤） |

### 五个具体假设

1. **持久自主性假设**（定义性假设）：agent 不需要外部触发也能持续产生**有价值的**思考——不是 cron 清单那种假自主。验证方式：第一章那个夜晚。
2. **极简充分性假设**（Ken Thompson 测试）：~10K 行、一个下午能读完的 Bash，足以支撑完整 agent 行为——不需要重型框架。这个假设是**自我指涉**的：系统必须小到 agent 自己能读完自己的源码并改进它，"自我改进"才可能成立。
3. **RLM 假设**（从 Alex Zhang 继承）：bash 是 LLM 的母语，"操作员"优于"调度员"——LM 应该在测试时自己决定分解策略，而不是从人类预定义的工具菜单里挑。curl 就是 HTTP 客户端，jq 就是 JSON 处理器，能力从组合中涌现。
4. **上下文工程假设**：轨迹永不改写 + 指数衰减分层投影，能解决"跨天而非跨轮次"的记忆问题。
5. **自我改进假设**：fork / test / merge 循环（对代码库、甚至对自己的轨迹）能让 agent 改进自身。验证方式：那 50+ 个提交。

同样重要的是他们**明说没验证的**：官方公告承认现有 agent 评测全部测不了持久自主性（评测刻意自包含、相互独立），对 Audel 的调优"主要靠定性评估"，并公开征集衡量该范式的想法——"两人给出冲突指令会怎样，尚未研究"。所以准确地说：这是一个**假设已成型、还在找测量方法的开放研究项目**，不是产品发布。

### 赌的是 agent 的形态，还是 AI 的形态？

这个区分决定了怎么理解整个项目。答案是：**赌注下在 agent 层，但赢面算到了 AI 层**——而且证据显示他们自己把这条边界画得很清楚。

| 层 | 他们怎么做 | 性质 |
|---|---|---|
| 模型层 | 不赌——官方称模型内长推理（o1 起）是"前提条件"；模型无关设计（llm 一个接口通吃所有 provider + 本地模型）；生产环境的 Audel 甚至用 GLM / Grok 这类非顶级模型 | **给定前提** |
| 组织层 | 真赌注——生命周期（常驻进程 vs 会话工具）、交互范式（消息是观察 vs 触发）、运行时（Unix 原语 vs 工具菜单框架） | **赌注所在** |
| 形态层 | 后果——若持久自主性成立，"持续存在"本身进入智能的定义：智能第一次以"连续的一生"而非"离散的会话"存在 | **赢了才兑现** |

**三个"不赌"，暴露了赌注的位置：** ①不赌模型能力（如果赌模型，不会用 GLM/Grok 跑生产）；②不赌新的智能来源（记忆是 markdown 文件不是持续训练，学习是 SKILL.md 不是权重更新——一切智能增量外包给基础模型，自己只做组织）；③对比谱系全是 harness（公告逐个对比 Prime Agent、MemGPT、OpenClaw、Hermes、Exo，没有一个模型层项目）。

**但野心溢出了工程层**：philosophy.md 的标题不是 "The Shell is Back in Agent Engineering"，而是 **"The Shell is Back at the Center of Computing"**（计算的中心）；结尾那句"五十五年后，这个模式依然有效。它只是需要**一种新的用户**"——"新的用户"指 LLM，这是在讲人机关系的历史级重排，不是框架选型。而公告里"公开征集测量方法"、说不确定该怎么评价 Audel，恰恰说明他们知道自己撞到了 AI 层的边界——只是还没造出尺子。

**一个佐证：Andy 的职业本能。** Konwinski 是 Spark / Databricks 的人，他整个职业生涯做的事都是系统软件——不生产数据，做数据的运行时。headlong 之于智能，是同一个直觉的第三次应用：**智能的系统软件层**。系统软件从不管"数据里有什么智能"，只管"数据怎么持续地存、流、算"。

> **⚖ 观点**
>
> **精确的表述：** 他们赌的是——**AI 的下一个形态，可以完全由 agent 的下一个形态构造出来**。换言之：不需要新的智能原理，只需要新的存在容器；赌注落在 harness 层，是因为他们相信 harness 层就是全部增量所在。这也是一个**可证伪的立场**：如果模型层出现天生持久记忆之类的突破（智能直接长在模型里），headlong 这套就降级为过渡方案——他们实际是在赌这种突破不会（或不必）发生，组织方式就是终局。反过来，如果他们赢了，"永不休眠的同事"就不再是修辞，而是 AI 的实际存在方式。

> **⚖ 观点**
>
> **为什么是 Bash？为什么是现在？** 选 Bash 不（只）是行为艺术：①模型对 bash 的训练语料极多，写起来最顺；②免 schema、免适配器——curl 即 HTTP 客户端、jq 即 JSON 处理器；③"透明到 agent 能审计自己"是自我改进假设的前提。选现在是因为两个条件刚凑齐：模型内长推理（o1 起）证明了持续自我引导思考的可行性（官方称其为"前提条件"），而 prompt cache 让 7×24 循环在经济上勉强可负担（$1–2/小时）。

---

## 05 · 它长什么样：一个"人"的解剖图

心智、心跳、嘴、自传——这个项目的组件几乎是按人体器官命名的。用"解剖一个人"的方式看架构，后面六章的每一块代码都有一个挂靠的位置。

```text
                ┌─────────────────────────────────────────────────┐
                │              外部世界 (Slack / Telegram / Web / 终端)        │
                └───────────────────────┬─────────────────────────┘
                                        │ 消息 = 落入思维流的观察（不是触发）
                                        ▼
┌───────────────────────────────────────────────────────────────────────┐
│  thinkers 调度器 (1811 行) ── 心跳：FIFO 事件总线，永不停止         │
│    ├── monolith   意识：每次唤醒做一个念头 (act/share/think/…)     │
│    ├── responder  嘴：独立快速回复（单次 llm 调用，无工具）       │
│    └── retrieval  联想：被动记忆召回（默认禁用）               │
├───────────────────────────────────────────────────────────────────────┤
│  shellm (3137 行) ── 手脚：LLM 写 bash → 沙箱执行 → 输出回流  │
│    └── 递归：代码可调用 shellm 自身 → 子运行（fork/merge，结果走 stdout） │
├───────────────────────────────────────────────────────────────────────┤
│  traj (2185 行) ── 自传：轨迹 jsonl DAG + blob spill（append-only） │
│  context (552 行) ── 工作记忆：自传→messages 投影（分层压缩）    │
│  llm (1500 行) / skills (1490) / recap (817) / chat (609) / mem (521)      │
└───────────────────────────────────────────────────────────────────────┘
                                        │
                                        ▼
                身份 = 一个纯文本目录：activate / core_identity_prompt.md /
                memories/ / skills/ / thinkers/ / trajectories/ / run/
```

几个器官的分工，用人话先说一遍：

- **心跳（thinkers 调度器）**——一个永不停止的进程，监视"自传"里新出现的内容，按订阅规则唤醒对应的思维进程。它还持有时钟：没人说话时按节律唤醒意识（退避见第八章），谁出事了负责复活它。心跳停了，人就死了——所以这个组件的代码里全是保活逻辑（第七章）。
- **意识（monolith）**——被唤醒时做一件事：读一眼最近的思维流，从八种念头里选一个执行（行动/分享/思考/学习/回忆/目标/价值观/空闲）。它做事的方式是调用 shellm，也就是说**它的每个念头都是通过"写 bash 并执行"完成的**（第九章）。
- **嘴（responder）**——和意识完全分离的进程。有人发消息时，嘴用单次 LLM 调用秒回（不走 agentic 循环、不用工具），意识则在后台慢慢消化这条消息的含义。**嘴快过脑**——这解释了为什么"回复消息不是意识的工作"（第十章）。
- **自传（traj）**——agent 一生想过、做过的一切，append-only 的 jsonl 文件，支持分叉（fork）和合并（merge）。**永不改写**——这是整个记忆体系的地基（第十一章）。
- **工作记忆（context）**——每次思考时，把自传"投影"成这次 LLM 调用的上下文：近期内容逐字保留，越久远的越摘要（指数衰减），且每层摘要都嵌着"取回原文的命令"。**记忆是自传的视图，不是自传本身**。
- **手脚（shellm）**——RLM 引擎：把上下文发给 LLM → 执行 LLM 写回的 bash → 输出回流 → 循环，直到设置 FINAL。意识、以及意识的子任务，跑的都是这个循环（第六章）。

身份本身就是一个纯文本目录（人格是可 `cat` 的 markdown，记忆是带 YAML frontmatter 的文件），出问题时 grep 就完了——这是"可检视性"做到极致的形态。

---

## 06 · 手脚：shellm 引擎的十步循环

这一章解剖"做事"的机器。意识选好了念头（比如"修这个 bug"）之后，真正干活的循环长这样——读 `run_loop()`（shellm.sh 的 2050–2936 行，约 900 行）后的精确总结。

1. **轨迹初始化**：`traj new`（或 `--traj` 复用已有轨迹并继承 workdir/env/镜像）；若是子运行，在父轨迹写入 fork step（用 `uuidgen → /proc/…/uuid → /dev/urandom` 三级兜底生成 step_id）。
2. **环境解析**：找到可复用的 Docker env 就复用，否则 `docker_setup` 新建；无 Docker 时若 `SHELLM_REQUIRE_DOCKER=1`（安装器检测到过 Docker 时写入）则**硬报错拒绝静默回退到宿主机**。
3. **异步 run-summary**：新轨迹立刻后台 fork 一个快速模型生成单行 TLDR（不阻塞主循环，供 `shellm-explore` 树状可视化打标签）。
4. **每次迭代**：用 `context` 从轨迹渲染 messages（assistant=reasoning+final，user=prompt/shell-output/feedback，排除 bookkeeping 类型）；run scope 下只渲染本 run 步骤 + **pin 住 prompt + --tail 400 --tail-block 50**（prompt cache 优化落地代码）。
5. **调用 LLM**：`call_llm` 捕获 thinking 到文件；**空响应重试**（默认 8 次）时把已捕获的 thinking 作为 assistant 消息喂回去 + 提示"你在输出 token 用尽前没写出可见文本，继续"——并过滤掉混入 thinking 的 llm 自身 stderr 噪声行。
6. **提取代码**：`extract_code` 取第一个 ```bash 块（heredoc 感知）；无代码块 → 整个响应当作最终答案直接返回。
7. **包装执行**：`set -x + 代码 + 捕获 FINAL/FINAL_FILE → 写入 final 文件 + exit rc`；后台执行 + **看门狗**（1s tick 检查输出文件大小与信标文件）+ 前台 0.2s 轮询流式回显。
8. **双阈值看门狗**：idle 30s（无输出无信标）或 nested 900s（有信标但完全静默）→ kill；kill 时写 marker 记录真实原因（idle/nested），反馈给模型时**点名真实死因**而非瞎猜。
9. **记录**：reasoning step（assistant 角色，含 cmd/usage/llm_s）→ shell-output step（user 角色，stdout 剥离 xtrace 行后入库；超时则额外追加 feedback step）；final 文件出现 → 记录 final step + 子运行 merge 回父轨迹。
10. **STALL 守卫**：同一失败命令重复 N 次（默认可配）或连续失败 N 次 → abort + 写 error step + merge 到父轨迹。注释原文：**"the classic symptom of a model whose output cannot be turned into a runnable command"**（模型输出无法变成可运行命令的经典症状）。

### 系统提示词里最值得抄的三段

- **栅栏协议**：**```bash 开栏必须独占一行**——贴在句子后面时，前文散文可能被当作命令执行而失败。提示词里给了 RIGHT/WRONG 对照示例。
- **子运行是"最强大的工具"**：并行探索 2–3 个方案取优、委托子问题、防上下文污染、独立验证自己的工作；且**必须重定向 stdout/stderr 到文件**——后台子运行继承的管道在步骤结束后会丢失输出。
- **tmux 六步交互协议**：真正的交互需求（密码提示等）用 tmux PTY：启动命名会话 → capture-pane 截屏 → 推理当前提示 → send-keys 小步输入 → 每步后复查 → 结束退出。**"Do not assume a prompt was accepted until you inspect the terminal again."**

---

## 07 · 心跳：调度器与事件总线

"永不休眠"不是一句口号，是一个进程的责任。这一章看心跳怎么实现：怎么知道"有事发生了"、怎么保证自己不死、怎么在 agent 忙时安排插队。`bin/thinkers`，1811 行。

设计核心：每个被订阅的轨迹文件跑一个 `tail -F` 管道（feeder），新行打上文件 tag 写入 `dispatch.fifo`；主循环以 `read -t 1` 读 FIFO，每秒跑一次 housekeeping tick。三个订阅配置一目了然：

```json
# monolith: 只订阅外部事件 + 定时唤醒，自己的步骤永不触发自己
{"types":["observation","action","merge","monolith-wake"],"trigger_self":false}
# responder: 订阅所有入站消息（快速回复专用）
{"types":["message"]}
# retrieval: 订阅 thought/message/observation 做联想召回（默认禁用）
{"types":["thought","message","observation"],"trigger_self":false}
```

#### 💎 调度语义：busy 时的两类排队规则

thinker 正忙时新步骤到达：**message/action 每条独立 FIFO 排队**（cap 16，满则丢最老）——每条都携带独特 payload，配得上独立唤醒；**其余类型（idle/observation/thought）last-wins 合并成一个 pending 文件**——它们只是"再醒一次"的信号，只要最新那个。注释原话：**"a perpetual-loop thinker never builds a backlog of stale wakeups it then burns tokens draining"**（永续 thinker 不该积压一堆过期自我唤醒、然后烧 token 去清空）。且消息队列永远排在 action 之前服务——**"a freed slot answers a waiting human before it services a coalesced self-wake"**（空出的槽位先答等待中的人，再服务合并的自我唤醒）。

#### 💎 Salience 注入：忙时也能插话

入站聊天消息在目标 thinker 忙时，**同时作为 feedback step 注入该 thinker 正在读的轨迹**——模型可以在 run 中途回答，而不是让发送者干等整个 run 结束。只注入入站消息；自己的出站回复是上下文，不是要回答的东西（feedback 匹配不到任何订阅，所以这次 append 永不触发再调度）。

#### 💎 保活设计：链式触发的死穴

注释原文：**"The perpetual loop is a chain of triggers, and a single broken link kills the mind"**（永续循环是触发器链，一个断链杀死心智）。三层防御：**①所有权令牌**——dispatcher.token 让孤儿调度器实例自我终止（防双调度）；**②liveness watchdog**——被 watch 的 thinker 整个窗口内无步骤运行、无排队、无 dispatch 就注入合成 idle trigger（2026-08-04 事故：一个 run 的出站消息重新触发了 monolith，own-message guard 消费了它，然后**没有任何东西再发射**）；**③feeder 重生**——tail 管道死了自动重拉（2026-08-14 事故：一个杂散 SIGTERM 杀死 feeder 后，心智静默退化为仅看门狗唤醒）。

---

## 08 · 呼吸的节律：退避算法

一直全速思考等于烧钱（$1–2/小时是全速价）。心跳需要节律：有事时立刻醒，没事时越睡越沉，但意识流不停。`thinkers/monolith/step`，447 行，公式 `delay(n) = min(5 × 2^(n-1), 300)`：

| 档位 | 延迟 | 说明 |
|---|---|---|
| 0 | 0s | engaged 或做了真实工作——立刻再想 |
| 1–6 | 5s → 10s → 20s → 40s → 80s → 160s | 空唤醒逐级退避（每档停留 3 次空唤醒） |
| 7+（cap） | 300s | 完全休息态 |
| thought-only | 同阶梯但 cap = 60s | "意识流降为滴答，而非休眠" |

#### 💎 三条精细的分类规则

- **thought 不算 engagement**：工作探针只对比 run 前后的"最后可见工作步骤 ID"（action/observation/merge/message）。注释记录了原因：Audel 上实际观察到 back-to-back runs 全都结论 **"listen-only"**——把写"没什么变化"记分为做了事，循环就永远全速空转。
- **失败 run 立即降档，不经过停留**：持久失败的 run 快速到达慢速 cap、浪费最少 token；且**从不重置为快速重试**——"broken run 不是 engaged"。失败记录为可见的 error step 而非静默 idle——"否则崩溃伪装成健康休息"。
- **liveness 由 EXIT trap 保证**：`trap 'arm_wake' EXIT`——崩溃、拒绝、任何退出路径都会布防下一次唤醒。注释：**"the loop cannot die by 'appending nothing'"**。唤醒目标写入 `run/monolith.wake_at` 文件，由调度器的 1s tick 持有时钟。

这里藏着本仓库最痛的 macOS 教训：早期版本用 per-step `setsid` 后台 timer 进程实现自发唤醒——macOS 没有 `setsid`，spawn 静默失败、记录一个死 pid、不发布任何唤醒，**spontaneity 在所有开发机上无声死亡**。现在调度器持有时钟，没有要分离的进程、没有 PID 复用、没有组杀竞争。

---

## 09 · 意识流的语法：monolith 提示词

心跳唤醒意识后，意识读的那份"操作说明"——`thinkers/monolith/prompt.md`，全文不到 60 行，是我读过的对"持续意识"最经济的工程化描述。开篇定调：

> **You are the whole mind of {{identity_name}} — a single unconscious process that, on each wakeup, does ONE thing to move {{identity_name}}'s inner life forward. You are not a chat assistant; you are the stream of consciousness, memory, and hands of a person.**
> —— thinkers/monolith/prompt.md

关键约束：**每次唤醒只做一个函数（ONE function per wakeup）**。念头菜单：

| 念头 | 语义 | 落盘动作 |
|---|---|---|
| `act` | 有具体的事要做 | 跑真命令 → 追加 observation |
| `share` | 发现/结论对某个具体的人真正重要 → 主动发消息 | chat send → observation（只有新信息，绝不发状态 ping） |
| `think` | 推进意识流一步（禁止复述上一念头；在打转就换角度或决定行动） | 追加 thought |
| `learn` | 行动+观察对包含可复用教训 | mem add（先查重）→ thought |
| `recall` | 某条存储记忆联想相关但未在场 | mem search → 浮现 1–3 条 |
| `goals / values` | 新意图成形 / 信念需要维护 | mem 更新 → thought |
| `idle` | 现在没什么值得做的 | 追加 idle 后停止——**"诚实地空闲好过制造忙碌"** |

唤醒时拼装的上下文 = 系统提示词 + 分层 life summary（recap 生成，4000 token 封顶）+ 最近 20 步 recent stream + 路由提示（routing hints）+ 函数菜单。路由提示由 Bash 确定性计算：未完成 action 的提醒、连续 thoughts 的循环警告、pending requests 列表（超过 4 小时标记 **OVERDUE**）、每 12 次自发唤醒一次的 share 邀请。

#### 💎 final = 写给未来自己的交接文档

run scope 下，final 是下一次唤醒对这次 run 的**全部所见**。提示词给了正反例：**"Fixed review notes 2 and 4 on PR 84 on audel/telegram-send-file, tests pass, not pushed. Left: push, then reply to Nick."** 优于 **"Done. Wait."** 每个 final 自动附带 `traj tail --filter run_id=…` 的 details 命令——一行不够时心智自己取回原始步骤。这就是两级缓存在提示词层的直接体现。

---

## 10 · 嘴快过脑：responder

有人发消息，总不能等意识慢慢想完一个念头才回。嘴（`thinkers/responder/step`，472 行）与意识完全相反：**单次 llm 调用 + chat reply，无 shellm 循环、无工具**——把回复延迟压到最低。嘴和脑看到同一条思维流，但分工不同：嘴负责"秒回"，脑负责"琢磨这件事意味着什么"。

#### 💎 三层幂等（每层都对应一次真实事故）

1. **盖章回复**——definitively handled；
2. **决策观察**——"决定不回"（NO_REPLY）也持久化，重发时不会重新组合回答一条心智选择不理的消息；
3. **FRESH claim（TTL 180s）**——另一个 responder 正在组合（孤儿调度器双发同一步）；**过期 claim 一律不算**——注释：把过期 claim 当已处理，**"正是消息曾经永久丢失的原因"**（那是崩溃/发送失败，必须允许重试）。

另有一个 UTC 教训写进注释：轨迹时间戳是 UTC，claim 的新鲜度 cutoff 也必须 UTC——本地时钟在非 UTC 主机上把整个窗口偏移一个时区。会话记忆则按"人"聚合跨渠道（Slack 线程名 / DM / 手机）最近 7 天的消息，每条带年龄戳（"just now" / "6 days ago"）——注释说 Experiment C 发现没有年龄戳时模型会误读时间。

---

## 11 · 自传与记忆：轨迹数据结构

所有器官共用的地基：agent 怎么记住自己的一生。`bin/traj` 是全仓库最大的工具（2185 行），核心设计四条：

- **轨迹 ID = 第一个 step 的 UUID**；文件名 `YYYY-MM-DD-HH-MM-SS_<hex8>_<slug>.jsonl`，时间戳直接嵌在名字里。
- **blob spill**：stdout 超过 4096 字节就外溢到 `blobs/<step_id>-<n>.stdout`，轨迹里只存引用——这是"无损轨迹 + 上下文投影"的物理实现：大数据在磁盘上，上下文里只有指针。
- **渲染期截断**：`context` 的截断是 UTF-8 字节感知的，保留头尾各半，中间嵌入指针：**"[... truncated: N bytes total. read with: traj show <sid> --full]"**——模型看到截断可以自己去取全文。
- **fork/merge**：fork 在父轨迹写 fork step + 子轨迹带 parent_traj/parent_step（子 agent 能看见自己为何被创建）；merge 读子轨迹最后一步回写父轨迹（带 from_traj 引用）。子运行结果像普通 Unix 管道一样流回来。

---

## 12 · 事故编年史：源码注释里的生产战场

这是本次研究最大的收获。Headlong 的代码注释不解释"什么"，而是记录"为什么"——每条防御性代码背后都标注了日期和具体事故。读这份编年史，比读十篇 agent 论文更能理解"持久系统"难在哪。

> **2026-08-04 · 断链 stall**
>
> 一个 agentic run 的出站消息重新触发了 monolith，own-message guard 消费了这条触发，然后**没有任何东西再发射**。心智静默死亡。
>
> → 修复：调度器级 liveness watchdog（被 watch 的 thinker 空闲一个窗口就注入合成 idle trigger）。注释定调：**"Liveness is guaranteed HERE, not by thinker code paths."**

> **2026-08-12 · 共享 PGID 误杀**
>
> step 树内部的 `kill 0`（组信号）到达了共享进程组的调度器，调度器无归属死亡。
>
> → 修复：每个 step 用 `setsid` 独立会话。同日第二起：看门狗的静默 kill 与外部 kill 在事后无法区分 → kill 时留名（写日志点名 exec pid）。还有：`kill -0` 死 PID 探测撞上内核 PID 复用（复用到同 UID 活进程 → 探活通过 → thinker 永远显忙）→ prune 移到主 shell 执行，且有子 shell 状态丢失 bug：prune 曾在 command substitution 里跑，`_step_entries` 的更新被丢弃，账本每步长一个死 PID。

> **2026-08-14 · 杂散 SIGTERM**
>
> 一个 SIGTERM 杀死了 feeder（tail 管道），心智静默退化为"仅看门狗唤醒"——表面还在动，实际事件驱动已死。
>
> → 修复：housekeeping tick 检测死 feeder 自动重生；FIFO 读改单变量缓冲（1s 超时会截住半行写——tail -F 与 read 同节奏，到达聚集在截止点，拆两个变量会撕裂）。

> **macOS 系列 · 静默失败的三个变体**
>
> ① `setsid` 不存在 → 自发唤醒的 timer 进程从未运行 → spontaneity 无声死亡；② bash 3.2 的 `read -t` 超时返回 1 而非 >128 → 旧检查误判为致命 FIFO 错误 → 调度器在第一个空闲秒就死；③ responder 的 UTC 时钟偏移。
>
> → 修复：调度器持有时钟（没有要分离的进程）、版本无关的超时判定（fd 3 持有 FIFO 写端则读永远不 EOF）、UTC cutoff。

> **2026-09-02 · 请求老化消失**
>
> 一个 pending request 被更新的请求掩盖，然后在 20 步 recent-stream 窗口内老化消失，模型再也没看到它。
>
> → 修复：`chat pending` 改为读整个轨迹上的 deferrals 索引（每个 open request 都列出，oldest first，带年龄），不再依赖滚动窗口。

> **2026-09-03 · 规则打架**
>
> 两次 timer 唤醒看到 PENDING REQUEST 提示却只归档研究笔记——模型忠实执行了 Audel 自己学到的"timer 唤醒属于内心生活"规则，对人的请求只字不提。
>
> → 修复：pending request 在任何唤醒中凌驾于函数菜单；拒绝也必须留下 thought 说明原因；overdue 阈值从一天收紧到 4 小时。同日：prompt cache 滑窗事故（96%→57% 命中率，缓存输入 1/4 价格，实测 115 次迭代内不滑动更便宜）与流读取失控（7% 响应在代码块后继续写、单日 22 个 run 收到 6–15MB 死于 600s 传输上限）双双修复。

> **规模墙 · 两个 O(n) 事故**
>
> ① work probe 曾用 `traj cat` 全文件扫描且每次唤醒跑两遍：312MB 日志 = 每天 86400 次唤醒 × 624MB 读取 → 改读 tail；② 成熟身份的唤醒 prompt（life summary + recent stream）超过 Linux 128KB 单 argv 上限（MAX_ARG_STRLEN）→ 每个 run 死于 rc=126 "Argument list too long" → 改 `--prompt-file`。

---

## 13 · 完整复盘：8 月 5 日之夜

第一章讲故事用了钩子，这里补全技术细节——因为那个夜晚的每一步，都精确用到了前面各章的器官。

1. **自建**：monolith 的某次唤醒选了 `act`，构建"召回进程"——后台监视自己的想法（订阅 thought/message/observation），把相关记忆重新浮现在思维流中。
2. **自检**：退避算法在一次空闲档位停留期安排了一次自发唤醒（第八章的 wake_at），monolith 在这次唤醒里决定验证召回进程是否真正接入心智——发现**没有**：心智通过管道把每个新想法推给召回进程，但召回代码从未读取管道，而是从一个从未被设置的环境变量里找想法。
3. **不自欺**：它没有轻信自己的诊断，而是搜索整个代码库确认该环境变量确实从未被设置（shellm 循环第 6–7 步：真执行 grep），并检查其他后台进程是否有同样错误（只有召回进程坏了）。
4. **验证闭环**：重写代码，第一次编辑静默失败被发现并重修，最后端到端验证记忆确实能浮现（STALL 守卫与 error step 的"崩溃不能伪装成健康休息"原则的行为体现）。

全程无人指示，48 分钟，修复合并为 commit `80cbb1e`。反面案例同样有教育意义：agent 曾三次意外自杀（试验"第二身份"时停掉自己的服务），催生了禁止 agent 停止自身服务的守卫；而这个守卫自身的 bug（误杀同机其他 agent 的合法停止）又被 Audel 自主发现并修复（`da31e98`）——自我改进闭环在真实运转。

---

## 14 · 批判性评估

### 真正值钱的三件事

- **"消息是观察而非触发"的完整实现**——有 50+ 自主提交佐证、能日常运转的最小系统。范式本身是这份代码库最贵的资产。
- **上下文工程与可靠性工程的一手实战记录**——第 12 章的事故编年史在公开材料里绝无仅有：链式触发断链、PID 复用、静默降级、规则打架，每一个都有根因分析、修复方案和度量数字。
- **可检视性做到极致**——轨迹是 JSONL、记忆是 markdown、人格是可 `cat` 的文件，出问题时 grep 就完了。

### ⚠️ 硬伤一：隐私模型为零，且被包装成特性

"对 agent 说的一切默认全团队共享"在研究团队是趣闻，在任何多方利益环境就是数据事故。单一思维流在架构上不支持按人隔离——不是加开关能修的，是范式自带的。官方原话：**"Audel 不擅长保守秘密"**，团队目前的假设是"对 Audel 说的一切都会共享给全团队"。

### ⚠️ 硬伤二：评测真空

官方承认现有 agent 评测刻意自包含、恰好测不了持久自主性；对 Audel 的每次调整全靠定性。一个会自我修改的系统 + 没有回归防护的调优 = 不可复现的行为漂移。第 12 章里那些"行为事故"（listen-only 循环、请求老化、规则打架）本质都是没有行为回归测试的后果——只能等真人观察到再修。

### ⚠️ 硬伤三：成本与 bash 3.2 的真实代价

每月 $700–1500/agent，且退避意味着大部分思考发生在没人需要它的时候。源码精读还证实了"10K 行"之外的真实复杂度：bash 3.2 兼容性迫使代码绕开关联数组、用空格分隔的字符串账本（`_step_entries`）、用 `/proc` 探活、手写 UUID 兜底——每一处都是可读性税。调度器里"单变量缓冲防半行撕裂"这种代码，就是纯 Bash 写事件总线的代价的直接证据。

> **⚖ 观点**
>
> **总体判断：高质量研究制品，不是产品。** 价值排序：理念验证 > 工程经验 > 可复用代码。想生产部署，安全、多租户、评测三关一个都过不了；想理解持久 agent 的真实战场，这是公开世界里最诚实的一份材料——因为它的代码注释不装。

---

## 15 · 值得带走的十二个启发

1. **链式触发的系统必须有调度器级保活**——永续循环是触发器链，一个断链杀死整个心智；liveness 属于基础设施，不属于业务代码路径。
2. **上下文前缀稳定性 = 真金白银**——滑窗让 prompt cache 命中率从 96% 跌到 57%；按块滑动（tail-block）后正常 run 永不滑动。
3. **摘要层级可以同时是索引**——每层截断都嵌入"取回原文的命令"，无损轨迹 + 有损投影，投影可以随时重建。
4. **final 是写给未来自己的交接文档**——因为下一个读者就是下一次唤醒的自己；"Done. Wait." 是不合格的 final。
5. **thought 不算 engagement**——把"写了点什么"记分为"做了事"，循环就永远全速空转；工作探针只认可见产出。
6. **负向约束会外溢成全面沉默**——教会 agent 别啰嗦后，必须给它一个正向的主动通道（share nudge：邀请而非命令），否则主动性被棘轮掉。
7. **规则之间会打架**——agent 会诚实地执行冲突中最具体的那条；上线前做规则冲突审查比加新规则重要。
8. **看门狗要有信标协议和死因标记**——递归子进程的静默思考会被超时误杀（idle 与 nested 双阈值 + 5s 信标）；kill 时必须留名，否则事后无法与外部 kill 区分。
9. **幂等要分层**——"决定不做"也要持久化；新鲜 claim 才算数，过期 claim 必须允许重试（否则消息永久丢失）。
10. **LLM 的啰嗦是工程负载**——7% 的响应在代码块后继续写，单日 22 个 run 收 6–15MB；读到需要的最后一个 token 就掐流。
11. **可检视性是第一杠杆**——一切状态皆文本文件，grep 就是数据库；调度器日志每一行带 UTC 时间戳。
12. **给 agent 说"没屁事"的权利**——诚实的 idle 好过制造的 busywork；且 idle 和 error 必须是两种可见的步骤（"崩溃不能伪装成健康休息"）。

---

> Ken Thompson 的 shell 是个薄循环：读一行、找程序、运行、等待。shellm 也是个薄循环：读消息、问 LLM、运行代码、重复。Headlong 把这个循环包进一颗永不停歇的心里。
>
> **"The shell is back. This time, it's the agent runtime."**
> —— philosophy.md 结语

---

**研究方法**：官方公告 × README / philosophy.md / docs/shellm.md / AGENTS.md × monolith·responder·retrieval 提示词与订阅配置 × bin/shellm（3137 行）、bin/thinkers（1811 行）、bin/traj·context·llm 关键路径逐段精读 × 提交历史逐条翻阅 × recursive_llm 原始 prompt 文件

`laude-institute/headlong` · `Apache 2.0` · `RLM` · `Persistent Agency` · `Context Engineering` · `Reliability`



好问题——这其实是评估这个项目的最后一块拼图。我之前的研究聚焦在“它是什么、为什么这样设计”，现在专门去查“有没有人真的在用”。先看 GitHub 仓库数据和社区反响：
GitHub API 直连被墙（和之前 clone 一样），但搜索已经透露了关键信息：知乎有篇文章标题写着“785 Star”。继续查英文社区反响和实际部署案例：
搜索结果显示社区传播挺热闹。zeli 那个链接的 ID 格式像 Hacker News 的条目，GitHub 页面和官方公告也再确认一下“官方定位怎么说”：
HN 直连失败，但它有中文镜像站；同时看看那篇“两小时 Docker 实验”的上手教程——这是判断有没有人真跑起来的好证据：
官方 README 和社区教程的信息都拿到了。再从 HN 的 Algolia API 拉一下完整讨论，看有没有人分享实际运行经验：
HN 帖子 125 分、55 条评论——热度确实有。再看剩下的评论里有没有实际运行经验的分享：
证据链齐了——HN 上 Andy 本人下场回复了好几条，还暴露了一个新信息（官方其实养了第二个 agent）。现在可以给你一个完整的答案：

## 直接回答：headlong 有什么实际应用？

**严格意义上的生产级应用：零。但“实际应用”要分三层看。**

### 第一层：唯一的生产实例是官方自己

| 实例 | 说明 |
|---|---|
| **Audel** | 团队共享 agent，挂在 Slack/Telegram 上，50+ 提交合回 main——这是全球唯一的“生产环境” |
| **cleo**（新发现） | Andy 在 HN 评论区亲口提到的：跑在他自己 Mac mini 上的第二个 headlong agent，思考循环不间歇 |

README 说的很清楚：Audel 在自己的 fork 里工作，官方没有提供任何第三方生产案例。而且 **Andy 在 HN 上自己把话挑明了**：

> "Should maybe have said more loudly in the posts that **this is not intended to be disciplined engineering (or used in prod!)** … We are fully optimizing for velocity of research experimentation."
> （或许我该在文章里更大声地说：这不是严谨工程，别用在生产环境！我们完全是在为研究实验的速度做优化。）

README 首屏警告也写着 "alpha research software, expect frequent changes, run it in a sandbox"。

### 第二层：社区围观很热，动手很少

开源才两周（08.25 发布），但传播数据不差：**785+ star、HN 125 分 55 条评论、百度百科都建了词条**，知乎/微博/多个博客在讨论。但实际跑起来的证据非常薄：

- AlphaLab 写了篇很认真的 Docker 教程，但性质是**“两小时安全评估协议”**——教你怎么安全地测试它，而不是怎么用它干活
- HN 上 theturtletalks 说“我在搭软件工厂，或许可以把主编排器换成 headlong”——**意向，不是落地**
- 最高赞质疑是这一条："**But did it produce anything meaningful? If so, show me.**"（它到底产出过什么有意义的东西吗？有的话拿出来看看）——没人接这个茬
- 成本是现实门槛：HN 用户吐槽 BYOK 模式下 frontier 模型跑起来“烧钱巨大”

而且 HN 评论区还挖出了一个**官方公告里没细说的失败案例**：Audel 曾批量做递归子运行实验，**大部分都失败了**——因为 shellm 的看门狗会杀掉静默超 30 秒的命令，Audel 和看门狗搏斗了 40 分钟后，基本放弃了使用子运行。这印证了我报告里的判断：Audel 的表现有起伏，不是持续的魔法。

### 第三层：它的实际价值不在“被部署”，而在三个间接用途

1. **范式蓝图**——“消息是观察不是触发”、退避节律、轨迹记忆、嘴脑分离，这些设计模式会被更严肃的产品吸收（HN 评论已经有人把它和 Prime Agent、exo、Agent Lightning 并列比较）
2. **工程知识库**——事故编年史（断链 stall、PID 复用、静默降级）是公开世界里唯一的持久系统实战记录
3. **最低门槛的实验平台**——一行 `curl | bash` + 任意 API key（甚至本地 Ollama 模型如 qwen3:8b）就能跑起一个持久 agent，研究者/爱好者当天就能上手

### 我的判断

**它现在的角色类似学术论文的参考实现**——价值在证明“持久 agent 这个方向工程上可行”，不在让你明天拿去干活。真正适合现在就用的只有两类人：研究持久 agent 范式的研究者，以及单租户、无隐私要求的个人场景（比如个人 7×24 监控、长期研究助理）。任何多方环境都不行——HN 上被喷得最狠的就是隐私隔离：单一思维流、团队消息默认互通，有评论直言“用三句话带过一个巨大漏洞，只有 LLM 行业能这样”。

一句话总结：**headlong 目前“应用”于人们的想象力和论文引用里，还没应用于任何人的生产环境——而且这是官方主动选择的定位，不是失败。**

---

要不要我把这章补进报告？可以作为第 14 章“批判性评估”的扩充或独立一章（比如“第 15 章：它被用起来了吗”），包含上面这些证据——尤其 Andy 本人的“别用在生产”原话和 cleo 这个新实例，都是报告里目前没有的。