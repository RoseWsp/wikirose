# 推理的杰文斯悖论

**TL;DR** 推理可能永远不会真正免费。杰文斯悖论：效率提高→需求增加→消耗掉所有效率收益。百万级Agent集群、并行思考都会吃掉算力，即使能源成本趋零，芯片制造仍是瓶颈。

Hassabis在YC访谈中回应"推理成本趋近零"的假设：推理可能永远不会真正免费。他引用了杰文斯悖论——1865年经济学家William Stanley Jevons观察到蒸汽机效率提高后煤炭消费量不降反升，原始语境是煤炭效率与消费的关系。([[hassabis-agi-agents-science]])

## 吃掉算力的方式

- **[[agent-matrix|百万级Agent集群]]**协同工作
- **单Agent多方向并行思考**然后综合结果
- **更长的思维链**和更深的推理

即使通过可控核聚变或超导等材料科学突破将能源成本降到接近零，芯片的物理制造仍然是瓶颈。至少在未来几十年内，推理端仍然会有配额限制。Hassabis同时在做建前沿模型（Gemini）和用AI做科学（AlphaFold、Isomorphic Labs）两件事，这让他的判断比纯模型派或纯应用派更有参考价值。([[hassabis-agi-agents-science]])

## 对工程的意义

这个判断影响了多个工程决策：

- [[harness-engineering|脚手架工程]]中的Agent预算管理不只是成本优化，而是长期约束
- [[agent-matrix]]的规模扩展不会因为推理降价而消失上限
- 小模型蒸馏（Hassabis说前沿模型半年到一年后同等能力出现在边缘级小模型上）是应对推理配额的关键策略

## 命名致敬：一个叫 Jev 的模型

2026-09-15，TypeSafe AI 发布的决策模型直接叫 **Jev**——取自 William Stanley Jevons。官方希望"智能判断"足够便宜后被大规模嵌入软件。这不只是命名趣味，是把杰文斯悖论当成了**商业计划书**：模型本身必须便宜到 100 倍，需求才会涨 100 倍。输入 $0.042/百万 token、输出免费，就是这份赌注的定价形态。([[jev-typesafe-decision-model]])

这也给本页的判断补了一个反面注脚：Hassabis 说推理可能永远不会真正免费（因为需求会吃掉效率收益），而 Jev 正是**主动把那部分收益让出去换取调用量**的一方——它赌的不是省算力，是把判断变成像电力一样的基础消耗。谁赌对，取决于推理配额最终卡在哪里。([[jev-typesafe-decision-model]])

## 与其他概念的关系

- [[agent-matrix]] — Agent矩阵的规模受推理配额约束
- [[harness-engineering]] — 脚手架工程需要为推理配额做预算
- [[continual-learning]] — 持续学习可能减少重复推理的需求，是对杰文斯悖论的一个缓解路径
- [[general-specialized-architecture]] — 推理配额限制强化了通用+专用分层的必要性——专用系统更高效地使用算力
- [[machine-economy]] — 机器经济中杰文斯悖论更为尖锐：AI运营的公司越多，推理需求越大，算力越紧张——效率提升不会降低总消耗（[[jack-clark-ai-self-construction]]）
- [[typed-decision-interface]] — Jev 把成本砍到输出免费、输入 $0.042/百万 token，是"用效率换调用量"的极端定价实验
- [[calibrated-decisions]] — 校准过的判断才敢被高频自动调用，是杰文斯悖论在决策层的前置条件
