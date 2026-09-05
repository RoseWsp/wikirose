# 入口迁移

## TL;DR

用户现在不是先打开你的 App，而是先打开 Agent。购买决策发生在 Agent 对话里，你的详情页就变成了 Agent 的数据源。最诚实的信号是作者本人：宝玉自己写的 BaoCut，现在他都不打开它的界面了——Codex 里丢个视频链接，说一句"帮我翻译这个字幕"，它调 BaoCut 命令行翻完，人只确认。

## 从"打开 App"到"打开 Agent"

宝玉买吸树叶机器没逛电商，直接问 ChatGPT 对比选型，把看中的一款发给它，它用"吹叶吸叶参数两回事、裸机不含电池、电池生态锁定"说服了他——"比我刷商品页深得多"。**购买决策发生时，决策发生在 Agent 对话里，而不是详情页上。** 产品设计必须面对这个现实：你的详情页、你的 GUI，先是 Agent 的界面，然后才是人的。([[baoyu-ai-native-thinking]])

## 设计要照顾两头

Agent 操作方便，人确认方便。"确认不了的东西人不会放心用"——所以 GUI 没有消失，但它从"操作界面"退化成"确认界面"：BaoCut 从 GUI 变成命令行工具加 Skill 文件，整个流程 Agent 自主完成，人只在两头：输入视频，最后验收。

## 与 Agent Native 产品的关系

Mike Krieger 的 Agent Native 定义是产品维度："用户能做的，AI 代理也应该能做"——产品要**对 Agent 开放**。[[agent-native-tooling]] 讲的是工具/格式为 Agent 优化（语言、错误信息、契约），入口迁移讲的是**入口本身**从人迁移到 Agent：产品不只需要"Agent 也能操作"，更需要承认 Agent 可能是第一用户，产品主页、详情页、API 都要按"Agent 先读、人后读"来设计。

## 连接

- [[agent-native-tooling]] — 工具为 Agent 优化（格式/语言），入口迁移是产品/入口为 Agent 优化
- [[ai-native-thinking]] — "把 App 做成 Agent 的插件"是重设计阶段的三条准则之一
- [[action-based-ai]] — 从聊天到行动：Agent 不只是回答，而是代替你完成购买/开发动作
- [[distribution-bottleneck]] — 入口迁移改变分发渠道：SEO 对象从人变成 Agent，详情页是 Agent 的数据源
- [[software-no-moat]] — 当界面不再被打开，功能型界面的壁垒消失得更彻底

来源：[[baoyu-ai-native-thinking]]
