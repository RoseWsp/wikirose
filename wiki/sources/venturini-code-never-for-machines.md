---
type: article
date: 2026-03-23
author: Hugo Venturini
url: https://skiplabs.io/blog/future_of_tools_for_ai
raw: raw/blog/Code Was Never for Machines — Until Now.md
---

# Code Was Never for Machines — Until Now

**TL;DR** — 编程语言的全部演进史就是一部"让人更容易读"的历史。现在Agent成了代码的主要作者，工具和语言应该为Agent而非人类优化。我们会抵触这个转变——然后像Facebook工程师从PHP切到Hack一样，被环境推着接受它。

## 可读性时代的终结

每一次编程语言的跃进本质上都是可读性跃进：汇编→C→高级语言→Python/Ruby。Python的缩进规则不是技术需要，是可读性约定。Ruby的语法刻意接近自然语言。TIOBE指数衡量的是工程师想读写什么，不是什么技术最优。几十年来，这两者是同一件事。

不再了。当Agent成为主要代码作者，优化人类可读性就是在为错误的消费者设计。

## Hack的先例

Julien Verlaguet在Facebook创建Hack——一个逐步类型化、严格注解的PHP替代品。Hack比PHP更冗长、更不友好、更精确。工程师强烈抵抗：要逃逸舱、要豁免、要延期。但组织守住底线——CI流水线逐步收紧，更严格检查，更少容错，不提供选择退出。阻力不是被说服消解的，是环境让留在PHP上越来越难，最小阻力路径慢慢变成了遵从。

## Agent不需要训练轮

Agent需要的是人类不需要的、和人类需要的Agent给不了的东西：

- **冗长胜过简洁**——长、精确、无歧义的工具输出比短小精悍的人类友好输出更容易解析
- **吹毛求疵胜过宽容**——系统出错时大声、具体地失败，而不是静默类型强转或吞错
- **强类型不是护栏是信息**——类型是描述"代码应该做什么"的信息密度最高的方式

人类要简洁、同情心、叙事性。Agent要完整、结构化、机器可解析。这两个优化目标几十年来被压缩为一个，因为读者一直是人类。

## 工具分叉

Venturini预期工具将分化为两条路线：

1. **继续优化人类作者**——永远会有人类作者
2. **以Agent为主要消费者**——严格、冗长、形式化、敌视歧义

SkipLabs的SKJS类型检查器在标准TypeScript不sound的地方sound——对人类更难，对Agent更好。反应式运行时强制显式依赖契约——手写代码觉得过度工程，Agent推理"什么依赖什么"时刚好。

## 为什么会抵触，为什么还是会做

抵触的原因和Facebook工程师抵触Hack一样——新工具按人类标准写起来更差，而且确实更差。这不是设计失败，是为不同消费者做的刻意优化。不适感就是目标。

但系统级论证压倒一切：如果Agent生成大部分代码，而它们使用的工具仍然围绕人类可读性设计，就是在让Agent在为别人优化的介质中工作，留下巨大能力空白。

## 关联

- 核心概念[[agent-native-tooling]]：为Agent而非人类优化的工具与语言
- 上篇[[venturini-agent-output-compiler]]建立了"验证替代审查"的框架，本文推进到"工具本身也需要重新设计"
- 编译器类比的延伸：编译器输出不需要人读→Agent输出不需要人读→Agent的输入工具也不需要人读
- 与[[harness-engineering]]互补：脚手架为Agent构建约束环境，Agent-native工具为Agent构建原生工作介质
- 与[[architect-operator-model]]呼应：当Agent承担操作员角色，工具应该为操作员（Agent）而非架构师（人类）优化
- 与[[software-3.0]]深层连接：Software 3.0以LLM为计算机，语言应服务于LLM而非人类

> 来源：[[venturini-code-never-for-machines]] | 前篇：[[venturini-agent-output-compiler]]
