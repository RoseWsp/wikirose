---
name: goal-driven-agent
description: 从Task-Driven到Goal-Driven的认知跃迁：解决执行问题→解决迭代问题，有限自治而非更放权
metadata:
  type: concept
  foundation: [bounded-rationality, contradiction-dialectics]
---

# Goal-Driven Agent

**TL;DR** Task-Driven解决执行问题，Goal-Driven解决迭代问题。Goal-Driven不是更放权，是更强约束下的有限自治。

## Task-Driven的天花板

[[zhiyuanfu-ai-agent-exploration]]的24h打工人系统能24小时执行任务，但更高层的判断仍然依赖人：

- 现在最值得做什么？
- 哪个方向应该继续推进？
- 遇到阻塞时该换路径还是等待？
- 哪些问题值得主动探索？

**24h在线，不等于24h迭代。** 只要任务还需要人持续供给，人仍然是瓶颈。

## Goal-Driven的5个前提

很多人不敢放手让Agent自主推进，担心它跑偏、浪费token、做无效工作。这些担心都成立：

1. **目标必须清晰** — 不是模糊愿望，而是可推进、可判断的目标表达
2. **边界必须清晰** — 哪些能做，哪些不能做，资源上限是什么
3. **状态必须可见** — 当前做到哪一步，卡在哪，为什么卡
4. **过程必须留痕** — 否则无法知道为什么成功，也无法知道为什么失败
5. **权限必须可控** — 它到底能调用哪些工具，能写到哪里，谁来兜底

只有在这5个前提成立时，自主推进才是资产；否则只会把错误放大得更快。

## 共享状态：STATE.yaml

多Agent协作时，主Agent本身变成新瓶颈——上下文越来越重、通信越来越慢、单点故障。更务实的做法是用共享状态来协调：每个Agent自己读取状态、写回进度，主会话只负责高层目标和验收。

```
goal: "优化搜索模块响应速度，P95从800ms降到200ms"
constraints:
  - "不修改已有API契约"
  - "每日API成本不超过$5"
agents:
  profiler:
    status: "completed"
    summary: "瓶颈定位在DB全表扫描"
  backend_dev:
    status: "in_progress"
    current_step: "为热点查询添加Redis缓存"
```

## 与wiki其他概念的关系

- [[harness-engineering]] — Goal-Driven是脚手架工程的最高形态：脚手架从外部护栏进化为内部治理结构
- [[bounded-rationality]] — 5个前提是有限理性的Goal-Driven版：不可能完美自治，只能在约束内有限自治
- [[agent-matrix]] — Agent矩阵的进化方向：从人派活的矩阵到目标驱动的自组织矩阵
- [[loop-scheduling]] — Loop是Task-Driven的自动化，Goal-Driven是Loop之上的自主迭代
- [[clarity-before-automation]] — Goal-Driven把"先清晰"推到极致：目标、边界、状态、留痕、权限——五个维度都必须清晰
- [[contradiction-dialectics]] — "更强约束下的有限自治"是对立统一：自治和约束不是矛盾的，约束是自治的前提条件
- [[sdd]] — SDD是Task-Driven的方法论，Goal-Driven是SDD成功运行后的下一站
- [[practice-epistemology]] — Task-Driven是"实践→认识"的第一趟，Goal-Driven是"认识→再实践"的自主螺旋
