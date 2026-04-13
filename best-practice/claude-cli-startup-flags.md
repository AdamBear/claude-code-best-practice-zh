# CLI 启动参数最佳实践

![Last Updated](https://img.shields.io/badge/Last_Updated-Mar%2002%2C%202026-white?style=flat&labelColor=555)

这是一份从终端启动 Claude Code 时可用启动参数、顶层子命令和启动阶段环境变量的参考。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 目录

1. [会话管理](#会话管理)
2. [模型与配置](#模型与配置)
3. [权限与安全](#权限与安全)
4. [输出与格式](#输出与格式)
5. [系统提示词](#系统提示词)
6. [代理与子代理](#代理与子代理)
7. [MCP 与插件](#mcp-与插件)
8. [目录与工作区](#目录与工作区)
9. [预算与限制](#预算与限制)
10. [集成](#集成)
11. [初始化与维护](#初始化与维护)
12. [调试与诊断](#调试与诊断)
13. [设置覆盖](#设置覆盖)
14. [版本与帮助](#版本与帮助)
15. [子命令](#子命令)
16. [环境变量](#环境变量)

---

## 会话管理

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--continue` | `-c` | 继续当前目录中的最近一次会话 |
| `--resume` | `-r` | 按 ID 或名称恢复指定会话，或显示交互式选择器 |
| `--from-pr <NUMBER\|URL>` | | 恢复与特定 GitHub PR 关联的会话 |
| `--fork-session` | | 恢复会话时创建新的 session ID（与 `--resume` 或 `--continue` 配合使用） |
| `--session-id <UUID>` | | 使用指定 session ID（必须是合法 UUID） |
| `--no-session-persistence` | | 禁用会话持久化（仅 print 模式） |
| `--remote` | | 在 claude.ai 上创建新的 Web 会话 |
| `--teleport` | | 在本地终端中恢复一个 Web 会话 |

---

## 模型与配置

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--model <NAME>` | | 使用别名（`sonnet`、`opus`、`haiku`）或完整模型 ID 指定模型 |
| `--fallback-model <NAME>` | | 当默认模型过载时自动切换的备用模型（仅 print 模式） |
| `--betas <LIST>` | | 要附加到 API 请求中的 beta headers（仅 API Key 用户可用） |

---

## 权限与安全

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--dangerously-skip-permissions` | | 跳过**所有**权限提示，务必极度谨慎使用 |
| `--allow-dangerously-skip-permissions` | | 允许把权限绕过作为一个可选项，但不立即启用 |
| `--permission-mode <MODE>` | | 以指定权限模式启动：`default`、`plan`、`acceptEdits`、`bypassPermissions` |
| `--allowedTools <TOOLS>` | | 无需提示即可执行的工具（使用权限规则语法） |
| `--disallowedTools <TOOLS>` | | 从模型上下文中彻底移除的工具 |
| `--tools <TOOLS>` | | 限制 Claude 可用的内置工具（用 `""` 可禁用全部） |
| `--permission-prompt-tool <TOOL>` | | 在非交互模式下，指定处理权限提示的 MCP 工具 |

---

## 输出与格式

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--print` | `-p` | 直接输出响应，不进入交互模式（headless / SDK 模式） |
| `--output-format <FORMAT>` | | 输出格式：`text`、`json`、`stream-json` |
| `--input-format <FORMAT>` | | 输入格式：`text`、`stream-json` |
| `--json-schema <SCHEMA>` | | 输出符合指定 schema 的校验后 JSON（仅 print 模式） |
| `--include-partial-messages` | | 包含部分流式事件（需要 `--print` 且 `--output-format=stream-json`） |
| `--verbose` | | 启用详细日志，输出完整逐轮信息 |

---

## 系统提示词

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--system-prompt <TEXT>` | | 用自定义文本替换整个系统提示词 |
| `--system-prompt-file <PATH>` | | 从文件加载系统提示词并替换默认值（仅 print 模式） |
| `--append-system-prompt <TEXT>` | | 在默认系统提示词后追加自定义文本 |
| `--append-system-prompt-file <PATH>` | | 将文件内容追加到默认提示词后（仅 print 模式） |

---

## 代理与子代理

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--agent <NAME>` | | 为当前会话指定代理 |
| `--agents <JSON>` | | 通过 JSON 动态定义自定义子代理 |
| `--teammate-mode <MODE>` | | 设置代理团队显示方式：`auto`、`in-process`、`tmux` |

---

## MCP 与插件

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--mcp-config <PATH\|JSON>` | | 从 JSON 文件或 JSON 字符串加载 MCP 服务器 |
| `--strict-mcp-config` | | 仅使用 `--mcp-config` 指定的 MCP 服务器，忽略其他来源 |
| `--plugin-dir <PATH>` | | 仅在当前会话中从指定目录加载插件（可重复传入） |

---

## 目录与工作区

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--add-dir <PATH>` | | 增加 Claude 可访问的工作目录 |
| `--worktree` | `-w` | 在隔离的 git worktree 中启动 Claude（基于当前 HEAD 分出） |

---

## 预算与限制

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--max-budget-usd <AMOUNT>` | | API 调用累计到指定美元金额后停止（仅 print 模式） |
| `--max-turns <NUMBER>` | | 限制 agentic 轮次数（仅 print 模式） |

---

## 集成

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--chrome` | | 启用 Chrome 浏览器集成以进行 Web 自动化 |
| `--no-chrome` | | 在当前会话中禁用 Chrome 浏览器集成 |
| `--ide` | | 启动时若恰好存在一个可用 IDE，则自动连接 |

---

## 初始化与维护

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--init` | | 运行初始化钩子并进入交互模式 |
| `--init-only` | | 仅运行初始化钩子后退出（不进入交互会话） |
| `--maintenance` | | 运行维护钩子后退出 |

---

## 调试与诊断

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--debug <CATEGORIES>` | | 启用调试模式，并可选择按类别过滤（例如 `"api,hooks"`） |

---

## 设置覆盖

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--settings <PATH\|JSON>` | | 要加载的 settings JSON 文件路径或 JSON 字符串 |
| `--setting-sources <LIST>` | | 要加载的来源列表，逗号分隔：`user`、`project`、`local` |
| `--disable-slash-commands` | | 在当前会话中禁用所有技能和斜杠命令 |

---

## 版本与帮助

| 参数 | 短参数 | 说明 |
|------|-------|-------------|
| `--version` | `-v` | 输出版本号 |
| `--help` | `-h` | 显示帮助信息 |

---

## 子命令

这些是以 `claude <subcommand>` 形式运行的顶层命令：

| 子命令 | 说明 |
|------------|-------------|
| `claude` | 启动交互式 REPL |
| `claude "query"` | 带初始提示词启动 REPL |
| `claude agents` | 列出已配置的代理 |
| `claude auth` | 管理 Claude Code 认证 |
| `claude doctor` | 从命令行运行诊断 |
| `claude install` | 安装或切换 Claude Code 原生构建版本 |
| `claude mcp` | 配置 MCP 服务器（`add`、`remove`、`list`、`get`、`enable`） |
| `claude plugin` | 管理 Claude Code 插件 |
| `claude remote-control` | 管理远程控制会话 |
| `claude setup-token` | 为订阅使用创建长期有效 token |
| `claude update` / `claude upgrade` | 更新到最新版本 |

---

## 环境变量

这些仅在启动阶段生效的环境变量，需要在 shell 中先设置好再启动 Claude Code（不能通过 `settings.json` 配置）：

| 变量 | 说明 |
|----------|-------------|
| `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` | 启用实验性的 agent teams |
| `CLAUDE_CODE_TMPDIR` | 覆盖内部临时文件使用的临时目录。也可通过 `env` 键配置，参见 [设置参考](./claude-settings.md#environment-variables-via-env) |
| `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1` | 启用附加目录中的 `CLAUDE.md` 加载 |
| `DISABLE_AUTOUPDATER=1` | 禁用自动更新 |
| `CLAUDE_CODE_EFFORT_LEVEL` | 控制思考深度，参见 [设置参考](./claude-settings.md#environment-variables-via-env) |
| `USE_BUILTIN_RIPGREP=0` | 使用系统 ripgrep 而不是内置版本（适用于 Alpine Linux） |
| `CLAUDE_CODE_SIMPLE` | 启用简化模式（仅 Bash + Edit 工具）。也可通过 `env` 键配置，参见 [设置参考](./claude-settings.md#environment-variables-via-env) |
| `CLAUDE_BASH_NO_LOGIN=1` | 让 BashTool 跳过 login shell |
| `CCR_FORCE_BUNDLE=1` | 使用 `claude --remote` 时，强制打包并上传本地仓库 |

对于可通过 `settings.json` 中 `"env"` 键配置的环境变量（包括 `MAX_THINKING_TOKENS`、`CLAUDE_CODE_SHELL`、`CLAUDE_CODE_ENABLE_TASKS`、`CLAUDE_CODE_DISABLE_BACKGROUND_TASKS`、`CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` 等），请参考 [Claude Settings Reference](./claude-settings.md#environment-variables-via-env)。

---

## 来源

- [Claude Code CLI Reference](https://code.claude.com/docs/en/cli-reference)
- [Claude Code Headless Mode](https://code.claude.com/docs/en/headless)
- [Claude Code Setup](https://code.claude.com/docs/en/setup)
- [Claude Code CHANGELOG](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
- [Claude Code Common Workflows](https://code.claude.com/docs/en/common-workflows)
