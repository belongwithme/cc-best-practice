# Commands 命令最佳实践

> 来源：[best-practice/claude-commands.md](https://github.com/shanraisshan/claude-code-best-practice/blob/main/best-practice/claude-commands.md)

Claude Code 命令 — 前置字段（frontmatter）与官方内置斜杠命令。

---

## 前置字段（4 个）

| 字段 | 类型 | 必需 | 描述 |
|------|------|------|------|
| `description` | string | 推荐 | 命令功能描述，在自动补全中显示，Claude 用于自动发现 |
| `argument-hint` | string | 否 | 自动补全时显示的提示（如 `[issue-number]`, `[filename]`） |
| `allowed-tools` | string | 否 | 此命令激活时允许无需权限确认的工具 |
| `model` | string | 否 | 运行此命令时使用的模型（如 `haiku`, `sonnet`, `opus`） |

---

## 官方内置命令（62 个）

### 认证类 (Auth)
| # | 命令 | 描述 |
|---|------|------|
| 1 | `/login` | 通过 OAuth 认证 Claude Code |
| 2 | `/logout` | 登出 Claude Code |
| 3 | `/upgrade` | 打开升级页面切换更高计划 |

### 配置类 (Config)
| # | 命令 | 描述 |
|---|------|------|
| 4 | `/color [color\|default]` | 设置当前会话的提示栏颜色 |
| 5 | `/config` | 打开带搜索的交互式设置界面 |
| 6 | `/keybindings` | 自定义快捷键 |
| 7 | `/permissions` | 查看或更新工具权限 |
| 8 | `/privacy-settings` | 管理隐私和遥测偏好 |
| 9 | `/sandbox` | 配置沙箱及依赖状态 |
| 10 | `/statusline` | 设置状态栏 UI |
| 11 | `/stickers` | 订购 Claude Code 贴纸 |
| 12 | `/terminal-setup` | 在 IDE 终端中启用 shift+enter 换行 |
| 13 | `/theme` | 更改颜色主题 |
| 14 | `/vim` | 启用 vim 风格编辑模式 |

### 上下文类 (Context)
| # | 命令 | 描述 |
|---|------|------|
| 15 | `/context` | 以彩色网格可视化当前上下文用量和 token 计数 |
| 16 | `/cost` | 显示当前会话的 token 使用统计 |
| 17 | `/extra-usage` | 配置订阅计划的按量计费溢出 |
| 18 | `/insights` | 生成 Claude Code 会话分析报告 |
| 19 | `/stats` | 可视化每日使用量、会话历史和模型偏好 |
| 20 | `/status` | 打开设置界面显示版本、模型、账户和连接状态 |
| 21 | `/usage` | 显示计划使用限制和速率限制状态 |

### 调试类 (Debug)
| # | 命令 | 描述 |
|---|------|------|
| 22 | `/doctor` | 检查 Claude Code 安装健康状况 |
| 23 | `/feedback [description]` | 生成 GitHub issue URL 用于报告 bug |
| 24 | `/help` | 显示斜杠命令帮助 |
| 25 | `/release-notes` | 显示最近的发布说明 |
| 26 | `/tasks` | 列出和管理后台任务 |

### 导出类 (Export)
| # | 命令 | 描述 |
|---|------|------|
| 27 | `/copy` | 复制最后一条助手响应到剪贴板 |
| 28 | `/export [filename]` | 导出当前对话到文件或剪贴板 |

### 扩展类 (Extensions)
| # | 命令 | 描述 |
|---|------|------|
| 29 | `/agents` | 管理自定义子代理 — 查看、创建、编辑、删除 |
| 30 | `/chrome` | 管理 Chrome 浏览器集成 |
| 31 | `/hooks` | 管理钩子配置 |
| 32 | `/ide` | 连接 IDE 集成 |
| 33 | `/mcp` | 管理 MCP 服务器连接 |
| 34 | `/plugin` | 管理 Claude Code 插件 |
| 35 | `/reload-plugins` | 重新加载已安装插件 |
| 36 | `/skills` | 列出可用技能 |

### 记忆类 (Memory)
| # | 命令 | 描述 |
|---|------|------|
| 37 | `/memory` | 查看和编辑记忆文件 |

### 模型类 (Model)
| # | 命令 | 描述 |
|---|------|------|
| 38 | `/effort [low\|medium\|high\|max\|auto]` | 设置模型推理深度 |
| 39 | `/fast` | 切换快速模式 — 同一 Opus 4.6 模型更快输出 |
| 40 | `/model` | 切换模型（haiku, sonnet, opus）和调整推理深度 |
| 41 | `/passes [number]` | 分享 Claude Code 免费周给朋友 |
| 42 | `/plan` | 进入只读计划模式 — 只建议不修改 |

### 项目类 (Project)
| # | 命令 | 描述 |
|---|------|------|
| 43 | `/add-dir` | 添加额外工作目录到当前会话 |
| 44 | `/diff` | 查看活跃仓库的当前 git diff |
| 45 | `/init` | 用 CLAUDE.md 指南初始化新项目 |
| 46 | `/pr-comments` | 查看或回复 PR 评论 |
| 47 | `/review` | 已弃用 — 改用 `code-review` 插件 |
| 48 | `/security-review` | 对当前变更运行安全审查 |

### 远程类 (Remote)
| # | 命令 | 描述 |
|---|------|------|
| 49 | `/desktop` | 在 Claude Code 桌面应用中继续会话 |
| 50 | `/install-github-app` | 安装 GitHub App |
| 51 | `/install-slack-app` | 安装 Slack App |
| 52 | `/mobile` | 连接移动伴侣应用 |
| 53 | `/remote-control` | 从另一设备继续会话 |
| 54 | `/remote-env` | 检查或复制远程控制环境设置 |

### 会话类 (Session)
| # | 命令 | 描述 |
|---|------|------|
| 55 | `/btw <question>` | 不加入对话地快速提问侧链 |
| 56 | `/clear` | 清除对话历史重新开始 |
| 57 | `/compact [prompt]` | 压缩对话以释放上下文窗口 |
| 58 | `/exit` | 退出 REPL |
| 59 | `/fork` | 将当前对话分叉到新会话 |
| 60 | `/rename <name>` | 重命名当前会话 |
| 61 | `/resume [session]` | 恢复之前的对话 |
| 62 | `/rewind` | 回退对话和/或代码到之前的点 |

> 注意：捆绑技能如 `/debug` 也会出现在斜杠命令菜单中，但它们不是内置命令。

---

## 参考来源

- [Claude Code 斜杠命令文档](https://code.claude.com/docs/en/slash-commands)
- [Claude Code 交互模式](https://code.claude.com/docs/en/interactive-mode)
- [Claude Code CHANGELOG](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
