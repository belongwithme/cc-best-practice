# MCP 服务器最佳实践

> 来源：[best-practice/claude-mcp.md](https://github.com/shanraisshan/claude-code-best-practice/blob/main/best-practice/claude-mcp.md)

MCP（Model Context Protocol）服务器扩展 Claude Code 与外部工具、数据库和 API 的连接。

---

## 日常推荐 MCP 服务器

> "装了 15 个 MCP 服务器以为越多越好，结果每天只用 4 个。" — [r/mcp](https://reddit.com/r/mcp/comments/1mj0fxs/)（682 赞）

| MCP 服务器 | 功能 | 资源 |
|------------|------|------|
| [**Context7**](https://github.com/upstash/context7) | 获取最新的库文档到上下文。防止过时训练数据导致的 API 幻觉 | [Reddit](https://reddit.com/r/mcp/comments/1qarjqm/) |
| [**Playwright**](https://github.com/microsoft/playwright-mcp) | 浏览器自动化 — 实现、测试和验证 UI 功能。截图、导航、表单测试 | [文档](https://playwright.dev/) |
| [**Claude in Chrome**](https://github.com/nicobailon/claude-code-in-chrome-mcp) | 连接到真实 Chrome 浏览器 — 检查控制台、网络、DOM | [Reddit](https://reddit.com/r/mcp/comments/1qarjqm/) |
| [**DeepWiki**](https://github.com/devanshusemwal/deepwiki-mcp) | 获取任何 GitHub 仓库的结构化 wiki 文档 | [GitHub](https://github.com/devanshusemwal/deepwiki-mcp) |
| [**Excalidraw**](https://github.com/antonpk1/excalidraw-mcp-app) | 从提示生成架构图、流程图和系统设计 | [GitHub](https://github.com/antonpk1/excalidraw-mcp-app) |

**使用链路**：Research (Context7/DeepWiki) → Debug (Playwright/Chrome) → Document (Excalidraw)

---

## 配置

MCP 服务器在项目根目录的 `.mcp.json`（项目范围）或 `~/.claude.json`（用户范围）中配置。

### 服务器类型

| 类型 | 传输方式 | 示例 |
|------|----------|------|
| **stdio** | 启动本地进程 | `npx`, `python`, 二进制文件 |
| **http** | 连接远程 URL | HTTP/SSE 端点 |

### 示例 `.mcp.json`

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"]
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp"]
    },
    "deepwiki": {
      "command": "npx",
      "args": ["-y", "deepwiki-mcp"]
    },
    "remote-api": {
      "type": "http",
      "url": "https://mcp.example.com/mcp"
    }
  }
}
```

### 密钥处理

使用环境变量扩展，避免在 `.mcp.json` 中提交 API 密钥：

```json
{
  "mcpServers": {
    "remote-api": {
      "type": "http",
      "url": "https://mcp.example.com/mcp?token=${MCP_API_TOKEN}"
    }
  }
}
```

---

## MCP 设置项

在 `.claude/settings.json` 中控制 MCP 服务器审批：

| 键 | 类型 | 描述 |
|-----|------|------|
| `enableAllProjectMcpServers` | boolean | 自动批准所有 `.mcp.json` 服务器 |
| `enabledMcpjsonServers` | array | 自动批准的服务器名称白名单 |
| `disabledMcpjsonServers` | array | 拒绝的服务器名称黑名单 |

### MCP 工具权限规则

MCP 工具在权限规则中遵循 `mcp__<server>__<tool>` 命名约定：

```json
{
  "permissions": {
    "allow": [
      "mcp__*",
      "mcp__context7__*",
      "mcp__playwright__browser_snapshot"
    ],
    "deny": [
      "mcp__dangerous-server__*"
    ]
  }
}
```

---

## MCP 作用域

| 范围 | 位置 | 用途 |
|------|------|------|
| **项目** | `.mcp.json`（仓库根目录） | 团队共享服务器，提交到 git |
| **用户** | `~/.claude.json`（`mcpServers` 键） | 跨所有项目的个人服务器 |
| **子代理** | Agent frontmatter（`mcpServers` 字段） | 作用域为特定子代理的服务器 |

**优先级**：子代理 > 项目 > 用户

---

## 参考来源

- [MCP 服务器 — Claude Code 文档](https://code.claude.com/docs/en/mcp)
- [Model Context Protocol 规范](https://modelcontextprotocol.io/)
- [5 个让我效率提升 10 倍的 MCP — r/mcp](https://reddit.com/r/mcp/comments/1qarjqm/)
