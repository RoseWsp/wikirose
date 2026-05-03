---
type: article
date: 2026-04-06
author: Alexander Embiricos, Romain Huet (宝玉xp 翻译)
url: https://weibo.com/ttarticle/p/show?id=2309405284728495538279
raw: raw/clips/Codex 团队如何用自己的产品构建产品.md
---

# Codex 团队如何用自己的产品构建产品

OpenAI Codex 团队50人只有1个PM，整个产品spec只有10个要点，设计师写的代码量超过6个月前的工程师——因为他们用Codex构建Codex，把自己活成了产品的最强用户。

## 核心要点

**极简spec。** Codex团队几乎不写产品规格文档，只有涉及多人协调时才写，且不超过10个要点。原则：让离金属最近的人做决策。([[minimal-product-specs]])

**双极规划。** 只做8周以内的近期冲刺，和一年以上的方向感（"vibes"），永远不做中期路线图。模型能力快速变化让中期规划变成猜测。([[dual-horizon-planning]])

**用产品建产品。** PM用Codex做"思维探索"——不是写代码，是建立心智模型，然后把理解分享给工程师。设计师现在写的代码量超过6个月前的工程师。([[dogfooding-as-method]])

**海盗船式运作。** 50-100人团队长期只有1个PM，跨职能协调极少，汇报结构极简。([[pirate-ship-team]])

**PM是填空岗位。** Alex认为PM不是领导岗位，而是填补空缺的岗位。"人才栈压缩"正在发生——每个人能覆盖更多角色。([[pm-as-gap-filler]])

**Power user拉你进未来。** 先为power user做可配置性，再为普通用户做简化。核心交互极简，让产品"隐形"，通过分层让power user自己解锁深层功能。([[power-user-pull]])

## 关键转折点

GPT-5.2 Codex在2025年12月发布，模型能力跨过"可以可靠长时间独立工作"的门槛，直接催生了Codex桌面应用。用户开始用tmux同时开18个终端窗口运行Codex，但只有1%的工程师会这样工作——如何让多Agent协作变得直觉化成了产品问题。

## 技术架构

Codex App、IDE扩展和CLI底层共用同一套开源Rust核心（Codex harness），三个产品形态共享代码和能力。Romain把Codex定位为"OpenAI整个开发者平台的入口"——不管接Imagen、Sora还是Speech-to-Speech，Codex都是起点。

## 值得追问的张力

Codex的极简管理建立在特殊条件上：**他们是自己产品的用户**。当野心是"把编码Agent带给ChatGPT的9亿用户"时，"让离金属最近的人做决策"还适用吗？产品决策的复杂度会发生质变。

## 招聘哲学

看作品不看简历，看能动性不看资历。"给我看你做了什么"取代了学历证书。入职没有任务列表，就是"欢迎，自己找事做"。

![](https://wx3.sinaimg.cn/large/66fd066bgy1ibx3rt99vyj20zk0jz42o.jpg)
![](https://wx4.sinaimg.cn/large/66fd066bgy1ibx3ppn6glj20zk0k00x7.jpg)
