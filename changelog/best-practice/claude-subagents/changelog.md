# 子代理报告变更历史

## 状态图例

| 状态 | 含义 |
|--------|---------|
| `COMPLETE (reason)` | 已执行并成功解决 |
| `INVALID (reason)` | 结论不正确、不适用，或当前状态属预期 |
| `ON HOLD (reason)` | 已暂缓处理，等待外部依赖或用户决定 |

---

## [2026-02-28 03:22 PM PKT] Claude Code v2.1.63

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | Agents 表 | 将 `workflow-changelog-claude-agents-frontmatter-agent` 加入 “Agents in This Repository” 表 | COMPLETE（已加入；model: opus，继承全部工具，无技能/记忆） |
| 2 | HIGH | Agents 表 | 修正 presentation-curator 的 skills 列，给技能名加上 `presentation/` 前缀 | COMPLETE（已更新为 `presentation/vibe-to-agentic-framework` 等） |
| 3 | MED | 字段文档 | 在 `color` 字段中补充说明：该字段可用，但不在官方 frontmatter 表里 | COMPLETE（已在 description 列加入官方未列出的说明） |
| 4 | MED | 调用章节 | 扩展调用章节，加入 `--agents` CLI 标志、`/agents` 命令、`claude agents` CLI 以及 agent 恢复 | COMPLETE（已新增包含 5 种方式的调用表） |

---

## [2026-03-07 08:35 AM PKT] Claude Code v2.1.71

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 失效链接 | 修复 agent memory 指向 `reports/claude-agent-memory.md` 的链接 | COMPLETE |
| 2 | HIGH | 行为变更 | 更新 `tools` 字段说明：`Task(agent_type)` → `Agent(agent_type)`（v2.1.63 更名） | COMPLETE |
| 3 | HIGH | 行为变更 | 更新调用章节：Task 工具 → Agent 工具（v2.1.63 更名） | COMPLETE（已更新标题、代码示例，并加入更名说明） |
| 4 | HIGH | 示例更新 | 更新完整示例：`Task(monitor, rollback)` → `Agent(monitor, rollback)` | COMPLETE |
| 5 | HIGH | 内置 Agent | 在 Official Claude Agents 表中加入 `Bash` agent（model: inherit；用途：在独立上下文中执行终端命令） | COMPLETE（已加入表格） |
| 6 | HIGH | Agents 表 | 将 `workflow-concepts-agent` 加入 “Agents in This Repository” 表（model: opus，color: green） | COMPLETE |
| 7 | HIGH | Agents 表 | 将 `workflow-claude-settings-agent` 加入 “Agents in This Repository” 表（model: opus，color: yellow） | COMPLETE |
| 8 | MED | 内置 Agent | 修正 `statusline-setup` 的 model：`inherit` → `Sonnet` | COMPLETE |
| 9 | MED | 内置 Agent | 修正 `claude-code-guide` 的 model：`inherit` → `Haiku` | INVALID（该项已从表中移除，不适用） |
| 10 | MED | Agents 表 | 修正 `weather-agent` 的 color：`teal` → `green` | COMPLETE |
| 11 | MED | 调用方式 | 在调用方式表中加入 `--agent <name>` CLI 标志 | COMPLETE（已作为第一行加入） |
| 12 | MED | 行为变更 | 更新第 147 行文本：“Task tool” → “Agent tool”，位于 Official Claude Agents 表头 | COMPLETE（用户已重写标题文本） |
| 13 | MED | 跨文件 | 更新 CLAUDE.md 中的 `Task(...)` → `Agent(...)` 引用（第 50-53、61 行） | COMPLETE（已更新编排章节和 tools 字段说明） |

---

## [2026-03-12 12:17 PM PKT] Claude Code v2.1.74

未发现漂移。报告已与官方文档完全同步：13 个 frontmatter 字段和 6 个内置 agent 全部匹配。

---

## [2026-03-13 04:21 PM PKT] Claude Code v2.1.74

未发现漂移。报告已与官方文档完全同步：13 个 frontmatter 字段和 6 个内置 agent 全部匹配。

---

## [2026-03-15 12:50 PM PKT] Claude Code v2.1.76

未发现漂移。报告已与官方文档完全同步：13 个 frontmatter 字段和 6 个内置 agent 全部匹配。

---

## [2026-03-17 12:42 PM PKT] Claude Code v2.1.77

未发现漂移。报告已与官方文档完全同步：13 个 frontmatter 字段和 6 个内置 agent 全部匹配。

---

## [2026-03-18 11:41 PM PKT] Claude Code v2.1.78

未发现漂移。报告已与官方文档完全同步：13 个 frontmatter 字段和 6 个内置 agent 全部匹配。

---

## [2026-03-19 11:56 AM PKT] Claude Code v2.1.79

未发现漂移。报告已与官方文档完全同步：13 个 frontmatter 字段和 6 个内置 agent 全部匹配。

---

## [2026-03-20 08:35 AM PKT] Claude Code v2.1.80

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 在 Frontmatter Fields 表中加入 `effort` 字段（string，可选；用于覆盖努力程度：`low`、`medium`、`high`、`max`） | COMPLETE（已加入 `background` 与 `isolation` 之间，计数从 14 更新为 15） |

---

## [2026-03-21 09:07 PM PKT] Claude Code v2.1.81

未发现漂移。报告已与官方文档完全同步：15 个 frontmatter 字段和 6 个内置 agent 全部匹配。

---

## [2026-03-23 09:49 PM PKT] Claude Code v2.1.81

未发现漂移。报告已与官方文档完全同步：15 个 frontmatter 字段（14 个官方字段 + 1 个非官方 `color`）和 6 个内置 agent 全部匹配。

---

## [2026-03-25 08:07 PM PKT] Claude Code v2.1.83

未发现漂移。报告已与官方文档完全同步：15 个 frontmatter 字段（14 个官方字段 + 1 个非官方 `color`）和 6 个内置 agent 全部匹配。

**观察项：** `initialPrompt` 已出现在 v2.1.83 changelog 中，但尚未进入官方文档支持的 frontmatter 字段表。一旦进入，报告需要更新。

---

## [2026-03-26 01:01 PM PKT] Claude Code v2.1.84

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 在 Frontmatter Fields 表中加入 `initialPrompt` 字段（string，可选；当 agent 作为主会话 agent 通过 `--agent` 或 `agent` 设置运行时，会自动作为第一条用户消息提交） | COMPLETE（已加入 `isolation` 与 `color` 之间，计数从 15 更新为 16） |

---

## [2026-03-27 06:28 PM PKT] Claude Code v2.1.85

未发现漂移。报告已与官方文档完全同步：16 个 frontmatter 字段（15 个官方字段 + 1 个非官方 `color`）和 6 个内置 agent 全部匹配。

---

## [2026-03-28 06:00 PM PKT] Claude Code v2.1.86

未发现漂移。报告已与官方文档完全同步：16 个 frontmatter 字段（15 个官方字段 + 1 个非官方 `color`）和 6 个内置 agent 全部匹配。

---

## [2026-04-01 12:26 PM PKT] Claude Code v2.1.89

未发现漂移。报告已与官方文档完全同步：16 个 frontmatter 字段（15 个官方字段 + 1 个非官方 `color`）和 6 个内置 agent 全部匹配。

---

## [2026-04-02 09:11 PM PKT] Claude Code v2.1.90

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 移除 Agent | 从 Official Claude Agents 表中移除 `Bash`，官方文档只列出 5 个内置 agent，`Bash` 不在其中 | COMPLETE（已移除 Bash 行，并重新编号） |
| 2 | LOW | 字段文档 | 更新 `color` 字段说明，移除 “不在官方 frontmatter 表中” 备注；`color` 现在已经出现在官方支持的 frontmatter 字段表里 | COMPLETE（已移除非官方说明） |

---

## [2026-04-03 08:30 PM PKT] Claude Code v2.1.91

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | LOW | 字段文档 | 更新 `permissionMode` 字段说明，加入 `auto` 作为有效值（官方文档现列出：`default`、`acceptEdits`、`auto`、`dontAsk`、`bypassPermissions`、`plan`） | COMPLETE（已在 permissionMode 描述中将 `auto` 插入 `acceptEdits` 与 `dontAsk` 之间） |

---

## [2026-04-04 10:43 PM PKT] Claude Code v2.1.92

未发现漂移。报告已与官方文档完全同步：16 个 frontmatter 字段和 5 个内置 agent 全部匹配。

---

## [2026-04-08 09:34 PM PKT] Claude Code v2.1.96

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | LOW | 字段文档 | 更新 `model` 字段说明，补充支持完整 model ID（例如 `claude-opus-4-6`）以及别名 | COMPLETE（已按官方文档措辞更新说明） |
| 2 | LOW | 字段文档 | 更新 `effort` 字段说明，为 `max` 增加 `（仅 Opus 4.6）` 限定 | COMPLETE（已为 max 选项加入 Opus 4.6 限定） |
| 3 | LOW | 字段文档 | 更新 `color` 字段说明，将 `(e.g., green, magenta)` 替换为完整合法值列表：`red`、`blue`、`green`、`yellow`、`purple`、`orange`、`pink`、`cyan` | COMPLETE（已用完整可选值列表替换示例式说明） |

---

## [2026-04-09 11:34 PM PKT] Claude Code v2.1.97

未发现漂移。报告已与官方文档完全同步：16 个 frontmatter 字段和 5 个内置 agent 全部匹配。

---

## [2026-04-11 06:10 PM PKT] Claude Code v2.1.101

未发现漂移。报告已与官方文档完全同步：16 个 frontmatter 字段和 5 个内置 agent 全部匹配。
