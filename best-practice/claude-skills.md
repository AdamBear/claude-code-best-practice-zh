# 技能最佳实践

![Last Updated](https://img.shields.io/badge/Last_Updated-Apr%2011%2C%202026%206%3A08%20PM%20PKT-white?style=flat&labelColor=555) ![Version](https://img.shields.io/badge/Claude_Code-v2.1.101-blue?style=flat&labelColor=555)<br>
[![Implemented](https://img.shields.io/badge/Implemented-2ea44f?style=flat)](../implementation/claude-skills-implementation.md)

Claude Code 技能：frontmatter 字段与官方内置技能总览。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## Frontmatter 字段（13）

| 字段 | 类型 | 必填 | 说明 |
|-------|------|----------|-------------|
| `name` | string | 否 | 显示名称与 `/slash-command` 标识符。若省略，默认使用目录名 |
| `description` | string | 建议填写 | 技能的作用。会显示在自动补全中，也会被 Claude 用于自动发现 |
| `argument-hint` | string | 否 | 自动补全时显示的参数提示（例如 `[issue-number]`、`[filename]`） |
| `disable-model-invocation` | boolean | 否 | 设为 `true` 可阻止 Claude 自动调用这个技能 |
| `user-invocable` | boolean | 否 | 设为 `false` 可将其从 `/` 菜单中隐藏，此时技能只作为后台知识存在，适合给代理预加载 |
| `allowed-tools` | string | 否 | 技能激活时无需权限提示即可使用的工具 |
| `model` | string | 否 | 运行该技能时使用的模型（如 `haiku`、`sonnet`、`opus`） |
| `effort` | string | 否 | 调用时覆盖模型的 effort 等级（`low`、`medium`、`high`、`max`） |
| `context` | string | 否 | 设为 `fork` 时，在隔离的子代理上下文中运行该技能 |
| `agent` | string | 否 | 当设置 `context: fork` 时使用的子代理类型（默认：`general-purpose`） |
| `hooks` | object | 否 | 作用域限定在该技能内的生命周期钩子 |
| `paths` | string/list | 否 | 限制技能自动激活时机的 Glob 模式。支持逗号分隔字符串或 YAML 列表，Claude 仅在处理匹配文件时自动加载此技能 |
| `shell` | string | 否 | `` !`command` `` 代码块使用的 shell，可为 `bash`（默认）或 `powershell`。需要 `CLAUDE_CODE_USE_POWERSHELL_TOOL=1` |

---

## ![Official](../!/tags/official.svg) **(5)**

| # | 技能 | 说明 |
|---|-------|-------------|
| 1 | `simplify` | 复查变更代码的复用性、质量与效率，并通过重构消除重复 |
| 2 | `batch` | 批量对多个文件执行命令 |
| 3 | `debug` | 调试失败的命令或代码问题 |
| 4 | `loop` | 按固定间隔重复运行一个提示词或斜杠命令（最长 3 天） |
| 5 | `claude-api` | 使用 Claude API 或 Anthropic SDK 构建应用；遇到 `anthropic` / `@anthropic-ai/sdk` 导入时会触发 |

另见：[官方 Skills 仓库](https://github.com/anthropics/skills/tree/main/skills)，其中提供了由社区维护、可安装的技能。

---

## 来源

- [Claude Code Skills - Docs](https://code.claude.com/docs/en/skills)
- [Skills Discovery in Monorepos](../reports/claude-skills-for-larger-mono-repos.md)
- [Claude Code CHANGELOG](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
