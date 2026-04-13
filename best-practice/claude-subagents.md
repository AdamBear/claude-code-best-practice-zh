# 子代理最佳实践

![Last Updated](https://img.shields.io/badge/Last_Updated-Apr%2011%2C%202026%206%3A10%20PM%20PKT-white?style=flat&labelColor=555) ![Version](https://img.shields.io/badge/Claude_Code-v2.1.101-blue?style=flat&labelColor=555)<br>
[![Implemented](https://img.shields.io/badge/Implemented-2ea44f?style=flat)](../implementation/claude-subagents-implementation.md)

Claude Code 子代理：frontmatter 字段与官方内置代理类型总览。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## Frontmatter 字段（16）

| 字段 | 类型 | 必填 | 说明 |
|-------|------|----------|-------------|
| `name` | string | 是 | 使用小写字母和连字符的唯一标识符 |
| `description` | string | 是 | 说明何时调用。使用 `"PROACTIVELY"` 可让 Claude 主动自动调用 |
| `tools` | string/list | 否 | 逗号分隔的工具白名单（如 `Read, Write, Edit, Bash`）。若省略则继承全部工具。支持 `Agent(agent_type)` 语法限制可派生的子代理；旧的 `Task(agent_type)` 别名仍可用 |
| `disallowedTools` | string/list | 否 | 要禁用的工具，会从继承或显式指定的列表中移除 |
| `model` | string | 否 | 使用的模型：`sonnet`、`opus`、`haiku`、完整模型 ID（如 `claude-opus-4-6`）或 `inherit`（默认即 `inherit`） |
| `permissionMode` | string | 否 | 权限模式：`default`、`acceptEdits`、`auto`、`dontAsk`、`bypassPermissions` 或 `plan` |
| `maxTurns` | integer | 否 | 子代理停止前允许的最大 agentic 轮次 |
| `skills` | list | 否 | 在代理启动时预加载到上下文中的技能名称（会注入完整内容，而不只是“可用”） |
| `mcpServers` | list | 否 | 该子代理可用的 MCP 服务器，可以是服务器名字符串，也可以是内联 `{name: config}` 对象 |
| `hooks` | object | 否 | 作用域限定在该子代理内的生命周期钩子。支持所有钩子事件，其中 `PreToolUse`、`PostToolUse` 和 `Stop` 最常见 |
| `memory` | string | 否 | 持久化记忆范围：`user`、`project` 或 `local` |
| `background` | boolean | 否 | 设为 `true` 时，始终以后台任务方式运行（默认：`false`） |
| `effort` | string | 否 | 当该子代理激活时覆盖 effort 等级：`low`、`medium`、`high`、`max`（仅 Opus 4.6）。默认继承会话设置 |
| `isolation` | string | 否 | 设为 `"worktree"` 时，在临时 git worktree 中运行（若无变更会自动清理） |
| `initialPrompt` | string | 否 | 当该代理作为主会话代理运行时（通过 `--agent` 或 `agent` 设置），会自动作为首条用户输入提交。命令和技能也会被处理，并且会在用户提供的提示词前拼接 |
| `color` | string | 否 | 子代理在任务列表和转录中的显示颜色：`red`、`blue`、`green`、`yellow`、`purple`、`orange`、`pink` 或 `cyan` |

---

## ![Official](../!/tags/official.svg) **(5)**

| # | 代理 | 模型 | 工具 | 说明 |
|---|-------|-------|-------|-------------|
| 1 | `general-purpose` | inherit | 全部 | 复杂多步骤任务的默认代理类型，适合研究、代码搜索与自主执行 |
| 2 | `Explore` | haiku | 只读（无 Write、Edit） | 用于快速搜索和探索代码库，擅长找文件、查代码、回答代码库问题 |
| 3 | `Plan` | inherit | 只读（无 Write、Edit） | plan 模式下的前置研究代理，在写代码前先探索代码库并设计实现方案 |
| 4 | `statusline-setup` | sonnet | Read、Edit | 配置用户的 Claude Code 状态栏设置 |
| 5 | `claude-code-guide` | haiku | Glob、Grep、Read、WebFetch、WebSearch | 回答与 Claude Code 功能、Agent SDK 和 Claude API 相关的问题 |

---

## 来源

- [Create custom subagents - Claude Code Docs](https://code.claude.com/docs/en/sub-agents)
- [CLI reference - Claude Code Docs](https://code.claude.com/docs/en/cli-reference)
- [Claude Code CHANGELOG](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
