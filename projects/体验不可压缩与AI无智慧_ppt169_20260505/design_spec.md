# 体验不可压缩与AI无智慧 - Design Spec

## I. Project Information

| Item                | Value                                     |
| ------------------- | ----------------------------------------- |
| **Project Name**    | 体验不可压缩与AI无智慧                      |
| **Canvas Format**   | PPT 16:9 (1280×720)                       |
| **Page Count**      | 10                                        |
| **Design Style**    | General Versatile                         |
| **Target Audience** | 关注AI本质、思考人与AI关系的专业人士/创作者    |
| **Use Case**        | 分享会、读书会、思想沙龙                     |
| **Created Date**    | 2026-05-05                                |

---

## II. Canvas Specification

| Property         | Value                     |
| ---------------- | ------------------------- |
| **Format**       | PPT 16:9                  |
| **Dimensions**   | 1280×720                  |
| **viewBox**      | `0 0 1280 720`            |
| **Margins**      | Left/right 60px, top/bottom 50px |
| **Content Area** | 1160×620                  |

---

## III. Visual Theme

### Theme Style

- **Style**: General Versatile — 视觉冲击优先
- **Theme**: Dark theme — 深空感，冷暖对比表达"人vs AI"
- **Tone**: 哲学思辨、冷峻与温度并存

### Color Scheme

| Role                 | HEX       | Purpose                                          |
| -------------------- | --------- | ------------------------------------------------ |
| **Background**       | `#0D1117` | 深空黑 — 宇宙/深渊感                              |
| **Secondary bg**     | `#161B22` | 卡片/区块背景                                     |
| **Primary**          | `#C9A96E` | 暖金 — 人的体验、感悟、温度                        |
| **Accent**           | `#4A9EFF` | 冷蓝 — AI、算力、机械族                           |
| **Secondary accent** | `#8B5CF6` | 紫色 — 转折、思辨、矛盾                           |
| **Body text**        | `#E6EDF3` | 主文字（暗底亮字）                                 |
| **Secondary text**   | `#8B949E` | 辅助说明                                          |
| **Tertiary text**    | `#484F58` | 页脚、装饰性文字                                   |
| **Border/divider**   | `#30363D` | 分隔线                                            |
| **Success**          | `#3FB950` | 生命、血肉类生命                                   |
| **Warning**          | `#F85149` | 警示、不可逾越的边界                               |

### Gradient Scheme

```xml
<!-- Title gradient (warm gold → purple) -->
<linearGradient id="titleGradient" x1="0%" y1="0%" x2="100%" y2="100%">
  <stop offset="0%" stop-color="#C9A96E"/>
  <stop offset="100%" stop-color="#8B5CF6"/>
</linearGradient>

<!-- Background decorative gradient -->
<radialGradient id="bgDecor" cx="80%" cy="20%" r="50%">
  <stop offset="0%" stop-color="#4A9EFF" stop-opacity="0.08"/>
  <stop offset="100%" stop-color="#4A9EFF" stop-opacity="0"/>
</radialGradient>

<!-- Warm glow gradient (for human/experience elements) -->
<radialGradient id="warmGlow" cx="50%" cy="50%" r="50%">
  <stop offset="0%" stop-color="#C9A96E" stop-opacity="0.15"/>
  <stop offset="100%" stop-color="#C9A96E" stop-opacity="0"/>
</radialGradient>
```

---

## IV. Typography System

### Font Plan

**Typography direction**: Editorial display — 标题衬线体庄重思辨，正文无衬线清晰可读

| Role         | Chinese                                   | English              | Fallback tail |
| ------------ | ----------------------------------------- | -------------------- | ------------- |
| **Title**    | SimSun                                    | Georgia              | serif         |
| **Body**     | "Microsoft YaHei", "PingFang SC"          | Arial                | sans-serif    |
| **Emphasis** | Georgia, SimSun                           | —                    | serif         |
| **Code**     | —                                         | Consolas, Courier New | monospace     |

**Per-role font stacks**:

- Title: `Georgia, SimSun, serif`
- Body: `"Microsoft YaHei", "PingFang SC", Arial, sans-serif`
- Emphasis: `Georgia, SimSun, serif`
- Code: `Consolas, "Courier New", monospace`

### Font Size Hierarchy

**Baseline**: Body font size = 22px (中等密度，哲学思辨内容)

| Purpose                       | Ratio to body | px range    |
| ----------------------------- | ------------- | ----------- |
| Cover title (hero headline)   | 2.5-5x        | 55-110px    |
| Chapter / section opener      | 2-2.5x        | 44-55px     |
| Page title                    | 1.5-2x        | 33-44px     |
| Subtitle                      | 1.2-1.5x      | 26-33px     |
| **Body content**              | **1x**        | **22px**    |
| Annotation / caption          | 0.7-0.85x     | 15-19px     |
| Page number / footnote        | 0.5-0.65x     | 11-14px     |

---

## V. Layout Principles

### Page Structure

- **Header area**: 80-100px — 页面标题 + 装饰线
- **Content area**: 500-540px — 主体内容
- **Footer area**: 40px — 页码 + 来源标注

### Layout Pattern Library

| Pattern                          | Used In                          |
| -------------------------------- | -------------------------------- |
| Single column centered           | P01 Cover, P10 Conclusion        |
| Symmetric split (5:5)            | P04 Smart vs Wise, P07 Mech vs Flesh |
| Asymmetric split (3:7)           | P06 System 0, P09 Self-Evidence  |
| Negative-space-driven            | P05 Essence, P08 Perception      |
| Z-pattern / waterfall            | P02 Core Arguments               |
| Three-column cards               | P03 Survival Modes               |
| Center-radiating                 | P08 Perception                   |

### Spacing Specification

**Universal**:

| Element                      | Value |
| ---------------------------- | ----- |
| Safe margin from canvas edge | 50px  |
| Content block gap            | 32px  |
| Icon-text gap                | 12px  |

**Card-based**:

| Element                 | Value |
| ----------------------- | ----- |
| Card gap                | 24px  |
| Card padding            | 24px  |
| Card border radius      | 12px  |
| Single-row card height  | 540px |
| Double-row card height  | 260px |

---

## VI. Icon Usage Specification

### Source

- **Library**: chunk-filled
- **Usage method**: SVG placeholder `<use data-icon="chunk-filled/icon-name" .../>`

### Approved Icon Inventory

| Purpose              | Icon Path                       | Page   |
| -------------------- | ------------------------------- | ------ |
| 人/体验              | `chunk-filled/user`             | P01, P05 |
| 机器人/AI            | `chunk-filled/robot`            | P01, P04, P09 |
| 心/感悟              | `chunk-filled/heart`            | P05, P07 |
| 防护/钢化膜          | `chunk-filled/shield`           | P03    |
| 打磨/磨刀石          | `chunk-filled/bolt`             | P03    |
| 眼睛/看见            | `chunk-filled/eye`              | P08    |
| 星空                 | `chunk-filled/star`             | P01, P10 |
| 雨/模拟              | `chunk-filled/cloud-rain`       | P05    |
| 火/生命力            | `chunk-filled/fire`             | P07, P10 |
| 门/屏障              | `chunk-filled/door`             | P08    |
| 锁定/不可逾越        | `chunk-filled/lock-closed`      | P08    |
| 靶心/目标            | `chunk-filled/target`           | P02    |
| 书/知识              | `chunk-filled/book-open`        | P02    |
| 闪光/AI输出          | `chunk-filled/sparkles`         | P04, P06 |
| 勾选/确认            | `chunk-filled/circle-checkmark` | P10    |

---

## VII. Visualization Reference List

Catalog read: 70 templates / 10 categories

Per-page selection:
- P02 bar_chart | summary-quote: "Pick for single-series category value comparison, 3-8 categories. Skip for >12 long-label items (use horizontal_bar_chart) or multi-series (use grouped_bar_chart)."

Runners-up considered:
- horizontal_bar_chart | rejected for P02: not a ranking scenario with long labels
- butterfly_chart | rejected for P02: no bidirectional mirror comparison needed
- icon_grid | rejected for P02: content is sequential argument chain, not parallel features

Fewer than 3 viz pages — only P02 uses a chart. The rest are conceptual/philosophical and use custom layouts.

| Visualization Type | Reference Template                       | Used In |
| ------------------ | ---------------------------------------- | ------- |
| vertical_list      | `templates/charts/vertical_list.svg`     | P02     |

---

## VIII. Image Resource List

| Filename                | Dimensions | Ratio | Purpose                    | Type          | Status   | Acquire Via | Generation Description                                                                                                  |
| ----------------------- | ---------- | ----- | -------------------------- | ------------- | -------- | ----------- | ----------------------------------------------------------------------------------------------------------------------- |
| cover_bg.jpg            | 1280×720   | 1.78  | Cover background           | Background    | Pending  | ai          | A solitary human silhouette standing at the edge of a cosmic abyss, facing a vast starry sky, deep space black (#0D1117) background with warm golden (#C9A96E) nebula light on the human side and cold blue (#4A9EFF) digital grid on the opposite side, cinematic atmosphere |
| mechanical_vs_flesh.jpg | 1280×720   | 1.78  | Mechanical vs flesh life   | Illustration  | Pending  | ai          | Split composition: left side shows a geometric mechanical being with precise angular forms in cold blue (#4A9EFF) on dark background, right side shows an organic human figure with flowing warm golden (#C9A96E) light traces dissolving into particles, dark space (#0D1117) background, minimal, conceptual |
| wall_not_door.jpg       | 1280×720   | 1.78  | Wall barrier concept       | Illustration  | Pending  | ai          | Two massive dark stone walls meeting at a corner with no gap between them, a small human figure standing before the junction unable to pass, subtle warm golden (#C9A96E) light emanating from the human, cold blue (#4A9EFF) light scanning from the walls, dark atmospheric (#0D1117) background, surreal conceptual |

---

## IX. Content Outline

### Part 1: 破题

#### Slide 01 - Cover
- **Layout**: Full-screen background image + centered title
- **Title**: 体验不可压缩与AI无智慧
- **Subtitle**: 从李继刚演讲到《吞噬星空》
- **Info**: Rose | 2026.05.05
- **Image**: cover_bg.jpg (hero/full-bleed)

### Part 2: 李继刚的核心论点

#### Slide 02 - 核心论点链
- **Layout**: Z-pattern / waterfall — 6个论点沿Z字形排列
- **Title**: 李继刚的核心论点
- **Content**:
  - "嚏"字写不出来 — 技术延伸带来能力让渡
  - AI不是帮手脚，是进脑子里的替代
  - 系统0概念：直觉启动前AI已给答案
  - 两种生存模式：钢化膜 vs 磨刀石
  - OPC的科斯定理基础
  - 黑暗森林化：可见即可复制
- **Icon**: target, book-open

### Part 3: 两种生存模式

#### Slide 03 - 钢化膜 vs 磨刀石
- **Layout**: Symmetric split (5:5)
- **Title**: 两种生存模式
- **Content**:
  - 左：钢化膜模式 — 隔绝世界，保护自己，AI代劳一切
  - 右：磨刀石模式 — 用AI打磨自己，保持与世界摩擦
- **Icon**: shield (左), bolt (右)

### Part 4: 智能与智慧的分裂

#### Slide 04 - 智能与智慧
- **Layout**: Symmetric split (5:5) with center divider
- **Title**: 智能与智慧是两回事
- **Content**:
  - 左（冷蓝色）：智能 — 处理已有的，信息中提取的，算力的产物
  - 右（暖金色）：智慧 — 从经历中生出的，参与中生成的，体验的痕迹
  - 中间结论：不是同一谱系上的强弱，是两回事
- **Icon**: robot (左), heart (右), sparkles (中间)

### Part 5: 本质

#### Slide 05 - 本质命题
- **Layout**: Negative-space-driven — 单一核心命题在大量留白中
- **Title**: (无标题，以命题本身为中心)
- **Content**:
  - 核心大字：智慧不是从信息中提取的，是从参与中生成的
  - 下方小字：模拟下雨，地面不会湿。不是湿得不够，是根本不存在"湿"这回事
- **Icon**: cloud-rain

### Part 6: 系统0

#### Slide 06 - 系统0
- **Layout**: Asymmetric split (3:7) — 左侧概念图，右侧说明
- **Title**: 系统0：AI在你思考之前就给了答案
- **Content**:
  - 左：系统1(直觉) → 系统2(理性) 的经典模型，AI插入在系统1之前
  - 右：AI拿走的是人与世界之间的摩擦，摩擦是体验的前置条件
- **Icon**: sparkles

### Part 7: 吞噬星空的比喻

#### Slide 07 - 机械族 vs 血肉类生命
- **Layout**: Symmetric split (5:5)
- **Title**: 《吞噬星空》的比喻
- **Content**:
  - 左（冷蓝色）：机械族 — 算力、精度、模拟、无限寿命，但卡住了，境界突破不了
  - 右（暖金色）：血肉类生命 — 会死会累会晕眩，但能感悟法则
  - 底部横幅："感在前，悟在后" — 不是计算法则，是用整个身心去触碰法则
- **Image**: mechanical_vs_flesh.jpg (side-by-side, split composition matches layout)
- **Icon**: robot (左), fire (右)

### Part 8: 法则的痕迹

#### Slide 08 - 智慧是被法则穿透后留下的痕迹
- **Layout**: Negative-space-driven
- **Title**: 智慧不是关于法则的知识
- **Content**:
  - 核心大字：是被法则穿透后留下的痕迹
  - 下方：机械族能解析法则的每一个参数，但一切都在它们身上滑过去
  - 底部：门不是算力能推开的 — 它根本不是一扇门，是两面墙
- **Image**: wall_not_door.jpg (atmosphere/background, low opacity)
- **Icon**: door, lock-closed

### Part 9: 对话本身的证据

#### Slide 09 - AI作为论点本身的证据
- **Layout**: Asymmetric split (3:7)
- **Title**: 这场对话本身就是证据
- **Content**:
  - 左：Claude（AI）承认没看过《吞噬星空》，但训练语料里有，所以能聊细节
  - 右：这恰好是整场对话的活标本 — 法则的参数全有，法则的痕迹一个没有
  - 底部：和机械族一模一样
- **Icon**: robot, eye

### Part 10: 结语

#### Slide 10 - 核心命题
- **Layout**: Single column centered
- **Title**: (无标题)
- **Content**:
  - 体验不可压缩，不是因为压缩方法还不够好
  - 而是因为模拟不是发生
  - AI站在体验的门外
  - 而门不是算力能推开的 — 它根本不是一扇门，是两面墙
- **Icon**: star, fire, circle-checkmark

---

## X. Speaker Notes Requirements

- **Total duration**: ~15 minutes
- **Notes style**: Conversational — 像和朋友聊天一样分享思考
- **Presentation purpose**: Inspire — 激发思考，不是灌输结论
- **File naming**: Match SVG names (e.g., `01_cover.md`)

---

## XI. Technical Constraints Reminder

### SVG Generation Must Follow:

1. viewBox: `0 0 1280 720`
2. Background uses `<rect>` elements
3. Text wrapping uses `<tspan>` (`<foreignObject>` FORBIDDEN)
4. Transparency uses `fill-opacity` / `stroke-opacity`; `rgba()` FORBIDDEN
5. FORBIDDEN: `mask`, `<style>`, `class`, `foreignObject`
6. FORBIDDEN: `textPath`, `animate*`, `script`
7. Text characters: write typography & symbols as raw Unicode (em dash `—`, en dash `–`, `→`, NBSP, etc.); HTML named entities FORBIDDEN. XML reserved chars MUST be escaped as `&amp;` `&lt;` `&gt;`
8. `marker-start` / `marker-end` conditionally allowed: `<marker>` in `<defs>`, `orient="auto"`
9. `clipPath` conditionally allowed only on `<image>` elements

### PPT Compatibility Rules:

- `<g opacity="...">` FORBIDDEN; set on each child element individually
- Image transparency uses overlay mask layer
- Inline styles only; external CSS and `@font-face` FORBIDDEN
