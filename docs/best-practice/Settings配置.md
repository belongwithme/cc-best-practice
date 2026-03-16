# Settings 配置最佳实践

> 来源：[best-practice/claude-settings.md](https://github.com/shanraisshan/claude-code-best-practice/blob/main/best-practice/claude-settings.md)

Claude Code `settings.json` 的所有可用配置选项指南。截至 v2.1.76，Claude Code 提供 **55+ 设置项**和 **140+ 环境变量**。

---

## 设置优先级层次

设置按优先级从高到低应用：

| 优先级 | 位置 | 范围 | 共享？ | 用途 |
|--------|------|------|--------|------|
| 1 | 托管设置 | 组织 | 是（IT 部署） | 不可覆盖的安全策略 |
| 2 | 命令行参数 | 会话 | N/A | 临时单次会话覆盖 |
| 3 | `.claude/settings.local.json` | 项目 | 否（git-ignored） | 个人项目特定设置 |
| 4 | `.claude/settings.json` | 项目 | 是（提交到 git） | 团队共享设置 |
| 5 | `~/.claude/settings.json` | 用户 | N/A | 全局个人默认值 |

**重要**：
- `deny` 规则拥有最高安全优先级，不可被低优先级的 allow/ask 规则覆盖
- 数组设置（如 `permissions.allow`）跨范围**合并去重**，而非替换

---

## 核心配置

### 常用设置

| 键 | 类型 | 默认值 | 描述 |
|-----|------|--------|------|
| `model` | string | `"default"` | 覆盖默认模型 |
| `agent` | string | - | 主对话的默认代理 |
| `language` | string | `"english"` | Claude 首选响应语言 |
| `cleanupPeriodDays` | number | `30` | 不活跃会话清理天数 |
| `alwaysThinkingEnabled` | boolean | `false` | 默认启用扩展思考 |
| `teammateMode` | string | `"auto"` | Agent 团队显示模式 |

### 示例

```json
{
  "model": "opus",
  "language": "chinese",
  "alwaysThinkingEnabled": true,
  "cleanupPeriodDays": 60
}
```

---

## 权限系统

### 权限结构

```json
{
  "permissions": {
    "allow": [],
    "ask": [],
    "deny": [],
    "additionalDirectories": [],
    "defaultMode": "acceptEdits"
  }
}
```

### 权限模式

| 模式 | 行为 |
|------|------|
| `"default"` | 标准权限检查并提示 |
| `"acceptEdits"` | 自动接受文件编辑 |
| `"dontAsk"` | 自动拒绝除预批准外的工具 |
| `"bypassPermissions"` | 跳过所有权限检查（危险） |
| `"plan"` | 只读探索模式 |

### 工具权限语法

| 工具 | 语法 | 示例 |
|------|------|------|
| `Bash` | `Bash(command pattern)` | `Bash(npm run *)`, `Bash(git *)` |
| `Read` | `Read(path pattern)` | `Read(.env)`, `Read(./secrets/**)` |
| `Edit` | `Edit(path pattern)` | `Edit(src/**)`, `Edit(*.ts)` |
| `Write` | `Write(path pattern)` | `Write(*.md)` |
| `WebFetch` | `WebFetch(domain:pattern)` | `WebFetch(domain:example.com)` |
| `MCP` | `mcp__server__tool` | `mcp__memory__*` |

**推荐**：使用通配符权限（如 `Bash(npm run *)`）替代 `dangerously-skip-permissions`。

---

## 沙箱配置

```json
{
  "sandbox": {
    "enabled": true,
    "autoAllowBashIfSandboxed": true,
    "excludedCommands": ["git", "docker", "gh"],
    "network": {
      "allowLocalBinding": true,
      "allowedDomains": ["api.example.com"]
    }
  }
}
```

---

## 计划目录与记忆

| 键 | 类型 | 描述 |
|-----|------|------|
| `plansDirectory` | string | `/plan` 输出存储目录（默认 `~/.claude/plans`） |
| `autoMemoryDirectory` | string | 自动记忆存储的自定义目录 |

---

## 归因设置

```json
{
  "attribution": {
    "commit": "Generated with AI\n\nCo-Authored-By: Claude <noreply@anthropic.com>",
    "pr": "Generated with Claude Code"
  }
}
```

设为空字符串 `""` 可完全隐藏归因。

---

## 显示与 UX

| 键 | 描述 |
|-----|------|
| `theme` | 颜色主题（`"dark"`, `"light"`, `"light-daltonized"`, `"dark-daltonized"`） |
| `outputStyle` | 输出风格（`"concise"`, `"normal"`, `"explanatory"`） |
| `spinnerVerbs` | 自定义加载动画文字 |
| `preferredNotifChannel` | 通知渠道（`"iterm2"`, `"terminal_bell"`, `"notifications_disabled"`） |

### 自定义 Spinner 示例

```json
{
  "spinnerVerbs": ["思考中", "分析中", "推理中", "编码中"]
}
```

---

## 参考来源

- [Claude Code 设置文档](https://code.claude.com/docs/en/settings)
- [Claude Code 权限文档](https://code.claude.com/docs/en/permissions)
- [Claude Code 沙箱文档](https://code.claude.com/docs/en/sandboxing)
