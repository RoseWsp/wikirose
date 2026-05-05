# Vibe Coding

**TL;DR**：Vibe Coding（凭感觉编程）是一种开发方式，开发者用自然语言提出意图，AI Agent生成、修改、调试代码，人不再逐行写代码，而是“凭感觉”让模型往前走，大幅降低软件创作门槛。

## 这是什么

Vibe Coding由Andrej Karpathy在2025年2月提出，描述了一种“放弃对代码本身的直接控制、顺着感觉让模型往前走”的开发体验。它不是硬性的方法论，而是一种状态转变：开发者从代码编写者变为意图表达者和质量监督者。

### 核心特征
1. **自然语言驱动**：用日常语言描述想要的功能，而非精确的API调用
2. **信任阈值突破**：AI生成的代码达到“直接可用”水平，无需或极少需要人工修改
3. **流程连续性**：模型能连续规划、写代码、调试、执行、根据反馈修正，形成连贯的工作流
4. **控制权转移**：人控制整体方向和规格，AI控制具体实现细节

## 为什么重要

Vibe Coding标志着编程范式的根本转变：

### 降低软件创作门槛
- **非程序员也能创建工具**：会描述需求就能做出可用软件
- **加速原型开发**：想法到可运行原型的周期从小时级缩短到分钟级
- **降低学习曲线**：不再需要记忆大量API细节和语法规则

### 改变开发者工作方式
- **从写代码到写规格**：重点转向清晰表达意图和约束条件
- **从调试到监督**：主要工作是审查AI输出是否符合系统边界和质量标准
- **从执行到协调**：协调多个AI Agent完成复杂任务

### 触发连锁反应
- **传统IDE进化**：代码编辑器集成自然语言理解成为标配
- **文档形式变化**：从“如何使用API”转向“如何描述意图”
- **团队协作调整**：代码审查重点从语法正确性转向架构合理性和系统安全性

## 演变轨迹

### 初期阶段（2024-2025）
- AI生成代码片段，但经常出错需要人工修改
- 开发者仍需要深入理解代码细节才能纠正错误
- 信任有限，仅用于辅助性任务

### 转折点（2025年12月）
- Karpathy报告AI生成的代码达到“直接可用”水平
- 连续数周无需修改AI输出，信任感建立
- Vibe Coding从实验状态进入实用状态

### 当前阶段（2026年）
- 成为AI-native开发者的标准工作方式
- 工具链成熟（Cursor、Claude Code等）
- 与Agentic Engineering形成互补：Vibe Coding降低门槛，Agentic Engineering保持专业标准

## 局限与挑战

### 代码质量的不确定性
- AI生成的代码“能跑但很难看”（Karpathy原话）
- 可能存在臃肿、复制粘贴、别扭的抽象和脆弱的结构
- 审美和代码品味尚未被有效训练进模型

### 系统理解的外包风险
- 开发者可能过度依赖AI，失去对底层机制的理解
- 当AI在系统边界、资金归属、安全模型上犯错时，缺乏发现和纠正的能力
- Vibe Coding隐含假设AI拥有类人感知能力，但AI实际上活在一个"永恒当下"——没有时间感、没有空间直觉 ([[sensory-gap]])。开发者凭"感觉"调prompt时，可能根本意识不到AI在某些感知维度上是全盲的。给AI一个新工具时，它不会"负责任地"使用，而是[[compulsive-capability-use|强迫性地过度使用]] ([[claude-discovers-clock]])
- CREAO的实践明确证明：Vibe Coding只能做原型验证，生产级系统需要[[harness-engineering]]——不是凭感觉调prompt，而是构建让AI稳定产出的系统。没有自动化测试、CI/CD、监控等[[ai-first-prerequisites]]的"AI First"本质上就是Vibe Coding ([[ai-first-strategy-wrong]])

### 验证的困难
- 如何确保AI生成的复杂系统符合所有业务规则和安全要求
- 传统测试方法可能无法覆盖AI引入的新类型错误

## 实践建议

### 如何开始Vibe Coding
1. **选择合适的工具**：Cursor、Claude Code等支持连贯工作流的AI编程工具
2. **从小项目开始**：用AI重写已有代码，熟悉工作流程
3. **学习表达意图**：练习用自然语言清晰描述功能需求、约束条件和质量要求
4. **建立审查流程**：即使信任AI，也要定期审查关键代码的架构和安全性

### 避免的陷阱
- **不要完全放弃理解**：即使不写代码，也要理解系统核心概念和边界
- **不要跳过测试**：AI生成的代码需要更严格的测试，尤其是边界情况
- **不要忽视代码品味**：定期重构AI生成的代码，保持系统可维护性

## 相关概念

- [[agentic-engineering]] - 在使用Agent加速的同时保持专业标准的工程纪律
- [[software-3.0]] - 以LLM为可编程计算机的新编程范式
- [[karpathy-interview-agentic-engineering]] - Karpathy关于Vibe Coding和Agentic Engineering的完整访谈
- [[ai-agent-frameworks]] - 支持Vibe Coding的AI Agent工具生态
- [[dogfooding-as-method]] - Codex团队明确区分：他们不是"凭感觉编程"，而是在系统思考和质量把控上大量投入
- [[pm-as-gap-filler]] - Vibe Coding降低门槛让更多人能"做"，PM从"规划者"变为"填空人"
- [[harness-engineering]] - 脚手架工程：Vibe Coding的对立面——一个靠系统，一个靠感觉；Vibe Coding只能做原型，脚手架工程才能做生产
- [[ai-piloting]] - AI驾驶能力：Vibe Coding的反面——凭感觉调prompt vs 系统性协作，前者靠运气后者靠纪律
- [[sensory-gap]] - Vibe Coding的隐含假设：AI拥有类人感知能力，但实际上AI在时间感等维度全盲
- [[einstein-test]] - 创造力的终极测试：vibe coding半小时做出Theme Park原型（Hassabis 17岁时花了6个月），但还没出爆款——缺的可能不是执行速度，而是[[einstein-test|发明围棋]]级别的创造力。Hassabis觉得缺的东西可能跟"craft和soul"有关，某种人类的品味和执着。他预计6到12个月内会出现用AI工具做出的有影响力的作品，最先出现的不会是完全自主的AI创作，而是某个人用AI工具实现了1000倍的生产力。([[hassabis-agi-agents-science]])
- [[role-convergence]] - 印刷机类比：Boris预言软件开发将像发短信一样自然普及。印刷机前识字率10%，之后50年出版物超千年总和，书籍成本降100倍，几百年后识字率70%。Vibe Coding是软件民主化的入口——门槛降到"会描述需求就能做软件"的程度，领域专家（会计师写会计软件）将取代纯工程师成为最合适的软件创建者。([[boris-chenyi-sequoia-ai-ascent]])

## 参考资料

1. Karpathy在Sequoia AI Ascent 2026的访谈（[[karpathy-interview-agentic-engineering]]）
2. Karpathy 2025年2月关于Vibe Coding的原始推文
3. 2026年AI编程工具对比分析（[[ai-agent-comparisons-2026]]）

> 返回门户：[[home]] | 浏览索引：[[index]]