# 命令最佳实践

![Last Updated](https://img.shields.io/badge/Last_Updated-Apr%2009%2C%202026%2011%3A31%20PM%20PKT-white?style=flat&labelColor=555) ![Version](https://img.shields.io/badge/Claude_Code-v2.1.97-blue?style=flat&labelColor=555)<br>
[![Implemented](https://img.shields.io/badge/Implemented-2ea44f?style=flat)](../implementation/claude-commands-implementation.md)

Claude Code 命令：frontmatter 字段与官方内置斜杠命令总览。

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
| `description` | string | 建议填写 | 命令的作用。会显示在自动补全中，也会被 Claude 用于自动发现 |
| `argument-hint` | string | 否 | 自动补全时显示的参数提示（例如 `[issue-number]`、`[filename]`） |
| `disable-model-invocation` | boolean | 否 | 设为 `true` 可阻止 Claude 自动调用该命令 |
| `user-invocable` | boolean | 否 | 设为 `false` 可从 `/` 菜单隐藏，该命令仅作为后台知识存在 |
| `paths` | string/list | 否 | 限制技能激活时机的 Glob 模式。支持逗号分隔字符串或 YAML 列表。设置后，Claude 仅在处理匹配文件时自动加载该技能 |
| `allowed-tools` | string | 否 | 该命令激活时无需权限提示即可使用的工具 |
| `model` | string | 否 | 运行该命令时使用的模型（如 `haiku`、`sonnet`、`opus`） |
| `effort` | string | 否 | 调用时覆盖模型的 effort 等级（`low`、`medium`、`high`、`max`） |
| `context` | string | 否 | 设为 `fork` 可在隔离的子代理上下文中运行该命令 |
| `agent` | string | 否 | 当设置 `context: fork` 时使用的子代理类型（默认：`general-purpose`） |
| `shell` | string | 否 | `` !`command` `` 代码块使用的 shell，可为 `bash`（默认）或 `powershell`。需要 `CLAUDE_CODE_USE_POWERSHELL_TOOL=1` |
| `hooks` | object | 否 | 作用域限定在该命令内的生命周期钩子 |

---

## ![Official](../!/tags/official.svg) **(68)**

| # | 命令 | 标签 | 说明 |
|---|---------|-----|-------------|
| 1 | `/login` | ![Auth](https://img.shields.io/badge/Auth-2980B9?style=flat) | 登录你的 Anthropic 账号 |
| 2 | `/logout` | ![Auth](https://img.shields.io/badge/Auth-2980B9?style=flat) | 退出 Anthropic 账号 |
| 3 | `/setup-bedrock` | ![Auth](https://img.shields.io/badge/Auth-2980B9?style=flat) | 通过交互式向导配置 Amazon Bedrock 认证、区域和模型固定设置。仅当设置 `CLAUDE_CODE_USE_BEDROCK=1` 时可见。首次使用 Bedrock 的用户也可以在登录界面进入此向导 |
| 4 | `/upgrade` | ![Auth](https://img.shields.io/badge/Auth-2980B9?style=flat) | 打开升级页面，切换到更高等级的套餐 |
| 5 | `/color [color\|default]` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 为当前会话设置提示栏颜色。可选颜色：`red`、`blue`、`green`、`yellow`、`purple`、`orange`、`pink`、`cyan`。使用 `default` 重置 |
| 6 | `/config` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 打开设置界面，调整主题、模型、输出风格等偏好。别名：`/settings` |
| 7 | `/keybindings` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 打开或创建你的按键绑定配置文件 |
| 8 | `/permissions` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 管理工具权限的 allow、ask 和 deny 规则。会打开交互式对话框，你可以按作用域查看规则、增删规则、管理工作目录，并审查最近的 auto mode 拒绝记录。别名：`/allowed-tools` |
| 9 | `/privacy-settings` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 查看并更新隐私设置。仅对 Pro 和 Max 订阅者开放 |
| 10 | `/sandbox` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 切换 sandbox 模式，仅在受支持平台可用 |
| 11 | `/statusline` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 配置 Claude Code 的状态栏。可以描述你的目标，也可以不带参数直接运行，让它根据 shell 提示自动配置 |
| 12 | `/stickers` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 订购 Claude Code 贴纸 |
| 13 | `/terminal-setup` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 配置 Shift+Enter 和其他快捷键的终端按键绑定。仅在确实需要该设置的终端中可见，例如 VS Code、Alacritty 或 Warp |
| 14 | `/theme` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 切换颜色主题，包含浅色/深色变体、色盲友好（daltonized）主题，以及复用终端调色板的 ANSI 主题 |
| 15 | `/voice` | ![Config](https://img.shields.io/badge/Config-F39C12?style=flat) | 开关按住说话的语音输入。需要 Claude.ai 账号 |
| 16 | `/context` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 用彩色网格可视化当前上下文使用情况，并给出针对上下文密集型工具、记忆膨胀和容量预警的优化建议 |
| 17 | `/cost` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 显示 token 使用统计。订阅相关的详细说明请查看成本跟踪指南 |
| 18 | `/extra-usage` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 配置 extra usage，以便在触达速率限制时继续工作 |
| 19 | `/insights` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 生成分析报告，总结你的 Claude Code 会话，包括项目区域、交互模式和摩擦点 |
| 20 | `/stats` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 可视化每日使用、会话历史、连续使用天数和模型偏好 |
| 21 | `/status` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 打开设置界面的 Status 标签，显示版本、模型、账号和连接状态。即使 Claude 正在响应，也无需等待当前回复结束 |
| 22 | `/usage` | ![Context](https://img.shields.io/badge/Context-8E44AD?style=flat) | 显示套餐使用上限和速率限制状态 |
| 23 | `/doctor` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 诊断并验证你的 Claude Code 安装与设置 |
| 24 | `/feedback [report]` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 提交关于 Claude Code 的反馈。别名：`/bug` |
| 25 | `/help` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 显示帮助和可用命令 |
| 26 | `/powerup` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 通过带动画演示的快速交互课程探索 Claude Code 功能 |
| 27 | `/release-notes` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 在交互式版本选择器中查看更新日志。可以选择具体版本查看发布说明，也可以一次性显示全部版本 |
| 28 | `/tasks` | ![Debug](https://img.shields.io/badge/Debug-E74C3C?style=flat) | 列出并管理后台任务。别名：`/bashes` |
| 29 | `/copy [N]` | ![Export](https://img.shields.io/badge/Export-7F8C8D?style=flat) | 将最近一次助手回复复制到剪贴板。传入数字 `N` 时，可复制倒数第 `N` 条回复，例如 `/copy 2` 会复制倒数第二条。当回复包含代码块时，会打开交互式选择器，可选择单独的代码块或整条回复。按 `w` 可将选中内容写入文件而不是复制到剪贴板，这在通过 SSH 使用时尤其有用 |
| 30 | `/export [filename]` | ![Export](https://img.shields.io/badge/Export-7F8C8D?style=flat) | 将当前对话导出为纯文本。指定文件名时直接写入文件；不指定时，会打开对话框让你复制到剪贴板或保存到文件 |
| 31 | `/agents` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 管理代理配置 |
| 32 | `/chrome` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 在 Claude 的 Chrome 设置中完成配置 |
| 33 | `/hooks` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 查看与工具事件相关的钩子配置 |
| 34 | `/ide` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 管理 IDE 集成并查看状态 |
| 35 | `/mcp` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 管理 MCP 服务器连接和 OAuth 认证 |
| 36 | `/plugin` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 管理 Claude Code 插件 |
| 37 | `/reload-plugins` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 重新加载所有激活中的插件，以便在不重启的情况下应用待处理改动。会报告每类组件的重载数量，并标记加载错误 |
| 38 | `/skills` | ![Extensions](https://img.shields.io/badge/Extensions-16A085?style=flat) | 列出可用技能 |
| 39 | `/memory` | ![Memory](https://img.shields.io/badge/Memory-3498DB?style=flat) | 编辑 `CLAUDE.md` 记忆文件，启用或禁用自动记忆，并查看自动记忆条目 |
| 40 | `/effort [low\|medium\|high\|max\|auto]` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 设置模型的 effort 等级。`low`、`medium` 和 `high` 会跨会话持久化；`max` 仅作用于当前会话，且需要 Opus 4.6；`auto` 则恢复为模型默认。无参数时会显示当前等级。设置会立即生效，无需等待当前回复结束 |
| 41 | `/fast [on\|off]` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 打开或关闭 fast mode |
| 42 | `/model [model]` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 选择或切换 AI 模型。对于支持的模型，可使用左右方向键调整 effort 等级。切换会立即生效，无需等待当前回复结束 |
| 43 | `/passes` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 向朋友赠送一周免费 Claude Code。仅在你的账号具备资格时可见 |
| 44 | `/plan [description]` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 直接从提示框进入 plan 模式。可传入可选描述，以便进入 plan 模式后立刻从该任务开始，例如 `/plan fix the auth bug` |
| 45 | `/ultraplan <prompt>` | ![Model](https://img.shields.io/badge/Model-E67E22?style=flat) | 在 ultraplan 会话中起草计划，在浏览器中审阅，然后远程执行或发回终端 |
| 46 | `/add-dir <path>` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 在当前会话中添加额外工作目录以便访问文件。多数 `.claude/` 配置不会从新增目录中自动发现 |
| 47 | `/diff` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 打开交互式 diff 查看器，显示未提交变更和按回合划分的 diff。可用左右方向键在当前 git diff 与各 Claude 回合之间切换，上下方向键浏览文件 |
| 48 | `/init` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 使用 `CLAUDE.md` 指南初始化项目。设置 `CLAUDE_CODE_NEW_INIT=1` 后，会进入交互流程，并一并引导你配置技能、钩子和个人记忆文件 |
| 49 | `/review` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 已弃用。请改装 `code-review` 插件：`claude plugin install code-review@claude-plugins-official` |
| 50 | `/security-review` | ![Project](https://img.shields.io/badge/Project-27AE60?style=flat) | 分析当前分支上的待提交改动，查找安全漏洞。会审查 git diff，并识别注入、认证问题和数据暴露等风险 |
| 51 | `/autofix-pr [prompt]` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 在 Web 上启动一个 Claude Code 会话，持续观察当前分支对应的 PR，并在 CI 失败或评审留言时自动推送修复。默认通过 `gh pr view` 检测当前分支打开的 PR；如果想监控其他 PR，先切换到对应分支。需要 `gh` CLI，并且需要可访问 Claude Code on the web |
| 52 | `/desktop` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 在 Claude Code Desktop 应用中继续当前会话。仅支持 macOS 和 Windows。别名：`/app` |
| 53 | `/install-github-app` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 为某个仓库安装 Claude GitHub Actions 应用，会引导你选择仓库并配置集成 |
| 54 | `/install-slack-app` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 安装 Claude Slack 应用，会打开浏览器完成 OAuth 流程 |
| 55 | `/mobile` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 显示二维码以下载 Claude 移动应用。别名：`/ios`、`/android` |
| 56 | `/remote-control` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 让当前会话可被 claude.ai 远程控制。别名：`/rc` |
| 57 | `/remote-env` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 配置通过 `--remote` 启动的 Web 会话所使用的默认远程环境 |
| 58 | `/schedule [description]` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 创建、更新、列出或运行 Cloud 定时任务。Claude 会以对话方式带你完成设置 |
| 59 | `/teleport` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 将一个 Claude Code on the web 会话拉回当前终端：会先打开选择器，再拉取对应分支和会话。也可使用 `/tp`。需要 claude.ai 订阅 |
| 60 | `/web-setup` | ![Remote](https://img.shields.io/badge/Remote-5D6D7E?style=flat) | 使用本地 `gh` CLI 凭据，把 GitHub 账号连接到 Claude Code on the web。若 GitHub 尚未连接，`/schedule` 会自动提示你完成此步骤 |
| 61 | `/branch [name]` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 在当前对话的此时此刻分出一个会话分支。别名：`/fork` |
| 62 | `/btw <question>` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 提一个快捷的旁支问题，而不把它加入主对话上下文 |
| 63 | `/clear` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 清空对话历史并释放上下文。别名：`/reset`、`/new` |
| 64 | `/compact [instructions]` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 压缩当前对话，并可附带聚焦说明 |
| 65 | `/exit` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 退出 CLI。别名：`/quit` |
| 66 | `/rename [name]` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 重命名当前会话，并在提示栏显示该名称。不传名称时，会根据对话历史自动生成 |
| 67 | `/resume [session]` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 按 ID 或名称恢复会话，或打开会话选择器。别名：`/continue` |
| 68 | `/rewind` | ![Session](https://img.shields.io/badge/Session-4A90D9?style=flat) | 将对话和/或代码回退到之前的某个时间点，或从选定消息生成摘要。参见 checkpointing。别名：`/checkpoint` |

`/debug` 之类的内置技能也可能出现在斜杠命令菜单中，但它们并不属于内置命令本身。

---

## 来源

- [Claude Code Slash Commands](https://code.claude.com/docs/en/slash-commands)
- [Claude Code Interactive Mode](https://code.claude.com/docs/en/interactive-mode)
- [Claude Code CHANGELOG](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
