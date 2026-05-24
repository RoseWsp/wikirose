---
type: podcast
date: 2026-05
author: Mike Krieger (Instagram联合创始人/Anthropic Labs产品负责人) × Dan Shipper (Every)
url: https://every.to
raw: raw/blog/为什么 AI 越强，产品经理越容易做出垃圾？Instagram 创始人给出了答案.md
---

# Mike Krieger × Dan Shipper：为什么AI越强，产品经理越容易做出垃圾

## TL;DR

AI让执行变廉价，但判断力反而更容易退化——工具越强，越容易跳过那些看似低效但实际上在建立直觉的思考过程。Mike Krieger从Instagram到Anthropic Labs的一手经验验证了一个反直觉的结论：**搭建变简单了，但做出好产品并没有**。

## 核心论点

### 搭建变简单了，但做出好产品并没有

Mike让Claude重建Bourbon（Instagram前身），2小时搞定功能齐全——还自动加了滤镜。但紧接着说：**AI擅长往产品里加功能，但不擅长判断该砍掉什么**。这种判断力来自长时间跟真实用户打交道积累的直觉，AI帮你跳过了建立直觉的过程。

### 室内树效应

Dan的比喻：室内种树没有风吹，长得快但树干不结实。Mike的亲身经历：V1阶段严重过度开发，每个功能看起来只是一个小PR的工作量，结果做出功能矩阵，测试和解释都困难。他还引用了"直接被扔进电视剧大结局"的比喻——没有前面几集的铺垫，根本不知道发生了什么。

### 重写不再可怕

以前铁律"不要轻易重写代码"需要重新审视——重写可能只需几天，模型还能帮你对比新旧版本。但重写的价值取决于你从V1中学到了什么，如果跳过了"从失败中提取认知"这一步，低成本重写就变成低成本重复犯错。

### Agent Native

产品里用户能做的，AI代理也应该能做。Mike用"Claude说让我告诉你怎么手动添加"作为反面案例——产品假设里根本没有Agent的位置。Claude AI是2024年的产品，Claude Code是2025年的产品，Agent Native程度有明显差距。

### 测试Agent Native产品

传统端到端测试不管用了——Claude在应用里跟自己聊了起来，这种场景不可能提前写单元测试覆盖。测试策略从验证具体行为转向验证不变量：不是测试"Agent会做什么"，而是确保"无论Agent做什么，系统都不会崩"。

### "没有人觉得这个东西非做不可"

被关停项目的共同点：没有人为之燃烧。核心人物"很少是纯粹的产品经理"，信念感是唯一不能被分配的东西。在想法还能装进一个人脑子里的阶段，加人实际上是负效果。

### 个人AI代理

2026年上半年最重要的产品问题：在完全开放和严格受控之间，存在什么样的产品形态？Dan观察到，给AI代理起名字、长期互动后产生归属感，别人的代理因为你信任你而信任它——形成影子组织架构。

## 与wiki的共振

这篇文章把多条已有线索串成一条线：

- [[experience-incompressible]] → AI省掉失败就省掉直觉
- [[steel-film-vs-whetstone]] → 室内树 = 钢化膜模式的产品版
- [[indoor-tree]] → 室内树效应：缺少摩擦导致脆弱生长
- [[anti-rationalization]] + [[scope-discipline]] → AI让加功能太容易，砍功能反而更难
- [[practice-epistemology]] → 重写的价值在于认知螺旋，不在于速度
- [[product-taste]] → 执行廉价化时代的品味崛起
- [[incompressible-judgment]] → 产品判断力是不可压缩的
- [[agent-native-tooling]] → Agent Native的产品设计维度

> 来源：为什么 AI 越强，产品经理越容易做出垃圾？Instagram 创始人给出了答案
