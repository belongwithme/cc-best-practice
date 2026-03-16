# Skills 技能最佳实践

> 来源：[best-practice/claude-skills.md](https://github.com/shanraisshan/claude-code-best-practice/blob/main/best-practice/claude-skills.md)

Claude Code 技能 — 前置字段（frontmatter）与官方捆绑技能。

---

## 前置字段（10 个）

| 字段 | 类型 | 必需 | 描述 |
|------|------|------|------|
| `name` | string | 否 | 显示名称和 `/slash-command` 标识符。省略则默认为目录名 |
| `description` | string | 推荐 | 技能功能描述，在自动补全中显示，Claude 用于自动发现 |
| `argument-hint` | string | 否 | 自动补全时显示的提示 |
| `disable-model-invocation` | boolean | 否 | 设为 `true` 阻止 Claude 自动调用此技能 |
| `user-invocable` | boolean | 否 | 设为 `false` 从 `/` 菜单隐藏 — 技能变为后台知识，用于代理预加载 |
| `allowed-tools` | string | 否 | 此技能激活时允许无需权限确认的工具 |
| `model` | string | 否 | 运行此技能时使用的模型 |
| `context` | string | 否 | 设为 `fork` 在隔离的子代理上下文中运行技能 |
| `agent` | string | 否 | 当 `context: fork` 设置时的子代理类型（默认：`general-purpose`） |
| `hooks` | object | 否 | 作用域为此技能的生命周期钩子 |

---

## 官方捆绑技能（5 个）

| # | 技能 | 描述 |
|---|------|------|
| 1 | `simplify` | 审查变更代码的复用性、质量和效率 — 重构消除重复 |
| 2 | `batch` | 批量跨文件运行命令 |
| 3 | `debug` | 调试失败的命令或代码问题 |
| 4 | `loop` | 按间隔重复运行提示或斜杠命令（最长 3 天） |
| 5 | `claude-api` | 使用 Claude API 或 Anthropic SDK 构建应用 |

另见：[官方 Skills 仓库](https://github.com/anthropics/skills/tree/main/skills) — 社区维护的可安装技能。

---

## 两种使用模式

### 1. 用户直接调用

用户通过 `/skill-name` 直接调用，技能的内容注入到当前上下文。

```yaml
---
name: my-coding-style
description: 我的编码风格指南
---

遵循以下编码规范：
- 使用 TypeScript 严格模式
- 函数注释使用 JSDoc
- ...
```

### 2. 代理预加载

通过子代理的 `skills` 字段预加载，作为代理的领域知识。

```yaml
# .claude/agents/my-agent.md
---
name: my-agent
skills:
  - my-coding-style  # 启动时预加载
---
```

---

## Monorepo 中的技能组织

在大型 Monorepo 中，可以在子目录中放置技能：

```
/my-monorepo/
├── .claude/skills/          # 全局技能
│   └── shared-utils/SKILL.md
├── frontend/
│   └── .claude/skills/      # 前端专用技能
│       └── react-patterns/SKILL.md
└── backend/
    └── .claude/skills/      # 后端专用技能
        └── api-guidelines/SKILL.md
```

技能发现遵循与 CLAUDE.md 相同的祖先/后代加载机制。

---

## 参考来源

- [Claude Code Skills 文档](https://code.claude.com/docs/en/skills)
- [Monorepo 中的 Skills 发现](https://github.com/shanraisshan/claude-code-best-practice/blob/main/reports/claude-skills-for-larger-mono-repos.md)
