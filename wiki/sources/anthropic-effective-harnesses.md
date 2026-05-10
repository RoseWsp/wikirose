---
type: blog
date: 2025-11-26
author: Justin Young (Anthropic)
url: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
raw: raw/blog/anthropic-effective-harnesses.html
---

# Effective harnesses for long-running agents

Anthropic关于长时间运行Agent的Harness设计的开山之作。核心解决跨上下文窗口的Agent一致性问题，从人类工程师的工作方式中汲取灵感。

### 核心内容

- **双Agent架构**：Initializer Agent（首次运行设置环境）+ Coding Agent（每次会话增量推进）
- **Feature List机制**：用JSON而非Markdown管理功能清单，标记为"failing"让后续Agent有明确目标
- **增量推进**：每次只处理一个feature，完成后留下干净状态（git commit + progress文件）
- **端到端测试**：引入Puppeteer MCP做浏览器自动化验证，Agent能截图识别Bug
- **failure modes**：One-shot Syndrome（试图一步到位）、Premature Victory Declaration（过早宣布胜利）、Premature Feature Completion（过早标记功能完成）
- **典型启动序列**：pwd → 读git log和progress → 选最高优先级未完成feature → 启动dev server → 验证基础功能 → 开始新feature

### 关键引述

> "Imagine a software project staffed by engineers working in shifts, where each new engineer arrives with no memory of what happened on the previous shift."

> "Claude tended to try to do too much at once—essentially to attempt to one-shot the app."

### 关联页面

[[harness-engineering]]、[[agent-failure-modes]]、[[context-architecture]]
