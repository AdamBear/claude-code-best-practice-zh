# 命令报告变更历史

## 状态图例

| 状态 | 含义 |
|--------|---------|
| `COMPLETE (reason)` | 已执行并成功解决 |
| `INVALID (reason)` | 结论不正确、不适用，或当前状态属预期 |
| `ON HOLD (reason)` | 已暂缓处理，等待外部依赖或用户决定 |

---

## [2026-03-13 04:23 PM PKT] Claude Code v2.1.74

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 向 frontmatter 表加入 `name`，作为技能的显示名称 | INVALID（仅技能字段，不适用于命令 frontmatter） |
| 2 | HIGH | 新字段 | 向 frontmatter 表加入 `disable-model-invocation`，用于阻止自动加载 | INVALID（仅技能字段，不适用于命令 frontmatter） |
| 3 | HIGH | 新字段 | 向 frontmatter 表加入 `user-invocable`，用于从 `/` 菜单隐藏 | INVALID（仅技能字段，不适用于命令 frontmatter） |
| 4 | HIGH | 新字段 | 向 frontmatter 表加入 `context`，用于以 fork 方式在子代理上下文中运行 | INVALID（仅技能字段，不适用于命令 frontmatter） |
| 5 | HIGH | 新字段 | 向 frontmatter 表加入 `agent`，作为 `context: fork` 的子代理类型 | INVALID（仅技能字段，不适用于命令 frontmatter） |
| 6 | HIGH | 新字段 | 向 frontmatter 表加入 `hooks`，作为绑定到技能生命周期的钩子 | INVALID（仅技能字段，不适用于命令 frontmatter） |
| 7 | HIGH | 新命令 | 加入 `/btw <question>`，用于在不加入主对话的情况下快速问一个旁支问题 | COMPLETE（已作为 Session 标签下的第 #53 项加入） |
| 8 | HIGH | 新命令 | 加入 `/hooks`，用于管理工具事件的 hook 配置 | COMPLETE（已作为 Extensions 标签下的第 #30 项加入） |
| 9 | HIGH | 新命令 | 加入 `/insights`，用于生成会话分析报告 | COMPLETE（已作为 Context 标签下的第 #17 项加入） |
| 10 | HIGH | 新命令 | 加入 `/plugin`，用于管理 Claude Code 插件 | COMPLETE（已作为 Extensions 标签下的第 #33 项加入） |
| 11 | HIGH | 新命令 | 加入 `/skills`，用于列出可用技能 | COMPLETE（已作为 Extensions 标签下的第 #35 项加入） |
| 12 | HIGH | 新命令 | 加入 `/upgrade`，用于打开升级页面切换套餐档位 | COMPLETE（已作为 Auth 标签下的第 #3 项加入） |
| 13 | HIGH | 移除命令 | 移除 `/output-style`，该命令在 v2.1.73 已弃用，改用 `/config` | COMPLETE（已从 Config 标签移除） |
| 14 | HIGH | 移除命令 | 移除 `/bug` 这一行，它现在作为 `/feedback` 的别名出现 | COMPLETE（已移除独立行，并在 `/feedback` 描述中加入 “Alias: /bug”） |
| 15 | HIGH | 描述变更 | 更新 `/passes`，其用途已从 review passes 改为 referral sharing | COMPLETE（已更新描述，并保留在 Model 标签） |
| 16 | HIGH | 描述变更 | 更新 `/review`，该命令已弃用，由 `code-review` marketplace plugin 取代 | COMPLETE（已更新 Project 标签中的描述） |
| 17 | MED | 描述变更 | 更新 `/stickers`，从 UI sticker packs 改为订购实体贴纸 | COMPLETE（已更新 Config 标签中的描述） |

---

## [2026-03-15 12:50 PM PKT] Claude Code v2.1.76

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新命令 | 在 Config 标签中加入 `/color [color\|default]`，用于设置当前会话的提示栏颜色 | COMPLETE（已作为 Config 标签第 #4 项加入） |
| 2 | HIGH | 新命令 | 在 Model 标签中加入 `/effort [low\|medium\|high\|max\|auto]`，用于设置模型 effort 等级 | COMPLETE（已作为 Model 标签第 #38 项加入） |
| 3 | MED | 描述变更 | 更新 `/status`，现为 “Open the Settings interface (Status tab)” 而非 “Show a concise session status summary” | COMPLETE（已更新 Context 标签第 #20 项的描述） |
| 4 | MED | 描述变更 | 更新 `/desktop`，现为 “Continue the current session in the Claude Code Desktop app. macOS and Windows only.” | COMPLETE（已更新 Remote 标签第 #49 项的描述） |
| 5 | LOW | 参数变更 | 更新 `/init`，官方文档已移除 `[prompt]` 参数提示 | COMPLETE（已移除 Project 标签第 #45 项的 [prompt] 提示） |

---

## [2026-03-17 12:45 PM PKT] Claude Code v2.1.77

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新别名 | 在 `/fork` 条目中加入 `Alias: /branch`（v2.1.77 将 fork 重命名为 branch） | COMPLETE（已在 Session 标签第 #59 项的 `/fork` 中加入 “Alias: /branch”） |
| 2 | HIGH | 新别名 | 为 8 个命令补充别名：`/clear`（+/reset、/new）、`/config`（+/settings）、`/desktop`（+/app）、`/exit`（+/quit）、`/rewind`（+/checkpoint）、`/resume`（+/continue）、`/remote-control`（+/rc）、`/mobile`（+/ios、/android） | COMPLETE（已在这 8 个命令的描述中加入 alias 标记） |
| 3 | MED | 描述变更 | 更新 `/diff`：“Open an interactive diff viewer showing uncommitted changes and per-turn diffs” | COMPLETE（已更新 Project 标签第 #44 项的描述） |
| 4 | MED | 描述变更 | 更新 `/memory`：“Edit CLAUDE.md memory files, enable or disable auto-memory, and view auto-memory entries” | COMPLETE（已更新 Memory 标签第 #37 项的描述） |
| 5 | MED | 描述变更 | 更新 `/copy`：“Copy the last assistant response to clipboard. Shows interactive picker for code blocks” | COMPLETE（已更新 Export 标签第 #27 项的描述） |
| 6 | MED | 描述变更 | 更新 `/mobile`：“Show QR code to download the Claude mobile app” | COMPLETE（已更新第 #52 项的描述并加入别名） |
| 7 | MED | 描述变更 | 更新 `/remote-control`：“Make this session available for remote control from claude.ai” | COMPLETE（已更新描述并加入别名） |
| 8 | LOW | frontmatter 范围 | 报告中仍未收录 6 个仅适用于技能的字段（这是有意的范围约束） | INVALID（仅技能字段，与 v2.1.74 的判定一致） |

---

## [2026-03-18 11:38 PM PKT] Claude Code v2.1.78

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新命令 | 在 Config 标签中加入 `/voice`，用于切换按住说话的语音输入 | COMPLETE（已作为 Config 标签第 #15 项加入） |
| 2 | HIGH | 倒置别名 | 将 `/fork` → `/branch` 调整为主命令，并把 `/fork` 改为别名 | COMPLETE（已切换为 Session 标签第 #56 项 `/branch`，并按字母顺序重排） |
| 3 | MED | 新别名 | 为 `/permissions` 加入 `/allowed-tools` 别名 | COMPLETE（已加入 Config 标签第 #7 项） |
| 4 | MED | 新参数 | 为 `/copy` 加入 `[N]` 参数语法 | COMPLETE（已更新为 Export 标签第 #28 项 `/copy [N]`） |
| 5 | LOW | frontmatter 范围 | 报告中未包含 6 个仅技能字段（有意保持范围） | INVALID（仅技能字段，与 v2.1.74、v2.1.77 的判定一致） |

---

## [2026-03-19 11:54 AM PKT] Claude Code v2.1.79

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | LOW | frontmatter 范围 | 报告中未包含 6 个仅技能字段（有意保持范围） | INVALID（仅技能字段，与 v2.1.74、v2.1.77、v2.1.78 的判定一致） |

---

## [2026-03-20 08:33 AM PKT] Claude Code v2.1.80

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 新字段 | 在 frontmatter 表中加入 `effort`，用于在调用命令时覆盖模型 effort 等级（v2.1.80） | COMPLETE（先作为第 5 个字段加入，之后在完整字段集加入时调整到第 8 位） |
| 2 | HIGH | QA 修正 | 加入 6 个缺失字段（`name`、`disable-model-invocation`、`user-invocable`、`context`、`agent`、`hooks`）；官方文档说明命令支持 “the same frontmatter” as skills，之前在 v2.1.74-v2.1.79 的 INVALID 判定是错误的 | COMPLETE（已补齐全部 6 个字段，计数从 5 更新为 11，顺序与官方文档一致） |
| 3 | HIGH | 跨报告修复 | 在技能报告 `claude-skills.md` 中也补上 `effort` 字段，该报告此前也漏了 | COMPLETE（已在技能报告中作为第 8 个字段加入，计数从 10 更新为 11） |

---

## [2026-03-21 09:08 PM PKT] Claude Code v2.1.81

未发现高优先级项。报告已与官方文档完全同步（11 个 frontmatter 字段，63 个内置命令）。

---

## [2026-03-23 09:48 PM PKT] Claude Code v2.1.81

未发现高优先级项。报告已与官方文档完全同步（11 个 frontmatter 字段，63 个内置命令）。

---

## [2026-03-25 08:07 PM PKT] Claude Code v2.1.83

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新命令 | 在 Remote 标签中加入 `/schedule [description]`，用于创建、更新、列出或运行云端计划任务 | COMPLETE（已作为 Remote 标签第 #56 项加入，计数从 63 更新为 64） |

---

## [2026-03-26 01:01 PM PKT] Claude Code v2.1.84

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 在 frontmatter 表中加入 `shell`，用于指定 `!command` 代码块使用的 shell（`bash` 或 `powershell`） | COMPLETE（已作为第 12 个字段加入，计数从 11 更新为 12） |
| 2 | LOW | 参数变更 | 为 `/fast` 命令补充 `[on\|off]` 参数提示 | COMPLETE（已更新为 Model 标签第 #40 项 `/fast [on\|off]`） |

---

## [2026-03-27 06:25 PM PKT] Claude Code v2.1.85

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 在 frontmatter 表中加入 `paths`，用于限制技能何时激活的 glob 模式 | COMPLETE（已作为 `user-invocable` 之后的第 6 个字段加入，计数从 12 更新为 13） |

---

## [2026-03-28 06:05 PM PKT] Claude Code v2.1.86

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 参数变更 | 更新 `/add-dir`，按官方文档补充必填参数提示 `<path>` | COMPLETE（已更新 Project 标签第 #44 项） |
| 2 | MED | 参数变更 | 更新 `/branch`，按官方文档补充可选参数提示 `[name]` | COMPLETE（已更新 Session 标签第 #57 项） |
| 3 | MED | 参数变更 | 更新 `/model`，按官方文档补充可选参数提示 `[model]` | COMPLETE（已更新 Model 标签第 #41 项） |
| 4 | MED | 参数变更 | 更新 `/plan`，按官方文档补充可选参数提示 `[description]` | COMPLETE（已更新 Model 标签第 #43 项） |
| 5 | MED | 参数变更 | 更新 `/pr-comments`，按官方文档补充可选参数提示 `[PR]` | COMPLETE（已更新 Project 标签第 #47 项） |
| 6 | MED | 参数变更 | 更新 `/passes`，移除 `[number]` 参数提示（官方文档中没有） | COMPLETE（已更新 Model 标签第 #42 项） |
| 7 | MED | 参数变更 | 更新 `/rename`，从必填 `<name>` 改为可选 `[name]`，以匹配官方文档 | COMPLETE（已更新 Session 标签第 #62 项） |
| 8 | LOW | 参数变更 | 更新 `/compact`，将参数标签从 `[prompt]` 改为 `[instructions]`，以匹配官方文档 | COMPLETE（已更新 Session 标签第 #60 项） |
| 9 | LOW | 参数变更 | 更新 `/feedback`，将参数标签从 `[description]` 改为 `[report]`，以匹配官方文档 | COMPLETE（已更新 Debug 标签第 #24 项） |

---

## [2026-03-31 06:55 PM PKT] Claude Code v2.1.88

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 描述同步 | 将全部 43 条命令描述与官方文档重新对齐，覆盖行为澄清（`/vim` 切换、`/sandbox` 切换、`/hooks` 查看）、细节扩展（`/effort` 持久化、`/copy` 的 SSH 写入、`/model` 的 effort 箭头），以及 Auth、Config、Context、Debug、Export、Extensions、Model、Project、Remote、Session 各标签下的措辞统一 | COMPLETE（64 条描述现已全部匹配 code.claude.com/docs/en/commands 官方文档） |

---

## [2026-04-01 12:26 PM PKT] Claude Code v2.1.89

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | LOW | 描述变更 | 更新 `/init`，官方文档现在使用 `CLAUDE_CODE_NEW_INIT=1`，而不再是 `=true` | COMPLETE（已将环境变量取值从 `=true` 改为 `=1`） |

---

## [2026-04-02 09:14 PM PKT] Claude Code v2.1.90

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 描述变更 | 更新 `/permissions`，官方文档现补充了交互对话框、作用域规则、目录管理以及 auto 模式拒绝回顾的说明 | COMPLETE（描述已更新以匹配官方文档） |
| 2 | MED | 新别名 | 按官方文档为 `/tasks` 命令加入 `/bashes` 别名 | COMPLETE（已在 Debug 标签第 #27 项 `/tasks` 中加入 “Alias: /bashes”） |

---

## [2026-04-03 08:34 PM PKT] Claude Code v2.1.91

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新命令 | 在 Config 标签中加入 `/powerup`，用于通过带动画演示的快速互动课程探索 Claude Code 功能 | COMPLETE（先作为 Debug 标签第 #26 项加入，已在 v2.1.92 轮次中归位） |

---

## [2026-04-04 10:40 PM PKT] Claude Code v2.1.92

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新命令 | 在 Debug 标签中加入 `/powerup`，用于通过带动画演示的快速互动课程探索 Claude Code 功能 | COMPLETE（已作为 Debug 标签第 #26 项加入，延续自 v2.1.91） |
| 2 | HIGH | 新命令 | 在 Auth 标签中加入 `/setup-bedrock`，通过交互式向导配置 Amazon Bedrock 认证、区域与模型 pin | COMPLETE（已作为 Auth 标签第 #3 项加入） |
| 3 | HIGH | 新命令 | 在 Model 标签中加入 `/ultraplan <prompt>`，可在 ultraplan 会话中起草计划，在浏览器中审阅后远程执行或发送回本地 | COMPLETE（已作为 Model 标签第 #45 项加入） |
| 4 | HIGH | 移除命令 | 从 Config 标签移除 `/vim`；该命令在 v2.1.92 已移除（max-version: 2.1.91），改用 `/config` 中的 Editor mode | COMPLETE（已从 Config 标签移除） |
| 5 | HIGH | 移除命令 | 从 Project 标签移除 `/pr-comments [PR]`；该命令在 v2.1.91 已移除（max-version: 2.1.90），改为直接向 Claude 提问 | COMPLETE（已从 Project 标签移除） |
| 6 | MED | 描述变更 | 更新 `/release-notes`，现为 “View the changelog in an interactive version picker. Select a specific version to see its release notes, or choose to show all versions.” | COMPLETE（已更新 Debug 标签第 #27 项的描述） |

---

## [2026-04-08 09:35 PM PKT] Claude Code v2.1.96

未发现高优先级项。报告已与官方文档完全同步（13 个 frontmatter 字段，65 个内置命令）。

---

## [2026-04-09 11:31 PM PKT] Claude Code v2.1.97

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新命令 | 在 Remote 标签中加入 `/autofix-pr [prompt]`，启动一个 web 会话持续观察当前分支的 PR，并在 CI 失败或评审留言时自动推送修复 | COMPLETE（已作为 Remote 标签第 #51 项加入，计数从 65 更新为 68） |
| 2 | HIGH | 新命令 | 在 Remote 标签中加入 `/teleport`，把 Claude Code on the web 会话拉回当前终端；别名：`/tp` | COMPLETE（已作为 Remote 标签第 #59 项加入） |
| 3 | HIGH | 新命令 | 在 Remote 标签中加入 `/web-setup`，通过本地 `gh` CLI 凭据，将 GitHub 账户连接到 Claude Code on the web | COMPLETE（已作为 Remote 标签第 #60 项加入） |
| 4 | MED | 描述变更 | 更新 `/add-dir`，官方文档现补充了从附加目录不会自动发现 `.claude/` 配置的提示 | COMPLETE（已更新 Project 标签第 #46 项的描述） |
