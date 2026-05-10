# 生成器-评估器循环 (Generator-Evaluator Loop)

**TL;DR** 受GAN（生成对抗网络）启发的多Agent架构：一个Generator Agent负责产出，一个Evaluator Agent负责评判，两者迭代循环驱动质量持续提升。

## 这意味着什么

Anthropic Labs的Prithvi Rajasekaran发现，AI Agent的一个根本问题是**自我评估偏差**——当被要求评估自己的工作质量时，Agent倾向于自信地给出好评，即使对人类观察者来说质量明显平庸。这在主观任务（如设计）中尤为突出，但在可验证任务中同样存在。

解耦做法事的Agent和评判的Agent被证明是一个"强有力的杠杆"——调优一个独立的Evaluator使其保持怀疑，比让Generator批判自己的工作要容易得多。一旦外部反馈存在，Generator就有了可以迭代的具体目标。([[anthropic-harness-design]])

## 工作原理

```
Generator → 产出 → Evaluator（Playwright点进页面QA）→ 评分+批评 → Generator迭代
                                    ↑
                             评分标准（编码化的判断维度）
```

### 前端设计场景

Evaluator使用Playwright MCP主动导航到页面、截图、仔细研究实现，然后按四个维度评分：

1. **Design Quality** — 设计是否构成连贯的整体而非部件的集合
2. **Originality** — 是否有自定义决策，还是模板布局和AI生成模式
3. **Craft** — 技术执行：排版层级、间距一致性、色彩和谐、对比度
4. **Functionality** — 可用性：用户能否理解界面、找到主要操作、完成任务

权重倾斜设计和原创性（Claude已在Craft和Functionality上默认表现良好），明确惩罚AI生成常见的"紫色渐变+白色卡片"模式。每次迭代5-15轮，全程可长达4小时。在荷兰艺术博物馆案例中，第10轮Generator废弃了之前的全部方案，重新想象为3D空间体验——从单次生成从未见过的创造性飞跃。

### 全栈编码场景

三个角色：

- **Planner**：将1-4句话的prompt扩展为完整产品spec，要求对scope保持雄心，聚焦产品上下文和高层技术设计而非详细实现细节。被要求寻找将AI功能编织进产品spec的机会。
- **Generator**：按sprint工作，每次从spec中选取一个feature。使用React/Vite/FastAPI/SQLite技术栈，每个sprint结束时自我评估。
- **Evaluator**：用Playwright MCP点进运行中的应用，像用户一样测试UI功能、API端点和数据库状态。每个标准有硬性阈值，低于阈值sprint失败，Generator收到详细反馈。

## Sprint Contract机制

在每次sprint开始前，Generator和Evaluator协商"done"的定义：Generator提出要构建什么以及如何验证成功，Evaluator审查提案确保方向正确。两者迭代直到达成一致。沟通通过文件进行。这保证了工作忠实于spec，又不会过早过度指定实现细节。

## Evaluator调优经验

出厂的Claude是一个糟糕的QA Agent——它会识别出真正的问题，然后说服自己"这没什么大不了的"并批准工作。它也倾向于表面测试而非探索边界情况。调优循环是：读Evaluator日志→找到评价与人类判断不一致的例子→更新QA prompt。需要多轮迭代。

## 效果数据

| 维度 | Solo Agent | 三Agent Harness |
|------|-----------|-----------------|
| 复古游戏制作器 | 20分钟/$9，核心玩法不可用 | 6小时/$200，核心玩法可玩 |
| DAW音乐工作站 | N/A | 4小时/$124.70，完整功能 |
| 关键Feature | 中心功能不可用 | 所有核心功能可用 |

## Opus 4.6后的简化

Opus 4.6去除了对Context Reset的需求、去除了Sprint结构（模型可原生处理长任务）、Evaluator改为单次通过（而非每sprint评分）。关键在于：Evaluator的价值取决于任务是否超出了模型可靠独立完成的能力边界——边界之内Evaluator是多余开销，边界之外则提供真实的提升。

## 关联

- [[harness-engineering]] — 脚手架工程是Generator-Evaluator Loop的上层框架
- [[agent-failure-modes]] — Generator-Evaluator Loop解决的核心问题：自我评估失败
- [[context-architecture]] — Sprint Contract是上下文架构在交互层面的实现
- [[agent-output-verification]] — Evaluator的功能等价于验证流程自动化
- [[anti-rationalization]] — Evaluator防Generator合理化跳过关键步骤
