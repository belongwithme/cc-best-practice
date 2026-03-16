# CLI 启动参数最佳实践

> 来源：[best-practice/claude-cli-startup-flags.md](https://github.com/shanraisshan/claude-code-best-practice/blob/main/best-practice/claude-cli-startup-flags.md)

Claude Code CLI 启动标志、子命令和环境变量完整参考。

---

## 会话管理

| 标志 | 描述 |
|------|------|
| `--resume, -r [session-id]` | 恢复之前的会话 |
| `--continue, -c` | 继续最近的会话 |
| `--session-name <name>` | 指定新会话名称 |
| `--new-session, -n` | 强制新建会话 |

---

## 模型与配置

| 标志 | 描述 |
|------|------|
| `--model <model>` | 覆盖默认模型 |
| `--effort <level>` | 设置推理深度（`low`, `medium`, `high`, `max`, `auto`） |
| `--fast` | 启用快速模式 |
| `--thinking-budget <tokens>` | 设置思考预算 token 数 |
| `--agent <name>` | 使用指定子代理作为主代理 |
| `--permission-mode <mode>` | 设置权限模式（`default`, `acceptEdits`, `dontAsk`, `bypassPermissions`, `plan`） |

---

## 权限与安全

| 标志 | 描述 |
|------|------|
| `--allowedTools <tools>` | 允许的工具白名单（逗号分隔） |
| `--disallowedTools <tools>` | 禁止的工具黑名单 |
| `--dangerously-skip-permissions` | 跳过所有权限检查（⚠️ 危险） |
| `--sandbox` | 启用沙箱模式 |
| `--no-sandbox` | 禁用沙箱模式 |

---

## 输出与格式

| 标志 | 描述 |
|------|------|
| `--output-format <format>` | 输出格式：`text`, `json`, `stream-json` |
| `--verbose` | 启用详细日志 |
| `--max-turns <n>` | 非交互模式的最大代理轮次 |
| `--no-user-input` | 禁止用户输入提示（CI/CD 模式） |

---

## 系统提示

| 标志 | 描述 |
|------|------|
| `--system-prompt <prompt>` | 覆盖系统提示 |
| `--append-system-prompt <prompt>` | 追加到系统提示 |

---

## Agent 与 Subagent

| 标志 | 描述 |
|------|------|
| `--agent <name>` | 使用指定代理 |
| `--max-sub-agent-turns <n>` | 限制子代理轮次 |

---

## MCP 与插件

| 标志 | 描述 |
|------|------|
| `--mcp-config <path>` | 指定 MCP 配置文件路径 |
| `--disable-mcp` | 禁用所有 MCP 服务器 |
| `--plugin <names>` | 安装/启用插件（逗号分隔） |

---

## 目录与工作区

| 标志 | 描述 |
|------|------|
| `--add-dir <path>` | 添加额外工作目录 |
| `--project-dir <path>` | 指定项目根目录 |
| `--worktree` | 在 git worktree 中运行 |

---

## 预算与限制

| 标志 | 描述 |
|------|------|
| `--max-cost <dollars>` | 设置最大花费限制（美元） |
| `--max-tokens <n>` | 设置最大 token 限制 |
| `--max-file-edit-tokens <n>` | 单次文件编辑的 token 限制 |

---

## 初始化与维护

| 标志 | 描述 |
|------|------|
| `--init` | 初始化项目（创建 CLAUDE.md 等） |
| `--upgrade` | 升级到最新版本 |
| `--version` | 显示版本号 |
| `--help` | 显示帮助 |

---

## 重要子命令

| 子命令 | 描述 |
|--------|------|
| `claude config` | 管理设置 |
| `claude mcp` | 管理 MCP 服务器 |
| `claude plugin` | 管理插件 |
| `claude api` | 发送 Claude API 请求 |
| `claude export` | 导出会话 |

---

## 常用环境变量

| 变量 | 描述 |
|------|------|
| `CLAUDE_MODEL` | 默认模型 |
| `CLAUDE_CODE_MAX_TURNS` | 非交互模式最大轮次 |
| `CLAUDE_CODE_USE_BEDROCK` | 使用 AWS Bedrock 后端 |
| `CLAUDE_CODE_USE_VERTEX` | 使用 GCP Vertex 后端 |
| `ANTHROPIC_API_KEY` | API 密钥 |
| `ANTHROPIC_BASE_URL` | 自定义 API 端点 |
| `DISABLE_PROMPT_CACHING` | 禁用提示缓存 |
| `MCP_TIMEOUT` | MCP 服务器超时（毫秒） |
| `CLAUDE_CODE_SKIP_MCP` | 跳过 MCP 初始化 |
| `CLAUDE_AGENT_TEAM_ID` | Agent Team 团队 ID |
| `CLAUDE_AGENT_TEAM_MEMBER_ID` | Agent Team 成员 ID |
| `CLAUDE_FAST_MODE` | 启用快速模式 |

---

## 参考来源

- [Claude Code CLI 参考](https://code.claude.com/docs/en/cli-reference)
- [Claude Code 环境变量](https://code.claude.com/docs/en/cli-reference#environment-variables)
