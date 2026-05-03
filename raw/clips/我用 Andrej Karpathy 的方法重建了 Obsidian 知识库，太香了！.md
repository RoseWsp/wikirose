---
title: "我用 Andrej Karpathy 的方法重建了 Obsidian 知识库，太香了！"
source: "https://mp.weixin.qq.com/s?__biz=MzkwNTYzNzMzNw==&mid=2247484862&idx=1&sn=4428efe840b5f1cca883884079538844&chksm=c19b28ead39527e0b9a0b2ed4de0d17d48f5bf053145c9f04d2980b71461b09b9f3a5d703c12&poc_token=HMq80Gmjq0lbpED3Z8CUWItT0Rjm2CQlbpK71whI"
author:
  - "[[曼谈AI]]"
published:
created: 2026-04-04
description: "Andrej Karpathy 昨天发了条推文，说他现在大部分 token 消耗不是在写代码，而是在用 LLM"
tags:
  - "clippings"
---
原创 曼谈AI *2026年4月3日 21:37*

Andrej Karpathy 昨天发了条推文，说他现在大部分 token 消耗不是在写代码，而是在 **用 LLM 管理知识** 。他把原始素材（论文、文章、数据集）扔进一个目录，然后让 LLM "编译"成一个 wiki——一堆.md 文件，有摘要、有分类、有反向链接，全部由 LLM 维护，人基本不碰。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/GDjtVibHyDbHoknichQXicXOFP69m3L3I4aZL3Z52UJGkVbf3nHVmhZNGfyePkcy9SDRs3w58EoL7qk5ibn8iaPTAQBPxXQFqmERDzWvWu1wjfz4/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0)

我看完第一反应：这不就是我想要的吗？我的 Obsidian 一直是个"高级收藏夹"——文件扔进去就不管了，偶尔打开翻翻，找东西全靠记忆和搜索。30 个 markdown 文件，7 个 PDF 报告，散落在"新闻""报告""洞察""笔记"几个目录里，互相之间没有任何关联。

于是我花了一个小时，用 Claude Code 把整个 vault 按 Karpathy 的思路重建了。过程中有几个认知上的转变，比方法本身更值得聊。

## 改造：从"收藏夹"到"编译型知识库"

<svg viewBox="0 0 640 260" xmlns="http://www.w3.org/2000/svg" font-family="-apple-system, PingFang SC, Microsoft YaHei, sans-serif" role="img" aria-label="插图"><rect x="20" y="10" width="270" height="240" rx="8" fill="#fff5f5" stroke="#e0b4b4" stroke-width="1.5"></rect><text x="155" y="38" text-anchor="middle" font-size="15" font-weight="700" fill="#c53030"><tspan leaf="">Before: 高级收藏夹</tspan></text> <text x="46" y="68" font-size="13" fill="#666"><tspan leaf="">vault/</tspan></text> <text x="66" y="90" font-size="12" fill="#999"><tspan leaf="">新闻/ (8 篇日报)</tspan></text> <text x="66" y="112" font-size="12" fill="#999"><tspan leaf="">报告/ (PDF + md 混放)</tspan></text> <text x="66" y="134" font-size="12" fill="#999"><tspan leaf="">洞察/ (2 篇笔记)</tspan></text> <text x="66" y="156" font-size="12" fill="#999"><tspan leaf="">笔记/ (3 篇)</tspan></text> <text x="66" y="178" font-size="12" fill="#999"><tspan leaf="">录音/ (1 篇转写)</tspan></text> <text x="66" y="200" font-size="12" fill="#999"><tspan leaf="">论文/ (空的)</tspan></text> <text x="155" y="232" text-anchor="middle" font-size="11" fill="#c53030"><tspan leaf="">30 个文件，零关联，6 份 PDF 沉睡</tspan></text> <path d="M 310 130 L 345 130" stroke="#333" stroke-width="2" fill="none" marker-end="url(#arrowhead)"></path><defs><marker markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#333"></polygon></marker></defs><rect x="350" y="10" width="270" height="240" rx="8" fill="#f0fff4" stroke="#9ae6b4" stroke-width="1.5"></rect><text x="485" y="38" text-anchor="middle" font-size="15" font-weight="700" fill="#276749"><tspan leaf="">After: 编译型知识库</tspan></text> <text x="376" y="66" font-size="13" fill="#666"><tspan leaf="">vault/</tspan></text> <text x="396" y="88" font-size="12" fill="#276749" font-weight="600"><tspan leaf="">INDEX.md + MOC.md</tspan></text> <text x="396" y="110" font-size="12" fill="#999"><tspan leaf="">raw/ (PDF, 录音, 剪藏)</tspan></text> <text x="396" y="132" font-size="12" fill="#999"><tspan leaf="">inbox/ (待处理日报)</tspan></text> <text x="396" y="154" font-size="12" fill="#276749" font-weight="600"><tspan leaf="">wiki/ (LLM 编译产物)</tspan></text> <text x="416" y="174" font-size="11" fill="#999"><tspan leaf="">concepts/ insights/ projects/</tspan></text> <text x="396" y="196" font-size="12" fill="#999"><tspan leaf="">output/ (生成的输出)</tspan></text> <text x="485" y="232" text-anchor="middle" font-size="11" fill="#276749"><tspan leaf="">35 篇互链，6 份 PDF 全部激活</tspan></text></svg>

改造前后的 vault 结构对比

原来的 vault 结构很典型——按内容类型分文件夹：新闻、报告、洞察、笔记、论文。看起来整齐，但有个致命问题： **原始素材和提炼后的知识混在一起** 。一篇 SemiAnalysis 的 40 页 PDF 和我写的 3 段洞察笔记放在同一层级，信息密度差了一个量级，却享受同等待遇。

Karpathy 的核心设计是 **raw/ 和 wiki/ 的分离** 。原始素材是原始素材，编译产物是编译产物，中间有一个 LLM 做"编译器"。这个隐喻很精确——不是在"整理"知识，而是在"编译"知识。就像源码和可执行文件的关系。

改完之后的结构：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/GDjtVibHyDbGgsOzLLbCp7b9hm07cuxYUhrRHibozqM5iacORkzTEPTibLYicTVLX28Ahk31vlz7YPqvYHjfmwltpGic6adlvHIaLRczo4H8mAzZ0/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1)

迁移文件只花了十分钟。重头戏在下一步。

## 编译：让 LLM 把 PDF "读"成知识

<svg viewBox="0 0 640 200" xmlns="http://www.w3.org/2000/svg" font-family="-apple-system, PingFang SC, Microsoft YaHei, sans-serif" role="img" aria-label="插图"><rect x="20" y="50" width="140" height="100" rx="8" fill="#fef3c7" stroke="#f59e0b" stroke-width="1.5"></rect><text x="90" y="80" text-anchor="middle" font-size="14" font-weight="700" fill="#92400e"><tspan leaf="">raw/</tspan></text> <text x="90" y="100" text-anchor="middle" font-size="11" fill="#92400e"><tspan leaf="">PDF 报告</tspan></text> <text x="90" y="116" text-anchor="middle" font-size="11" fill="#92400e"><tspan leaf="">网页剪藏</tspan></text> <text x="90" y="132" text-anchor="middle" font-size="11" fill="#92400e"><tspan leaf="">录音转写</tspan></text> <path d="M 168 100 L 218 100" stroke="#333" stroke-width="1.5" fill="none" marker-end="url(#arr2)"></path><defs><marker markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#333"></polygon></marker></defs><rect x="226" y="55" width="170" height="90" rx="40" fill="#e0e7ff" stroke="#6366f1" stroke-width="1.5"></rect><text x="311" y="92" text-anchor="middle" font-size="14" font-weight="700" fill="#3730a3"><tspan leaf="">LLM 编译器</tspan></text> <text x="311" y="112" text-anchor="middle" font-size="11" fill="#3730a3"><tspan leaf="">提炼 / 分类 / 关联 / 链接</tspan></text> <path d="M 404 100 L 454 100" stroke="#333" stroke-width="1.5" fill="none" marker-end="url(#arr2)"></path><rect x="462" y="30" width="160" height="140" rx="8" fill="#f0fff4" stroke="#38a169" stroke-width="1.5"></rect><text x="542" y="58" text-anchor="middle" font-size="14" font-weight="700" fill="#276749"><tspan leaf="">wiki/</tspan></text> <text x="542" y="80" text-anchor="middle" font-size="11" fill="#276749"><tspan leaf="">concepts/ 概念文章</tspan></text> <text x="542" y="98" text-anchor="middle" font-size="11" fill="#276749"><tspan leaf="">insights/ 报告洞察</tspan></text> <text x="542" y="116" text-anchor="middle" font-size="11" fill="#276749"><tspan leaf="">projects/ 项目知识</tspan></text> <text x="542" y="140" text-anchor="middle" font-size="11" fill="#276749"><tspan leaf="">INDEX.md 全局索引</tspan></text> <text x="542" y="158" text-anchor="middle" font-size="11" fill="#276749"><tspan leaf="">MOC.md 知识地图</tspan></text> <text x="90" y="30" text-anchor="middle" font-size="12" fill="#999"><tspan leaf="">原始素材</tspan></text> <text x="311" y="38" text-anchor="middle" font-size="12" fill="#999"><tspan leaf="">Claude Code</tspan></text> <text x="542" y="14" text-anchor="middle" font-size="12" fill="#999"><tspan leaf="">结构化知识</tspan></text></svg>

核心流程：原始素材经过 LLM 编译，变成结构化的 wiki

raw/reports/ 里躺着 6 份 PDF——Gartner、SemiAnalysis、Omdia 的行业报告。之前只有 2 份被我手动写了读书笔记，其他 4 份下载后就没打开过。

我让 Claude Code 逐个读取 PDF，提炼成中文洞察文章。不是翻译，不是摘要，而是 **提取 3-5 个核心判断，每个判断附上论据和我的评注** 。比如 SemiAnalysis 那篇 GPU 租赁报告，40 页内容编译成一篇 800 字的文章，核心判断是：H100 租赁价格 6 个月涨了 40%，需求驱动，On-Demand 全部售罄。

4 份 PDF 同时编译，几分钟后 wiki/insights/ 多了 4 篇文章，每篇都有 frontmatter（标题、标签、日期、来源链接）和 Obsidian 反向链接。

然后是更有价值的一步：我发现这几篇报告有一个 **共同的交叉节点——推理成本** 。Gartner 在讲中美推理成本差异，SemiAnalysis 在讲 GPU 租赁价格，Omdia 在讲 OpenClaw 带来的 token 消耗爆发。于是 LLM 自动生成了一篇概念文章《推理成本》，把散落在不同报告里的数据串成了一条逻辑链。

这就是"编译"和"摘要"的区别。摘要是把每篇文章缩短，编译是把多篇文章里的知识 **重新组织成概念网络** 。

## 交互：Wiki 不是终点，是起点

知识库建好之后，我试了一件事：直接问 Claude Code 一个跨报告的问题——"GPU 租赁价格还在涨吗？对 AI 漫剧生产成本有什么影响？"

Claude Code 先读了 wiki 里 SemiAnalysis 的两篇编译文章（截至 4 月初的数据），然后联网搜了最新的市场价格做交叉验证，最后把 wiki 里的 AI 漫剧行业数据拉过来做关联分析。

结论是反直觉的：GPU 租赁涨了 40%，但漫剧生产成本反而从 2000-5000 元/分钟降到了 400 元/分钟。因为头部团队在自建算力池+用开源模型，工具链自动化降了人力成本，模型效率也在提升。 **GPU 涨价对依赖 API 的小团队是灾难，对自建算力的头部团队几乎无感。**

这个分析质量让我意外。不是因为 LLM 有多聪明，而是因为 **它有足够的上下文** 。wiki 里有行业数据、有报告洞察、有成本结构，LLM 只需要把它们连起来，再用外部搜索验证时效性。

Karpathy 说"我以为要上 RAG，但 LLM 自己维护 INDEX 文件和摘要就够了"。实测确实如此。我的 wiki 只有 35 篇文章、几万字，LLM 通过 INDEX.md（每篇文章一句话摘要）就能快速定位相关内容，根本不需要向量数据库。

<svg viewBox="0 0 640 300" xmlns="http://www.w3.org/2000/svg" font-family="-apple-system, PingFang SC, Microsoft YaHei, sans-serif" role="img" aria-label="插图"><circle cx="320" cy="150" r="60" fill="#f0fff4" stroke="#38a169" stroke-width="2"></circle><text x="320" y="145" text-anchor="middle" font-size="15" font-weight="700" fill="#276749"><tspan leaf="">Wiki</tspan></text> <text x="320" y="165" text-anchor="middle" font-size="11" fill="#276749"><tspan leaf="">35 篇 / 持续增长</tspan></text> <rect x="240" y="10" width="160" height="44" rx="22" fill="#e0e7ff" stroke="#6366f1" stroke-width="1.5"></rect><text x="320" y="37" text-anchor="middle" font-size="13" font-weight="600" fill="#3730a3"><tspan leaf="">提问</tspan></text> <rect x="470" y="128" width="140" height="44" rx="22" fill="#fef3c7" stroke="#f59e0b" stroke-width="1.5"></rect><text x="540" y="155" text-anchor="middle" font-size="13" font-weight="600" fill="#92400e"><tspan leaf="">联网验证</tspan></text> <rect x="240" y="246" width="160" height="44" rx="22" fill="#fefce8" stroke="#ca8a04" stroke-width="1.5"></rect><text x="320" y="273" text-anchor="middle" font-size="13" font-weight="600" fill="#854d0e"><tspan leaf="">综合回答</tspan></text> <rect x="30" y="128" width="140" height="44" rx="22" fill="#fce7f3" stroke="#ec4899" stroke-width="1.5"></rect><text x="100" y="155" text-anchor="middle" font-size="13" font-weight="600" fill="#9d174d"><tspan leaf="">写回 Wiki</tspan></text> <path d="M 320 54 L 320 88" stroke="#6366f1" stroke-width="1.5" fill="none" marker-end="url(#arr3)"></path><defs><marker markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#666"></polygon></marker></defs><path d="M 378 140 L 466 145" stroke="#f59e0b" stroke-width="1.5" fill="none" marker-end="url(#arr3)"></path><path d="M 466 158 L 382 160" stroke="#38a169" stroke-width="1.5" stroke-dasharray="4 3" fill="none" marker-end="url(#arr3)"></path><path d="M 320 212 L 320 242" stroke="#ca8a04" stroke-width="1.5" fill="none" marker-end="url(#arr3)"></path><path d="M 240 268 L 148 195" stroke="#ec4899" stroke-width="1.5" fill="none" marker-end="url(#arr3)"></path><path d="M 148 148 L 258 148" stroke="#38a169" stroke-width="2" fill="none" marker-end="url(#arr3)"></path><text x="338" y="78" font-size="10" fill="#666"><tspan leaf="">读取相关文章</tspan></text> <text x="420" y="133" font-size="10" fill="#666"><tspan leaf="">搜最新数据</tspan></text> <text x="420" y="175" font-size="10" fill="#999"><tspan leaf="">更新过时信息</tspan></text> <text x="338" y="232" font-size="10" fill="#666"><tspan leaf="">生成分析</tspan></text> <text x="170" y="245" font-size="10" fill="#666"><tspan leaf="">有价值的结果</tspan></text> <text x="188" y="138" font-size="10" fill="#38a169" font-weight="600"><tspan leaf="">知识增值</tspan></text></svg>

知识复利循环：每次提问都在给知识库增值

更关键的是最后一步： **这个分析本身被写回了 wiki** 。一篇新的概念文章《漫剧工具推理经济学》被创建，链接回了推理成本、行业全景、GPU 租赁报告。我的每一次提问都在给知识库增值。Karpathy 说的"explorations always add up"，用起来确实是这个感觉——知识在滚雪球。

## 几个改变认知的点

### 知识管理的主体变了

传统流程是：人读素材 → 人写笔记 → 人建链接 → 人维护索引。Karpathy 的模式里，这四步全是 LLM 做的。人只做两件事： **往 raw/ 扔素材，对 wiki 提问题** 。

这意味着知识管理的瓶颈不再是"我有没有时间整理笔记"，而是"我有没有在持续喂入新素材"和"我有没有问出好问题"。投入的性质变了。

### "编译"和"存储"是两回事

Notion、语雀、Obsidian，大部分人的用法是"存储"——把信息放进去，需要时搜出来。问题在于存进去的原始信息和你需要的知识之间有一个巨大的 gap，这个 gap 以前靠人肉填（写读书笔记、做思维导图），现在可以让 LLM 填。

一份 40 页的 SemiAnalysis PDF 在 raw/ 里躺着，对我的价值接近零。经过 LLM 编译成 800 字的洞察文章，提炼出 4 个核心判断、标注了和其他文章的关联，它的价值瞬间变成了可查询、可关联、可复用的知识节点。

### 小规模下不需要 RAG

我一开始以为要搞向量数据库、embedding、相似度检索这一套。实际跑下来，在几十篇文章、几万字的规模下，一个 INDEX.md（每篇一句话摘要）加上 MOC.md（按主题分组的知识地图）就完全够了。LLM 读一遍 INDEX 就知道该去读哪些文章。

当然，如果 wiki 膨胀到几百篇文章、上百万字，可能确实需要更高级的检索。但绝大多数人的个人知识库到不了那个规模。 **先跑起来再优化，是比架构完美但从不开始更好的策略。**

### Wiki 是起点，不是牢笼

刚建好的时候我担心一个问题：LLM 会不会只在 wiki 里打转，变成一个封闭系统？实际使用发现不会。问"GPU 租赁价格还在涨吗"，它会先读 wiki 里的已有判断，然后主动联网搜最新数据做验证。如果外部信息和 wiki 有冲突，它会提示并更新。

wiki 提供的是 **积累的上下文** ，外部搜索提供的是 **实时的事实** 。两者组合比任何一个单独使用都强。这跟人的知识结构其实一样——你的认知框架帮你快速理解新信息，新信息反过来修正你的认知框架。

## 实操建议

如果你也想试，不需要从零搭建。拿你现有的 Obsidian vault 改就行：

**第一步** ：建 `raw/` 和 `wiki/` 两个目录，把原始素材和你写的笔记分开。

**第二步** ：建一个 `INDEX.md` ，把 wiki 里每篇文章用一句话概括。这是 LLM 的查询入口。

**第三步** ：拿一份你一直没读完的 PDF 或长文，让 LLM 编译成一篇 wiki 文章。感受一下"编译"和"摘要"的区别。

**第四步** ：对 wiki 问一个需要跨文章回答的问题。看看 LLM 能综合到什么程度。

**第五步** ：把有价值的问答结果写回 wiki。开始积累复利。

工具方面，我用的是 Claude Code 直接操作本地文件。Obsidian 只是"前端"——浏览 wiki、看 Graph View 的知识关联图。所有的读写、编译、索引维护都交给 LLM。

一个小时，30 个散乱文件变成了 35 篇互相链接的知识网络，6 份沉睡的 PDF 全部激活，还多了 2 篇从提问中长出来的概念文章。这个投入产出比，确实太香了。

**微信扫一扫赞赏作者**

继续滑动看下一个

曼谈AI

向上滑动看下一个