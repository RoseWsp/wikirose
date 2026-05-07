# Agent 隔离 (Agent Isolation)

**TL;DR** 并行需要隔离。没有隔离你没有多个agent——你只有一个很困惑的agent带着四个终端。

## 这意味着什么

多个coding agent并行工作时，第一个崩的永远是共享状态：Git冲突、文件系统踩脚、Docker Compose互相杀容器。这不是agent能力问题，是基础设施问题。

Finbarr Taylor用yolobox的实践给出了答案：**给每个agent一份完整的项目拷贝、独立的Compose命名空间、独立的URL。** 不是worktree（只隔离.git），不是overlay fs（聪明但脆弱），是全量拷贝——笨但可靠 ([[finbarr-treat-agents-like-developers]])。

## 隔离的三个层次

| 层次 | 问题 | 解法 |
|---|---|---|
| **代码隔离** | 两个agent改同一checkout | 各自的完整文件夹拷贝 + 各自commit/push |
| **运行时隔离** | 共享端口、容器、volume | 独立COMPOSE_PROJECT_NAME，各自的数据卷 |
| **网络隔离** | 端口冲突、URL混乱 | 本地反代 + 友好.localhost域名 |

每层对应人类开发者的一个需求：自己的clone、自己的开发环境、自己的预览URL。这正是[[agent-as-developer|Agent即开发者]]心智模型在基础设施层的落地。

## 为什么全量拷贝赢过精巧方案

Worktree、sparse checkout、rsync排除依赖、overlay filesystem——这些都更"优雅"。但全量拷贝有三个不可替代的属性：

1. **保留脏状态** — 项目运行依赖的东西不全在git里（.env、node_modules、SQLite），全量拷贝全带上
2. **路径一致性** — 拷贝挂载到原始路径，硬编码绝对路径、agent session history、IDE状态全都继续工作
3. **心智模型极简** — 每个fork = 另一个开发者的机器，没有新抽象

"存储便宜，耐心不便宜"——对大多数项目全量拷贝的代价可接受，对大型monorepo可能需要更细粒度的方案。

## 与其他隔离模式的类比

- **多租户架构** — COMPOSE_PROJECT_NAME就是tenant ID，每个agent是独立tenant
- **微服务隔离** — 每个service拥有自己的数据存储，不共享数据库
- **进程隔离** — 进程间通过IPC通信而非共享内存，agent间通过git remote同步
- **公地悲剧** — 共享checkout/Compose project是经典commons problem

## 为什么现在重要

Agent矩阵从"单任务"到"多任务并行"的跃迁，隔离是跳不过的门槛。Boris Cherny每天跑几百个agent ([[boris-chenyi-sequoia-ai-ascent]])，Cat Wu预见的50-100个Claude同时运行 ([[cat-wu-ai-pm-role]])——这些场景没有隔离全是空谈。

Finbarr的关键发现：**"让我惊讶的是，多少摩擦是协调摩擦，不是能力摩擦。Agent已经够用了，缺的是无聊的基础设施。"** 这与[[harness-engineering|脚手架工程]]的核心洞察一致——瓶颈不在模型，在护栏。

## 关联

- [[agent-as-developer]] — 隔离的逻辑前提：因为agent=开发者，所以需要开发者级别的隔离
- [[harness-engineering]] — 隔离是脚手架在运行时层的基础
- [[agent-matrix]] — 多agent并行是Agent矩阵的前提，隔离是多agent并行的前提
- [[agentic-engineering]] — 隔离是Agentic Engineering基础设施层的第一课
- [[scope-discipline]] — 隔离在物理层划定边界，范围纪律在行动层划定边界——两者合在一起是完整的agent约束
- [[anti-rationalization]] — 隔离防agent互相踩脚，反合理化防agent自我说服跳过纪律
- [[loop-scheduling]] — Loop调度的几百个agent同样需要隔离基础设施
- [[addyosmani-agent-skills]] — 隔离管"身体"，Agent Skills管"纪律"，合在一起才是完整的agent=developer
