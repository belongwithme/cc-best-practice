# Boris 与团队推文精选

> Claude Code 核心团队的经验分享和最佳实践建议

---

## Boris Cherny（Claude Code 创建者）

### 关于 CLAUDE.md
- CLAUDE.md 建议保持在 200 行以内
- 使用 `.claude/rules/` 拆分长指令
- CLAUDE.md 不保证 100% 执行，但可显著提高一致性

### 关于工作流编排
- 使用 **Commands** 做编排入口，而非 Subagents
- Subagents 应该是**功能特定的**（如 code-reviewer），而非通用角色（如 "QA Agent"）
- 说 "use subagents" 可以让 Claude 自动分配研究任务

### 关于代码质量
- "we both know this isn't your best work" — 挑战 Claude 输出更高质量
- 先用 plan 模式规划，再执行
- 让 Claude 审查自己的 diff
- 始终提供测试和 linter 工具

### 关于 Agent Teams
- Agent Teams + tmux + git worktrees = 多代理并行开发
- 每个 Agent 在独立 worktree 中工作
- 通过环境变量 `CLAUDE_AGENT_TEAM_ID` 协调

---

## Thariq（Claude Code 团队）

### 关于功能开发
- Code Review 使用多代理 PR 分析
- Scheduled Tasks 可通过 `/loop` 实现定期监控
- Voice Mode 支持语音输入提示

### 关于技术选型
- MCP 服务器推荐按需配置，不要贪多
- 沙箱模式适合不信任环境
- 权限规则支持通配符，避免使用 `dangerously-skip-permissions`

---

## 社区贡献者精华

### 效率提升技巧
- `/compact` 是上下文管理的关键 — 规划后压缩再执行
- `/btw` 侧链对话不污染主上下文
- 截图粘贴比文字描述更高效
- 使用 `ultrathink` 触发深度推理

### 工作流推荐
- **RPI 工作流**：Research → Plan → Implement（3 阶段隔离）
- **Cross-Model 工作流**：Claude Code 写代码 + Codex 审查
- **Ralph Wiggum Loop**：设置目标 → 自主循环 → 持续迭代直到完成

### 常见陷阱
- 任务太大导致 Claude 跑偏 → 分解为小任务
- 上下文过长导致质量下降 → 定期 `/compact` 或 `/clear`
- 过度依赖 CLAUDE.md → 在提示中重复关键指令

---

## 推荐关注

| 人物 | 平台 | 链接 |
|------|------|------|
| Boris Cherny | Twitter/X | [x.com/bcherny](https://x.com/bcherny) |
| Thariq | Twitter/X | [x.com/trq212](https://x.com/trq212) |
| Claude Code | GitHub | [anthropics/claude-code](https://github.com/anthropics/claude-code) |
| r/ClaudeCode | Reddit | [reddit.com/r/ClaudeCode](https://reddit.com/r/ClaudeCode) |
