# Agent-Native Tooling

**TL;DR** — 当Agent成为代码的主要作者，工具和语言应该为Agent而非人类优化：冗长胜过简洁，严格胜过宽容，形式化胜过可读。我们会抵触，然后像Facebook工程师从PHP切到Hack一样，被环境推着接受。

## 可读性时代的终结

编程语言的全部演进史就是一部"让人更容易读"的历史：汇编→C→高级语言→Python/Ruby。Python的缩进规则不是技术需要，是可读性约定——由语言自身强制执行。Ruby的语法刻意接近自然语言，柔软、宽容。TIOBE指数衡量的是工程师想读写什么，不是什么技术最优——几十年来，这两者是同一件事。

不仅是语言，工具也遵循同一逻辑：错误信息写给人看，输出格式为终端阅读优化，类型系统被做成可选或宽松以减少人类作者的摩擦。一切都是为坐在键盘前的人优化的。

当Agent成为主要代码作者，为人类可读性优化就是在为错误的消费者设计。([[venturini-code-never-for-machines]])

## 两种优化目标

| 维度 | 人类优化 | Agent优化 |
|------|---------|----------|
| 输出 | 简洁、同情心、叙事性 | 完整、结构化、机器可解析 |
| 类型 | 宽容、可选、减少摩擦 | 严格、强制、信息密度最高 |
| 错误 | 友好提示、静默修复 | 大声失败、精确诊断 |
| 契约 | 隐式约定、文档 | 显式声明、形式化规约 |

Agent不需要训练轮。冗长和吹毛求疵对人类是摩擦，对Agent是资产。

## Hack先例：环境驱动迁移

Facebook的Hack是先例：Julien Verlaguet创建的逐步类型化、严格注解的PHP替代品——比PHP更冗长更不友好更精确。工程师强烈抵抗，要逃逸舱、要豁免、要延期、要帮助迁移代码。但组织守住底线——CI流水线逐步收紧，更严格检查，更少容错，不提供选择退出。阻力不是被说服消解的，是环境让留在PHP上越来越难，最小阻力路径慢慢变成了遵从。

关键洞察：Hack比PHP严格，不是因为技术上有必要，而是因为Facebook的规模（数千工程师维护数亿行代码）需要不同的工具特性——PHP是为单人开发者快速写网页优化的，不是为大规模团队协作优化的。同样的逻辑适用于Agent：Python是为人类可读性优化的，不是为Agent可解析性优化的。([[venturini-code-never-for-machines]])

同样的模式会重演：Agent-native的工具按人类标准写起来更差，而且确实更差。这是刻意优化，不是设计失败。不适感就是目标。

## 工具分叉

Venturini预期两条路线：

1. **继续优化人类作者**——永远会有人类作者
2. **以Agent为主要消费者**——严格、冗长、形式化、敌视歧义

SkipLabs的SKJS是信号：TypeScript兼容但sound，对人类更难，对Agent更好。反应式运行时强制显式依赖契约——手写觉得过度工程，Agent推理依赖关系时刚好。

## 与wiki其他概念的关系

- [[agent-output-verification]]：验证体系是本文的姊妹篇——"输出不需要人读"和"输入不需要人读"是同一转变的两面
- [[harness-engineering]]：脚手架为Agent构建约束环境，Agent-native工具为Agent构建原生工作介质
- [[architect-operator-model]]：当Agent承担操作员角色，工具应服务于操作员（Agent）而非架构师（人类）
- [[software-3.0]]：Software 3.0以LLM为计算机——语言应服务于计算机（LLM）而非人类程序员
- [[agentic-engineering]]：工程纪律需要适应新工具——从"代码可读性"转向"验证完备性"
- [[self-healing-pipeline]]：当Agent-native工具大声失败，自愈流水线可以更快捕获和修复
- [[compulsive-capability-use]]：Agent-native工具"吹毛求疵胜过宽容"的设计是对强迫性使用的天然制衡——当系统出错时大声失败，等于在工具层面阻止了Agent对新能力的失控性扩散
- [[sensory-gap]]：感知缺失意味着Agent-native工具不能假设Agent拥有人类直觉（如"这个错误不重要"），必须显式编码所有判断
- [[action-based-ai]]：MCP是Agent获取工具权限的首选路径——Boris明确说"对知识工作来说，答案永远是最简单的那个：MCP"。MCP连接器让Agent直接接入Salesforce、Google Docs等云端工具，computer use是兜底方案。对模型来说，MCP、CLI还是API本质上都只是token。([[boris-chenyi-sequoia-ai-ascent]])

> 核心来源：[[venturini-code-never-for-machines]] | 姊妹概念：[[agent-output-verification]]
