# Memory 记忆最佳实践

> 来源：[best-practice/claude-memory.md](https://github.com/shanraisshan/claude-code-best-practice/blob/main/best-practice/claude-memory.md)

通过 CLAUDE.md 文件实现持久上下文 — 如何编写以及在 Monorepo 中如何加载。

---

## 1. 编写好的 CLAUDE.md

一个结构良好的 CLAUDE.md 是提升 Claude Code 项目输出质量的**最有效方式**。

### 关键原则

- **保持简短**：每个文件控制在 200 行以内（[官方建议](https://code.claude.com/docs/en/memory#write-effective-instructions)），[HumanLayer 建议 60 行](https://www.humanlayer.dev/blog/writing-a-good-claude-md)
- **CLAUDE.md 不保证执行**：即使写了 MUST 也可能被忽略（[Reddit 讨论](https://reddit.com/r/ClaudeCode/comments/1qn9pb9/))
- **使用 `.claude/rules/`**：拆分大型指令到独立规则文件

### 推荐内容

- 项目架构概述
- 编码规范和命名约定
- 测试要求
- 构建和部署命令
- 常见陷阱和注意事项

### 不推荐内容

- 过于冗长的文档
- 与编码无关的内容
- 重复 IDE 已提供的信息

---

## 2. CLAUDE.md 在 Monorepo 中的加载

### 两种加载机制

#### 祖先加载（向上遍历目录树）

启动 Claude Code 时，从当前工作目录**向上**遍历到文件系统根目录，加载沿途找到的每个 CLAUDE.md。这些文件在**启动时立即加载**。

#### 后代加载（向下遍历目录树）

当前工作目录的子目录中的 CLAUDE.md **不会在启动时加载**。只有当 Claude 在会话期间读取这些子目录中的文件时才会加载。这称为**懒加载**。

### 示例 Monorepo 结构

```
/mymonorepo/
├── CLAUDE.md          # 根级指令（所有组件共享）
├── frontend/
│   └── CLAUDE.md      # 前端专用指令
├── backend/
│   └── CLAUDE.md      # 后端专用指令
└── api/
    └── CLAUDE.md      # API 专用指令
```

### 场景 1：从根目录运行

```bash
cd /mymonorepo
claude
```

| 文件 | 启动时加载？ | 原因 |
|------|-------------|------|
| `/mymonorepo/CLAUDE.md` | 是 | 当前工作目录 |
| `/mymonorepo/frontend/CLAUDE.md` | 否 | 仅当读写 `frontend/` 中文件时加载 |
| `/mymonorepo/backend/CLAUDE.md` | 否 | 仅当读写 `backend/` 中文件时加载 |
| `/mymonorepo/api/CLAUDE.md` | 否 | 仅当读写 `api/` 中文件时加载 |

### 场景 2：从组件目录运行

```bash
cd /mymonorepo/frontend
claude
```

| 文件 | 启动时加载？ | 原因 |
|------|-------------|------|
| `/mymonorepo/CLAUDE.md` | 是 | 祖先目录 |
| `/mymonorepo/frontend/CLAUDE.md` | 是 | 当前工作目录 |
| `/mymonorepo/backend/CLAUDE.md` | 否 | 不同目录分支 |
| `/mymonorepo/api/CLAUDE.md` | 否 | 不同目录分支 |

### 关键要点

1. **祖先始终在启动时加载** — 确保始终能访问根级仓库指令
2. **后代懒加载** — 防止无关上下文膨胀会话
3. **兄弟永不加载** — 在 `frontend/` 时不会加载 `backend/CLAUDE.md`
4. **全局 CLAUDE.md** — 可在 `~/.claude/CLAUDE.md` 放置，适用于所有会话

### 最佳实践

1. **共享约定放根级 CLAUDE.md** — 编码标准、提交消息格式、PR 模板等
2. **组件特定指令放组件 CLAUDE.md** — 框架特定模式、组件架构、测试约定
3. **个人偏好用 CLAUDE.local.md** — 添加到 `.gitignore`，不与团队共享

---

## 记忆文件位置

| 位置 | 范围 | 说明 |
|------|------|------|
| `CLAUDE.md` | 项目 | 项目根目录，提交到 git |
| `CLAUDE.local.md` | 个人 | 本地，添加到 .gitignore |
| `.claude/rules/` | 项目 | 拆分的规则文件 |
| `~/.claude/rules/` | 全局 | 全局规则 |
| `~/.claude/CLAUDE.md` | 全局 | 所有项目通用指令 |
| `~/.claude/projects/<project>/memory/` | 项目个人 | 自动记忆存储 |

---

## 参考来源

- [Claude Code 记忆文档](https://code.claude.com/docs/en/memory)
- [Boris Cherny 关于 CLAUDE.md 加载的说明](https://x.com/bcherny/status/2016339448863355206)
- [HumanLayer - 编写好的 Claude.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md)
