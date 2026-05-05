# Loop调度：让Agent自主循环执行

## TL;DR

用cron调度Agent的重复任务——每分钟、每5分钟、每天——是最简单却最有效的Agent编排方式。关上笔记本，它还在跑。

## 它是什么

Loop是Agent工作流的一种模式：不是一次性给Agent一个任务，而是让它按时间间隔反复执行。Boris Cherny运行几十个Loop：一个持续看护PR（自动修复CI、rebase），一个维持CI健康（发现flaky test自动修复），一个每30分钟抓Twitter反馈聚类。([[boris-chenyi-sequoia-ai-ascent]])

它改变了Agent从"按需工具"到"持续运行服务"的性质——Agent不再等人触发，而是像后台进程一样持续运转。

## 为什么重要

Loop把Agent从"对话式助手"推进到"自主运行服务"。关键特性是**持续性**——即使人离线，任务仍在执行。Boris称"Loop就是未来"([[boris-chenyi-sequoia-ai-ascent]])。

这与[[agent-matrix]]互补：Agent矩阵解决并行度问题，Loop解决持续性问题。两者叠加，形成"数百Agent 24/7运行"的工作模式。

4.7模型已经能自发启动Loop——Boris让它做数据查询，它自己发现数据在变化，主动启动一个30分钟循环报告。当模型自己决定什么时候该循环运行，人就不再需要做编排决策。([[boris-chenyi-sequoia-ai-ascent]])

## 与其他概念的关系

- [[agent-matrix]] — Loop是Agent矩阵的持续性编排层
- [[self-healing-pipeline]] — Loop看护PR和CI是自愈流水线的具体实现
- [[harness-engineering]] — Loop减少了对脚手架的依赖，模型自主决定循环
- [[action-based-ai]] — Loop是行动派AI的持续性形态
- [[architect-operator-model]] — Boris用手机调度Loop，是架构师-操作员模型的实时版
