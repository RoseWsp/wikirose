# 编译型知识库

一种知识管理架构，将原始素材视为"源代码"，LLM作为"编译器"将其转换为结构化、互链的知识网络。

## 核心隐喻

**源代码** → **编译器** → **可执行程序**
**原始素材** → **LLM** → **结构化wiki**

## 架构设计

```
raw/          wiki/
├── PDF报告   ├── concepts/概念页
├── 网页剪藏   ├── insights/洞察页  
├── 录音转写   ├── sources/源摘要
└── 待处理材料 └── index.md全局索引
```

## 关键原则

1. **分离关注点**：`raw/`只存原始不可变素材，`wiki/`只存LLM生成内容
2. **编译非摘要**：不是简单缩短，而是跨文档知识重组
3. **网络化输出**：输出是互链页面网络，不是孤立文档
4. **持续维护**：新素材触发重新编译相关部分

## 编译过程示例（([[karpathy-llm-knowledge-management]])）

以SemiAnalysis GPU报告为例：
- **输入**：40页PDF（`raw/reports/semianalysis-gpu-lease.pdf`）
- **编译**：LLM提取4个核心判断+论据+评注
- **输出**：800字洞察页（`wiki/insights/gpu-lease-trends.md`）
- **关联**：自动链接到[[推理成本]]、[[AI漫剧经济学]]等相关概念
- **认知转变**：原始信息与所需知识之间存在gap，LLM填补这个gap，实现从"存储"到"编译"的转变

### 个人实践验证（([[karpathy-obsidian-rebuild]])）
- **结构改造**：从按类型分文件夹（新闻/报告/洞察/笔记）到`raw/`与`wiki/`分离的编译架构
- **编译效果**：40页SemiAnalysis PDF被编译为800字洞察文章，提炼4个核心判断
- **交叉节点发现**：自动生成《推理成本》概念页，串联不同报告中的相关数据
- **实践体会**："编译"与"摘要"的本质区别：不是单篇文章缩短，而是多篇文章知识重新组织成概念网络

## 与传统知识库对比

| 传统知识库 | 编译型知识库 |
|---|---|
| 存储原始文档 | 存储编译后的知识 |
| 检索时临时分析 | 预编译结构化知识 |
| 人工维护链接 | 自动维护交叉引用 |
| 信息孤岛风险 | 强制网络化连接 |

## 优势

- **激活沉睡内容**：未读PDF→可查询知识节点
- **知识密度提升**：40页→800字核心判断
- **自动关联发现**：跨文档概念链自动建立
- **维护成本趋零**：LLM处理更新传播

## 实践参考

- [[karpathy-llm-knowledge-management]]：如何将Obsidian改造成编译型知识库
- [[karpathy-knowledge-workflow-guide]]：详细的三层目录结构工作流指南，包含健康检查、增量编译等高级功能
- [[karpathy-obsidian-rebuild]]：个人实践验证与认知转变体验

## 相关概念

[[llm-knowledge-management]]、[[knowledge-compounding]]、[[obsidian-optimization]]、[[product-taste]]、[[action-based-ai]]、[[obsidian-rebuild-experience]]、[[knowledge-compilation-workflow]]、[[knowledge-health-check]]、[[incremental-compilation]]、[[knowledge-engineering]]