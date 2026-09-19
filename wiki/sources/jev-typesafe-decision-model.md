---
type: report
date: 2026-09-15
author: mindstudio.ai（二手汇编）＋ 本次 ingest 的一手核查
url: https://www.mindstudio.ai/
raw: raw/blog/Jev Explained Typesafe AI's Non-Autoregressive System-1 Model.txt
---

# Jev：一个拒绝说话的 AI，和它 48 小时内的公开压力测试

**TL;DR** TypeSafe AI 在 2026-09-15 发布 Jev——一个不做自回归、不生成文本、只输出**带校准置信度的类型安全决策**的模型，官方自报快 193.6 倍、便宜 444.6 倍。它的对手不是 GPT-6，是 `if` 语句。但真正有信息量的不是发布本身，而是**社区在 48 小时内把它拆成了"可复刻的壳"和"不可复刻的芯"两层**。

## 事实核查：raw 原文的三处错误

本页的原材料（`raw/blog/` 里那篇 mindstudio.ai 汇编稿）是二手 SEO 解释器，有三处硬伤。**以下为本次 ingest 的一手核查结论，与 raw 冲突时以本节为准：**

| raw 原文 | 实际情况 |
|---|---|
| "Diego Almeida" | **Diogo Almeida** —— 名字写错了。前 OpenAI 研究员，GPT-4 贡献者，InstructGPT/RLHF 论文共同作者，OpenAI 官方将其列入 "Foundational RLHF and InstructGPT work"。佐治亚理工毕业，曾任职 Google Brain，2024 年离开 OpenAI |
| "快约 100 倍、便宜 100 倍" | 官方口径是 **快 193.6 倍、便宜 444.6 倍**（公司自建 workflow eval，自认接近现实收益上限）。raw 把数字砍了一半 |
| 未提及 | 联合创始人 **Erik Gafni、Sasha Sheng**；**4000 万美元种子轮**（DCVC 领投，估值约 2 亿）；隐身研发两年；**模型名 Jev 取自杰文斯（William Stanley Jevons）** |

另外 raw 说演示是 Minecraft / 自动驾驶 / Subway Surfers / 无人机，一手报道里官方演示是**实时打 DOOM**（每秒约 10 次决策，约 $7/小时）。raw 里那些是社区自建 demo。

## 它到底是什么

**输入**：一段程序状态的文本描述 + 预先定义好的问题。
**输出**：三个原语之一，**都带置信度**。

| 原语 | 干什么 |
|---|---|
| **Choice** | 从最多 **255** 个预设选项里选一个，返回概率分布 |
| **Score** | 在指定数值区间里打分 |
| **Noul** | 是/否的概率（calibrated boolean） |

255 是 `uint8`——**动作空间就是一个字节**。

定价：输入 **$0.042/百万 token**，**输出免费**（约 $0.0004/次决策）。延迟 **70–500ms**。

## 三个论点，按锋利度排

### 1. 公司名就是论点：类型安全即抗幻觉

官方宣称 **0% 幻觉**，但被反复澄清——这是**构造性保证，不是实测数据**。它只保证输出在结构上不可能跑出 schema，**不保证判断内容正确**。一个格式完全正确的错误答案仍然是错的。

代价很硬：**模型只能在已枚举的动作里选，无法发现你忘了列进去的那个动作。** 详见 [[typed-decision-interface]]。

### 2. 定价结构暴露了架构

输出免费、输入收费，因为一次决策只有几个 token，而世界描述很长。翻译过来：**思考免费，因为根本没有思考；账单是"看一眼世界"的钱。**

推论：想让 Jev 变强，不能给它更多思考预算，只能给它更好的世界描述。**负担从模型搬到了环境编码和动作枚举上。**

### 3. 核心：从 RLHF 到 RLCD

Almeida 的判词是 **"RLHF 是一条弯路"**：

> RLHF 优化的是"人类评分者更喜欢"，不是"更准确"。所以**过度承诺是被设计出来的特性**……无论模型错得多离谱，它们看起来都会是对的。

他还有一句被引用最多的话：

> 我们有瓶中之闪电，却毫无用处……问题是我们一直在优化人类语言，**但计算机说另一种语言**。

于是有了 RLCD（Reinforcement Learning for Calibrated Decisions）——优化**校准**：说 70% 把握，长期就真有七成对。训练数据**全部为合成数据**，Almeida 称之为"我一生中最好的赌注之一——比 RLHF 还好"。

分析见 [[calibrated-decisions]]。

## 复刻压力测试（本页最重要的一节）

发布后 48 小时内，社区冒出一批开源复刻。**没有一个复刻了 Jev 的模型或训练方法**——它们复刻的是**接口**。至少一个项目在发布后补加了商标免责声明。

一句流传最广的调侃：**"你们 stealth 开发两年，我 stealth 开发两小时。"**

关键分界线：

- **接口层**（typed decision + 并行采样）：**两小时可复刻** ✅
- **校准层**（置信度真的对应频率）：**无人复刻** ❌

所有复刻都用 `softmax(logits)` 当置信度，而 softmax 给的是**相对排序**，不是**校准概率**——有人总结得精准：reading logits is **a ranking with a gap**, not calibrated confidence。

**所以复刻潮不是打脸，是精确圈出了 Almeida 真正的赌注在哪。** 详见 [[jev-clone-stress-test]]。

准确率参考：`TheoLeeCJ/openjev` 自测在 102 行 TypeSafe 子集上，Qwen3.5 4B 拿到 **0.845** modal agreement，对上已发布 Jev 的 **0.883**。浏览器内小模型掉到 40.7–63.7%。

## 该打折扣的地方

- **所有数字是自报的**，对照基线是竞品预测平均值，公司自认 193.6x/444.6x 是"接近现实收益上限"的高端值
- **没发论文、没放权重、没说参数量、没公开架构，RLCD 的 reward function 未公开**
- **第三方独立测试稀少**；传有测试显示真实 A/B 判断准确率约 64.5%（来源不明确，谨慎采信）
- **没有具名客户，没有收入披露**，定价看起来像在打价格战
- 采用速度倒是创纪录：Vercel AI Gateway 上 24 小时内约 **13%** 付费团队接入

**信号很强，证据很弱。**

## 关联

[[calibrated-decisions]] [[typed-decision-interface]] [[jev-clone-stress-test]] [[jevons-paradox-inference]] [[system-zero]] [[capability-boundary]] [[decision-hierarchy]] [[agent-output-verification]] [[agent-native-tooling]] [[harness-engineering]] [[general-specialized-architecture]] [[alphafold-breakthrough-conditions]] [[experience-incompressible]] [[bounded-rationality]] [[生命]]

### 按 [[生命]] 的轴重读

Jev 的意义不在"AI vs 人"这条轴上，在**有过程 vs 无过程**这条轴上：

- 它**一次前向传播出结果**，内部没有序列、没有展开、没有时间——不是"缺少体验的 AI"，是**内部没有过程**
- 它的过程被**外包**给组件：动作枚举清单、状态编码、外部循环，**都是有人走过过程之后留下的痕迹**（组件是痕迹的固态）
- 校准是它在**结果侧**唯一能给出的诚实；类型安全是结果侧的约束；输出免费是过程被移除的定价证据
- 复刻潮因此有了答案：**壳是形态（可抄），芯是那段路留下的痕迹**——而痕迹是**存在过的证明**，别人的证明证明不了你存在。所以芯不可抄不是因为它难，是**逻辑上不可抄**。见 [[jev-clone-stress-test]]
- 再往下：痕迹的意义是**内向的**（你存在过的证明）；在世间重不重要，**无所谓**（天地不仁，以万物为刍狗）。同一句话在《生命》第六幕已经出现过一次——"于是无所谓"

### 一手来源

- [至顶网｜Jev 模型创始人：RLHF 是一条弯路，下一个时代绝不是 Claude Code 时代](https://www.zhiding.cn/gaofei/2026/0919/3199854.shtml)
- [腾讯新闻｜ChatGPT 早期研究者做了一个"不会说话"的 AI，Jev 真是新范式吗？](https://news.qq.com/rain/a/20260918A058BW00)
- [36Kr｜刷屏爆火的"不说话"AI Jev 真的是 AI 新范式吗？](https://eu.36kr.com/zh/p/3988164509711361)
- [NYU Shanghai RITS｜TypeSafe AI Launches Jev](http://rits.shanghai.nyu.edu/ai/typesafe-jev-system-one-model/)
- [Yahoo/TechCrunch｜A new kind of AI model from a ChatGPT inventor is thrilling developers](https://tech.yahoo.com/ai/chatgpt/articles/kind-ai-model-chatgpt-inventor-184930808.html)
- [凤凰网｜2400 万人围观，前 OpenAI 研究员做了个「闭嘴」模型](https://i.ifeng.com/c/8wUdggBSwgU)
