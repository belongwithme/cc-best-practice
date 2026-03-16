# Claude Code Best Practice Wiki

> 基于 [shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice) 项目的中文分析与整理

本仓库是对 Claude Code 最佳实践项目的系统性分析，帮助中文开发者快速掌握 Claude Code 的核心概念、工作流、技巧和配置。

---

## 项目概览

| 项目 | 信息 |
|------|------|
| 原始仓库 | [shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice) |
| Stars | 17.2k+ |
| 许可证 | MIT |
| 最后更新 | 2026年3月15日 (v2.1.76) |
| 定位 | Claude Code 最佳实践大全 — "practice makes claude perfect" |

---

## 目录

### 核心概念
- [概念总览](docs/concepts/概念总览.md) — Commands、Subagents、Skills、Hooks、MCP 等核心模块
- [编排工作流](docs/concepts/编排工作流.md) — Command → Agent → Skill 编排模式详解

### 最佳实践
- [Commands 命令](docs/best-practice/Commands命令.md) — 前置字段与 62 个官方内置命令
- [Subagents 子代理](docs/best-practice/Subagents子代理.md) — 14 个前置字段与 6 个官方子代理
- [Skills 技能](docs/best-practice/Skills技能.md) — 10 个前置字段与 5 个官方技能
- [Memory 记忆](docs/best-practice/Memory记忆.md) — CLAUDE.md 编写与 Monorepo 加载机制
- [MCP 服务器](docs/best-practice/MCP服务器.md) — 日常推荐 MCP 与配置方法
- [Settings 配置](docs/best-practice/Settings配置.md) — 55+ 设置项与 140+ 环境变量
- [CLI 启动参数](docs/best-practice/CLI启动参数.md) — 启动标志、子命令与环境变量

### 技巧与窍门
- [提示词技巧](docs/tips/提示词技巧.md) — 提示、规划、工作流、调试、日常习惯
- [Boris 与团队推文精选](docs/tips/Boris与团队推文精选.md) — Claude Code 核心团队的经验分享

### 开发工作流
- [开发工作流](docs/workflows/开发工作流.md) — Cross-Model、RPI、Ralph Wiggum Loop 等
- [热门功能](docs/workflows/热门功能.md) — /btw、Code Review、Voice Mode、Agent Teams 等
- [🔥 开发工作流核心概念与后端实战](docs/workflows/开发工作流核心概念与后端实战.md) — 三层架构详解 + Spring Boot 订单查询 API 完整示例

### 深度报告
- [报告索引](docs/reports/报告索引.md) — 9 篇深度分析报告索引

### 其他
- [项目分析总结](docs/项目分析总结.md) — 项目整体分析
- [创业公司影响](docs/创业公司影响.md) — Claude Code 对创业产品的替代分析
- [十亿美元问题](docs/十亿美元问题.md) — 尚未解决的关键问题

---

## 如何使用

```
1. 按顺序阅读「核心概念」，了解 Commands、Agents、Skills、Hooks 的定义和区别
2. 阅读「最佳实践」，深入理解每个模块的配置字段和官方内置功能
3. 浏览「技巧与窍门」，学习 Claude Code 创建者 Boris Cherny 和团队的实战经验
4. 参考「开发工作流」，选择适合自己项目的工作模式
5. 查阅「深度报告」，了解高级主题如 Agent SDK vs CLI、Monorepo Skills 等
```

---

## 致谢

- 原始项目作者：[Shayan Rais (shanraisshan)](https://github.com/shanraisshan)
- Claude Code 团队：[Boris Cherny](https://x.com/bcherny)、[Thariq](https://x.com/trq212)
- 原始项目许可证：MIT
