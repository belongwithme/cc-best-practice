# Subagents 子代理最佳实践

> 来源：[best-practice/claude-subagents.md](https://github.com/shanraisshan/claude-code-best-practice/blob/main/best-practice/claude-subagents.md)

Claude Code 子代理 — 前置字段（frontmatter）与官方内置代理类型。

---

## 前置字段（14 个）

| 字段 | 类型 | 必需 | 描述 |
|------|------|------|------|
| `name` | string | 是 | 唯一标识符，使用小写字母和连字符 |
| `description` | string | 是 | 何时调用。使用 `"PROACTIVELY"` 让 Claude 自动调用 |
| `tools` | string/list | 否 | 逗号分隔的工具白名单（如 `Read, Write, Edit, Bash`）。省略则继承所有工具。支持 `Agent(agent_type)` 语法 |
| `disallowedTools` | string/list | 否 | 要拒绝的工具，从继承或指定列表中移除 |
| `model` | string | 否 | 模型别名：`haiku`, `sonnet`, `opus`, 或 `inherit`（默认：`inherit`） |
| `permissionMode` | string | 否 | 权限模式：`default`, `acceptEdits`, `dontAsk`, `bypassPermissions`, 或 `plan` |
| `maxTurns` | integer | 否 | 子代理停止前的最大代理轮次数 |
| `skills` | list | 否 | 启动时预加载到代理上下文中的技能名称（注入完整内容） |
| `mcpServers` | list | 否 | 此子代理的 MCP 服务器 — 服务器名称字符串或内联 `{name: config}` 对象 |
| `hooks` | object | 否 | 作用域为此子代理的生命周期钩子。支持所有钩子事件 |
| `memory` | string | 否 | 持久记忆范围：`user`, `project`, 或 `local` |
| `background` | boolean | 否 | 设为 `true` 始终作为后台任务运行（默认：`false`） |
| `isolation` | string | 否 | 设为 `"worktree"` 在临时 git worktree 中运行 |
| `color` | string | 否 | CLI 输出颜色（如 `green`, `magenta`） |

---

## 官方内置代理（6 个）

| # | 代理 | 模型 | 工具 | 描述 |
|---|------|------|------|------|
| 1 | `general-purpose` | inherit | 全部 | 复杂多步骤任务 — 研究、代码搜索和自主工作的默认代理 |
| 2 | `Explore` | haiku | 只读 | 快速代码库搜索和探索 — 查找文件、搜索代码 |
| 3 | `Plan` | inherit | 只读 | 预规划研究 — 在写代码前探索代码库并设计实现方案 |
| 4 | `Bash` | inherit | Bash | 在独立上下文中运行终端命令 |
| 5 | `statusline-setup` | sonnet | Read, Edit | 配置用户的状态栏设置 |
| 6 | `claude-code-guide` | haiku | Glob, Grep, Read, WebFetch, WebSearch | 回答关于 Claude Code 功能的问题 |

---

## 使用建议

### 创建自定义子代理示例

```yaml
---
name: code-reviewer
description: 审查代码变更，检查 bug 和安全漏洞
tools: Read, Glob, Grep, WebSearch
model: opus
permissionMode: plan
maxTurns: 20
skills:
  - code-review-guidelines
---

你是一个代码审查专家。审查提交的代码变更，关注：
1. 潜在的 bug 和逻辑错误
2. 安全漏洞
3. 性能问题
4. 代码风格一致性
```

### Boris 的建议

- 子代理应该是**功能特定的**（如 code-reviewer、data-migrator），而不是通用角色（如 "QA Agent"、"Backend Engineer"）
- 使用 `skills` 字段预加载相关领域知识
- 说 "use subagents" 可以让 Claude 自动将任务分配给子代理，保持主上下文清洁

---

## 参考来源

- [创建自定义子代理 — Claude Code 文档](https://code.claude.com/docs/en/sub-agents)
- [CLI 参考 — Claude Code 文档](https://code.claude.com/docs/en/cli-reference)
