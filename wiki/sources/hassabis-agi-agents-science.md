---
type: interview
date: 2026-04-30
author: Demis Hassabis / 宝玉翻译
url: https://baoyu.io/blog/demis-hassabis-agents-agi-and-the-next-big-scientific-breakthrough
raw: raw/clips/Demis Hassabis：AGI 还缺什么，智能体到底行不行，下一个科学突破长什么样.md
---

# Demis Hassabis：AGI 还缺什么，智能体到底行不行，下一个科学突破长什么样

**TL;DR** Hassabis用50/50的概率判断拆解AGI路径——现有范式可能是最终架构的一部分，但也可能还需要1-2个关键突破。智能体还在实验期，投入产出比没对上。AI for Science的下一个AlphaFold正在路上，但AI能否"发明围棋"而不仅是"下出Move 37"才是真正的创造力测试。

![封面](https://s.baoyu.io/imgs/2026-04-30/ytcover.jpg)

## 核心论点

### AGI还缺一两块拼图

Hassabis认为当前范式（预训练+RLHF+思维链）"几乎可以确定"是AGI架构的一部分，但给出了50/50的概率判断：一半可能现有技术足够，一半可能还缺一两个大想法。三个未解问题：[[continual-learning|持续学习]]、长程推理、记忆。([[hassabis-agi-agents-science]])

![AGI缺哪几块](https://s.baoyu.io/imgs/2026-04-30/01-framework-agi-missing-pieces.png)

### 记忆是"用胶带糊住的临时方案"

百万token上下文窗口听起来很大，但处理实时视频只够录20分钟。Hassabis博士研究的就是海马体如何整合新知识，DQN的经验回放就借鉴了这个机制。当前把所有东西塞进上下文窗口的做法不是长期方案。([[hassabis-agi-agents-science]])

![记忆不是上下文窗口](https://s.baoyu.io/imgs/2026-04-30/02-infographic-memory-context-window.png)

### AlphaGo遗产正在复活

DeepMind正在重新审视MCTS等AlphaGo时代的技术，在现代基础模型规模上重新应用。未来几年的进步将大量来自旧想法与新规模的结合。([[hassabis-agi-agents-science]])

![AlphaGo旧想法复活](https://s.baoyu.io/imgs/2026-04-30/03-flowchart-alphago-revival.png)

### 锯齿状推理：下棋暴露的缺陷

Hassabis用Gemini下棋时观察到一个现象：模型识别出一步是臭棋，找不到更好选择后又回去走那步臭棋。这种"缺乏自省"是[[jagged-intelligence|锯齿状智能]]的核心缺陷——能解IMO金牌题却犯基本算术错误。但修复可能只需一两个关键调整。([[hassabis-agi-agents-science]])

![下棋推理回路](https://s.baoyu.io/imgs/2026-04-30/05-flowchart-chess-reasoning-loop.png)

### 智能体投入产出比还没对上

智能体是通向AGI的路径，但目前还不能"交付后不管"。Hassabis直言："很多人启动几十个智能体跑40个小时，但我不确定产出能匹配这种级别的投入。"缺乏[[continual-learning|持续学习]]是根本原因。([[hassabis-agi-agents-science]])

![智能体ROI](https://s.baoyu.io/imgs/2026-04-30/06-comparison-agents-roi.png)

### 创造力测试：能发明围棋吗？

半小时做出Theme Park原型（原来要6个月），但还没有vibe coding做出的爆款。AlphaGo的Move 37还不够——[[einstein-test|真正的测试是能否发明围棋]]，而不仅是下出妙手。([[hassabis-agi-agents-science]])

![创造力阶梯](https://s.baoyu.io/imgs/2026-04-30/07-framework-creativity-ladder.png)

### AlphaFold式突破的三条件

1. 巨大的组合搜索空间（大到暴力搜索无法解决）
2. 清晰的目标函数（能定义"什么是好的"）
3. 足够的数据或能生成同分布合成数据的模拟器

三个条件成立时，现有方法就能在"大海捞针"式搜索中走很远。([[hassabis-agi-agents-science]])

![AlphaFold三条件](https://s.baoyu.io/imgs/2026-04-30/13-framework-alphafold-conditions.png)

### 爱因斯坦测试

用1901年的物理学知识训练系统，看它能不能做出爱因斯坦1905年做的事——包括狭义相对论。比解决千禧年难题更难的是：能否提出新的千禧年级别问题？当前系统缺乏"类比推理"能力。([[hassabis-agi-agents-science]])

![爱因斯坦测试](https://s.baoyu.io/imgs/2026-04-30/14-timeline-einstein-test.png)

### 通用+专用架构

未来不会是一个包含所有能力的巨大通用模型。更可能是通用模型（Gemini、Claude等）调用AlphaFold这样的专用系统作为工具。把蛋白质折叠知识直接塞进Gemini"肯定会影响它的语言能力"。做好垂直领域的专用系统在AGI时代依然有巨大价值。([[hassabis-agi-agents-science]])

### 把AGI算进商业计划

如果你的AGI时间线是2030年，深科技创业通常需要10年，那AGI会在你旅程的中途出现。你的系统能利用AGI吗？AGI出现后你的产品会怎样？

### 推理永远不会免费

杰文斯悖论：效率提高→需求增加→消耗掉所有效率收益。百万级智能体集群、并行思考都会吃掉所有算力。即使能源成本趋零，芯片制造仍是瓶颈。([[hassabis-agi-agents-science]])

## 相关概念

- [[agi-missing-pieces]] - AGI的50/50判断与三个未解问题
- [[einstein-test]] - AI创造力的终极测试
- [[alphafold-breakthrough-conditions]] - AlphaFold式突破的三条件框架
- [[continual-learning]] - 持续学习：AGI和Agent的共同瓶颈
- [[general-specialized-architecture]] - 通用编排器+专用工具架构
- [[jagged-intelligence]] - 锯齿状智能：AI能力高度不均匀
- [[agi-pilled]] - 恰好正确程度的AGI信仰
- [[vibe-coding]] - 凭感觉编程：执行门槛降低但创造力未被替代
- [[agent-matrix]] - Agent矩阵与多智能体并行
- [[action-based-ai]] - 从聊天到行动派的范式转移
- [[neural-computer]] - 神经计算机架构设想
- [[agent-architecture-patterns]] - Agent架构模式
