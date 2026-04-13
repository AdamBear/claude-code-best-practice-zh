# 设置最佳实践

![Last Updated](https://img.shields.io/badge/Last_Updated-Apr%2009%2C%202026%2011%3A39%20PM%20PKT-white?style=flat&labelColor=555) ![Version](https://img.shields.io/badge/Claude_Code-v2.1.97-blue?style=flat&labelColor=555)<br>
[![Implemented](https://img.shields.io/badge/Implemented-2ea44f?style=flat)](../.claude/settings.json)

这是一份关于 Claude Code `settings.json` 的中文参考。内容覆盖设置层级、权限、MCP、Sandbox、插件、模型、显示与环境变量等核心配置。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

## 目录

1. [设置层级](#设置层级)
2. [核心配置](#核心配置)
3. [权限](#权限)
4. [钩子](#钩子)
5. [MCP 服务器](#mcp-服务器)
6. [Sandbox](#sandbox)
7. [插件](#插件)
8. [模型配置](#模型配置)
9. [显示与 UX](#显示与-ux)
10. [AWS 与云凭据](#aws-与云凭据)
11. [环境变量](#环境变量-via-env)
12. [常用命令](#常用命令)

---

## 设置层级

设置优先级从高到低如下：

| 优先级 | 位置 | 作用域 | 是否共享 | 用途 |
|---|---|---|---|---|
| 1 | Managed settings | Organization | 是 | 不可覆盖的组织策略 |
| 2 | 命令行参数 | Session | 否 | 单次会话临时覆盖 |
| 3 | `.claude/settings.local.json` | Project | 否 | 个人项目级设置 |
| 4 | `.claude/settings.json` | Project | 是 | 团队共享设置 |
| 5 | `~/.claude/settings.json` | User | 否 | 全局个人默认值 |

Managed settings 可通过远程下发、MDM、Windows 注册表、`managed-settings.json` / `managed-mcp.json` 以及 `managed-settings.d/` 目录投递。其核心规则：

- `deny` 的优先级最高，不能被低优先级规则覆盖。
- 本地设置即使显式声明，也可能被 managed settings 锁定或覆盖。
- 数组型配置会跨层拼接并去重，而不是直接替换。
- Windows 旧路径 `C:\ProgramData\ClaudeCode\managed-settings.json` 已废弃，请使用 `C:\Program Files\ClaudeCode\managed-settings.json`。

---

## 核心配置

### 通用设置

| 键 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `$schema` | string | - | JSON Schema URL，用于 IDE 校验和自动补全 |
| `model` | string | `"default"` | 覆盖默认模型，支持 `sonnet`、`opus`、`haiku` 或完整模型 ID |
| `agent` | string | - | 设置主对话默认代理，也可用 `--agent` |
| `language` | string | `"english"` | Claude 的回复语言，也会影响语音输入语言 |
| `cleanupPeriodDays` | number | `30` | 清理非活跃会话与孤立 worktree 的时限，最小值为 1 |
| `autoUpdatesChannel` | string | `"latest"` | 更新渠道：`stable` 或 `latest` |
| `alwaysThinkingEnabled` | boolean | `false` | 默认启用 extended thinking |
| `skipWebFetchPreflight` | boolean | `false` | 跳过 WebFetch 的预检查 |
| `availableModels` | array | - | 限制用户可选模型 |
| `fastModePerSessionOptIn` | boolean | `false` | 每个会话都需显式选择是否启用 fast mode |
| `defaultShell` | string | `"bash"` | 输入框 `!` 命令默认 shell，可设为 `powershell` |
| `includeGitInstructions` | boolean | `true` | 是否把 git 提交和 PR 说明注入系统提示词 |
| `voiceEnabled` | boolean | - | 是否启用按住说话语音输入 |
| `showClearContextOnPlanAccept` | boolean | `false` | 在 plan 接受界面展示“清空上下文”选项 |
| `disableDeepLinkRegistration` | string | - | 设为 `"disable"` 后，阻止注册 `claude-cli://` 协议 |
| `showThinkingSummaries` | boolean | `false` | 在交互模式显示 thinking 摘要 |
| `disableSkillShellExecution` | boolean | `false` | 禁用技能 / 自定义命令里的 `` !`...` `` 执行 |
| `forceRemoteSettingsRefresh` | boolean | `false` | 仅 managed 可用，要求启动前先刷新远程策略 |
| `feedbackSurveyRate` | number | - | 会话质量调查出现概率 |

**示例：**
```json
{
  "model": "opus",
  "agent": "code-reviewer",
  "language": "japanese",
  "cleanupPeriodDays": 60,
  "autoUpdatesChannel": "stable",
  "alwaysThinkingEnabled": true
}
```

### Plans 与记忆目录

| 键 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `plansDirectory` | string | `~/.claude/plans` | `/plan` 产物保存目录 |
| `autoMemoryDirectory` | string | - | 自动记忆保存目录，项目设置里不可用 |

### Worktree 设置

| 键 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `worktree.symlinkDirectories` | array | `[]` | 在 worktree 中软链接的大目录 |
| `worktree.sparsePaths` | array | `[]` | 通过 sparse-checkout 检出的目录 |

### Attribution 设置

| 键 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `attribution.commit` | string | Co-authored-by | 提交 attribution |
| `attribution.pr` | string | Generated message | PR attribution |
| `includeCoAuthoredBy` | boolean | `true` | 已弃用，改用 `attribution` |

### 认证与公告

| 键 | 类型 | 说明 |
|---|---|---|
| `apiKeyHelper` | string | 输出认证 token 的脚本 |
| `forceLoginMethod` | string | 限制为 `"claudeai"` 或 `"console"` 登录 |
| `forceLoginOrgUUID` | string\|array | 限制可登录的组织 UUID |
| `companyAnnouncements` | array | 启动时显示的公司公告数组 |

---

## 权限

权限结构：

```json
{
  "permissions": {
    "allow": [],
    "ask": [],
    "deny": [],
    "additionalDirectories": [],
    "defaultMode": "acceptEdits",
    "disableBypassPermissionsMode": "disable"
  }
}
```

### 关键权限项

| 键 | 类型 | 说明 |
|---|---|---|
| `permissions.allow` | array | 允许直接使用的工具规则 |
| `permissions.ask` | array | 需要用户确认的规则 |
| `permissions.deny` | array | 拒绝规则，优先级最高 |
| `permissions.additionalDirectories` | array | 可访问的额外目录 |
| `permissions.defaultMode` | string | 默认权限模式 |
| `permissions.disableBypassPermissionsMode` | string | 禁止进入 bypass mode |
| `permissions.skipDangerousModePermissionPrompt` | boolean | 跳过进入危险模式前的确认 |
| `allowManagedPermissionRulesOnly` | boolean | 仅使用 managed 权限规则 |
| `allow_remote_sessions` | boolean | 是否允许 Remote Control / Web 会话 |
| `autoMode` | object | 自定义 auto mode 的环境、allow 与 soft_deny |
| `disableAutoMode` | string | 禁用 auto mode |
| `useAutoModeDuringPlan` | boolean | plan mode 是否沿用 auto mode 语义 |

### 权限模式

| 模式 | 行为 |
|---|---|
| `"default"` | 标准权限提示 |
| `"acceptEdits"` | 自动接受编辑 |
| `"askEdits"` | 每次操作都询问 |
| `"dontAsk"` | 未预先批准的工具一律拒绝 |
| `"viewOnly"` | 只读模式 |
| `"bypassPermissions"` | 跳过所有权限检查 |
| `"auto"` | 用后台分类器替代人工提示 |
| `"plan"` | 只读探索模式 |

### 工具权限语法

| 工具 | 语法 | 示例 |
|---|---|---|
| `Bash` | `Bash(command pattern)` | `Bash(npm run *)` |
| `Read` | `Read(path pattern)` | `Read(.env)` |
| `Edit` | `Edit(path pattern)` | `Edit(src/**)` |
| `Write` | `Write(path pattern)` | `Write(*.md)` |
| `NotebookEdit` | `NotebookEdit(pattern)` | `NotebookEdit(*)` |
| `WebFetch` | `WebFetch(domain:pattern)` | `WebFetch(domain:example.com)` |
| `WebSearch` | `WebSearch` | 全局 Web 搜索 |
| `Task` | `Task(agent-name)` | `Task(Explore)` |
| `Agent` | `Agent(name)` | `Agent(researcher)` |
| `Skill` | `Skill(skill-name)` | `Skill(weather-fetcher)` |
| `MCP` | `mcp__server__tool` / `MCP(server:tool)` | `mcp__memory__*` |

补充说明：

- 规则判断顺序是 `deny -> ask -> allow`，第一个命中的规则生效。
- `Read`、`Edit`、`Write` 支持 gitignore 风格模式。
- `//` 表示绝对路径，`~/` 表示主目录相对路径，`/` 表示项目根相对路径，`./` 或无前缀表示当前目录相对路径。
- `Bash(*)` 等价于允许全部 Bash 命令。

---

## 钩子

钩子配置（事件、属性、匹配器、退出码、环境变量与 HTTP hooks）维护在独立仓库中：

> **[claude-code-hooks](https://github.com/shanraisshan/claude-code-hooks)** - 完整钩子参考，覆盖声音通知、25 个 hook 事件、HTTP hooks、matcher、退出码和环境变量。

与钩子相关的设置键包括：

- `hooks`
- `disableAllHooks`
- `allowManagedHooksOnly`
- `allowedHttpHookUrls`
- `httpHookAllowedEnvVars`

官方文档见 [Claude Code Hooks Documentation](https://code.claude.com/docs/en/hooks)。

---

## MCP 服务器

### MCP 设置

| 键 | 类型 | 作用域 | 说明 |
|---|---|---|---|
| `enableAllProjectMcpServers` | boolean | Any | 自动批准 `.mcp.json` 中全部服务器 |
| `enabledMcpjsonServers` | array | Any | 自动批准白名单 |
| `disabledMcpjsonServers` | array | Any | 拒绝黑名单 |
| `allowedMcpServers` | array | Managed only | 允许的服务器匹配规则 |
| `deniedMcpServers` | array | Managed only | 拒绝的服务器匹配规则 |
| `allowManagedMcpServersOnly` | boolean | Managed only | 仅允许 managed 白名单中的服务器 |
| `channelsEnabled` | boolean | Managed only | 启用 channels |
| `allowedChannelPlugins` | array | Managed only | 允许向 channels 推送消息的插件白名单 |

**示例：**
```json
{
  "enableAllProjectMcpServers": true,
  "enabledMcpjsonServers": ["memory", "github", "filesystem"],
  "disabledMcpjsonServers": ["experimental-server"]
}
```

---

## Sandbox

### Sandbox 设置

| 键 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `sandbox.enabled` | boolean | `false` | 启用 bash sandbox |
| `sandbox.failIfUnavailable` | boolean | `false` | sandbox 不可用时直接失败 |
| `sandbox.autoAllowBashIfSandboxed` | boolean | `true` | 命令已在 sandbox 中时自动批准 bash |
| `sandbox.excludedCommands` | array | `[]` | 在 sandbox 外运行的命令 |
| `sandbox.allowUnsandboxedCommands` | boolean | `true` | 是否允许完全关闭 sandbox |
| `sandbox.ignoreViolations` | object | `{}` | 抑制 sandbox 违规警告 |
| `sandbox.enableWeakerNestedSandbox` | boolean | `false` | Docker 中启用较弱 sandbox |
| `sandbox.network.allowUnixSockets` | array | `[]` | 允许访问的 Unix socket |
| `sandbox.network.allowAllUnixSockets` | boolean | `false` | 允许全部 Unix socket |
| `sandbox.network.allowLocalBinding` | boolean | `false` | 允许绑定 localhost |
| `sandbox.network.allowedDomains` | array | `[]` | 网络白名单 |
| `sandbox.network.deniedDomains` | array | `[]` | 网络黑名单 |
| `sandbox.network.httpProxyPort` | number | - | HTTP 代理端口 |
| `sandbox.network.socksProxyPort` | number | - | SOCKS5 代理端口 |
| `sandbox.network.allowManagedDomainsOnly` | boolean | `false` | 仅允许 managed 白名单域名 |
| `sandbox.network.allowMachLookup` | array | `[]` | macOS 的额外 Mach / XPC 服务白名单 |
| `sandbox.filesystem.allowWrite` | array | `[]` | 允许写入的额外路径 |
| `sandbox.filesystem.denyWrite` | array | `[]` | 禁止写入路径 |
| `sandbox.filesystem.denyRead` | array | `[]` | 禁止读取路径 |
| `sandbox.filesystem.allowRead` | array | `[]` | 在 denyRead 区域中重新放行读取 |
| `sandbox.filesystem.allowManagedReadPathsOnly` | boolean | `false` | 只允许 managed 里的 allowRead |
| `sandbox.enableWeakerNetworkIsolation` | boolean | `false` | macOS 上放宽网络隔离 |

---

## 插件

### 插件设置

| 键 | 类型 | 作用域 | 说明 |
|---|---|---|---|
| `enabledPlugins` | object | Any | 启用 / 禁用指定插件 |
| `extraKnownMarketplaces` | object | Project | 添加自定义 marketplace |
| `strictKnownMarketplaces` | array | Managed only | 允许的 marketplace 白名单 |
| `skippedMarketplaces` | array | Any | 用户跳过的 marketplace |
| `skippedPlugins` | array | Any | 用户跳过的插件 |
| `pluginConfigs` | object | Any | 单插件配置 |
| `blockedMarketplaces` | array | Managed only | 禁止的 marketplace |
| `pluginTrustMessage` | string | Managed only | 信任提示文案 |

Marketplace source 类型包括：`github`、`git`、`directory`、`hostPattern`、`settings`、`url`、`npm`、`file`。

---

## 模型配置

### 模型别名

| 别名 | 说明 |
|---|---|
| `"default"` | 适合当前账号类型的推荐模型 |
| `"sonnet"` | 最新 Sonnet |
| `"opus"` | 最新 Opus |
| `"haiku"` | 快速版 Haiku |
| `"sonnet[1m]"` | 1M 上下文 Sonnet |
| `"opus[1m]"` | 1M 上下文 Opus |
| `"opusplan"` | 规划用 Opus，执行用 Sonnet |

### 其他模型设置

| 键 | 类型 | 说明 |
|---|---|---|
| `effortLevel` | string | 持久化 `low` / `medium` / `high` |
| `modelOverrides` | object | 把模型条目映射到 Bedrock / Vertex / Foundry 模型 ID |

### Effort 等级

| 等级 | 说明 |
|---|---|
| High | 深度推理，适合复杂任务 |
| Medium | 平衡推理与速度 |
| Low | 最少推理，响应最快 |

设置方式：

1. 运行 `/effort low`、`/effort medium` 或 `/effort high`
2. 或运行 `/model` 后，在界面中用方向键调整
3. 设置会通过 `effortLevel` 写入 `settings.json`

---

## 显示与 UX

### 显示设置

| 键 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `statusLine` | object | - | 自定义状态栏配置 |
| `outputStyle` | string | `"default"` | 输出风格 |
| `spinnerTipsEnabled` | boolean | `true` | 等待时显示提示 |
| `spinnerVerbs` | object | - | 自定义 spinner 动词 |
| `spinnerTipsOverride` | object | - | 自定义 spinner 提示 |
| `respectGitignore` | boolean | `true` | 文件选择器遵循 `.gitignore` |
| `prefersReducedMotion` | boolean | `false` | 减少动画和动态效果 |
| `fileSuggestion` | object | - | 自定义文件建议命令 |

### `~/.claude.json` 中的全局显示设置

| 键 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `autoConnectIde` | boolean | `false` | 自动连接正在运行的 IDE |
| `autoInstallIdeExtension` | boolean | `true` | 自动安装 IDE 扩展 |
| `editorMode` | string | `"normal"` | 输入框模式：`normal` 或 `vim` |
| `showTurnDuration` | boolean | `true` | 显示单轮耗时 |
| `terminalProgressBarEnabled` | boolean | `true` | 显示终端进度条 |
| `teammateMode` | string | `"in-process"` | agent team 的显示方式 |

### 状态栏字段

状态栏命令通过 stdin 接收 JSON。常见字段包括：

- `model.id`、`model.display_name`
- `cwd`、`workspace.current_dir`
- `workspace.project_dir`
- `workspace.added_dirs`
- `workspace.git_worktree`
- `cost.total_cost_usd`
- `context_window.used_percentage`
- `rate_limits.five_hour.used_percentage`
- `session_id`、`session_name`
- `transcript_path`
- `version`
- `vim.mode`
- `agent.name`
- `worktree.name`、`worktree.path`、`worktree.branch`

---

## AWS 与云凭据

| 键 | 类型 | 说明 |
|---|---|---|
| `awsAuthRefresh` | string | 刷新 AWS 认证的脚本 |
| `awsCredentialExport` | string | 输出 AWS 凭据 JSON 的脚本 |
| `otelHeadersHelper` | string | 生成 OpenTelemetry headers 的脚本 |

---

## 环境变量（via `env`）

可以通过 `settings.json` 中的 `env` 字段为 Claude Code 会话统一注入环境变量：

```json
{
  "env": {
    "ANTHROPIC_API_KEY": "...",
    "NODE_ENV": "development",
    "DEBUG": "true"
  }
}
```

### 常见环境变量分组

认证与模型：

- `ANTHROPIC_API_KEY`
- `ANTHROPIC_AUTH_TOKEN`
- `CLAUDE_CODE_OAUTH_TOKEN`
- `CLAUDE_CODE_OAUTH_REFRESH_TOKEN`
- `CLAUDE_CODE_OAUTH_SCOPES`
- `ANTHROPIC_MODEL`
- `ANTHROPIC_DEFAULT_HAIKU_MODEL`
- `ANTHROPIC_DEFAULT_SONNET_MODEL`
- `ANTHROPIC_DEFAULT_OPUS_MODEL`
- `CLAUDE_CODE_EFFORT_LEVEL`
- `MAX_THINKING_TOKENS`

云平台与端点：

- `ANTHROPIC_BASE_URL`
- `ANTHROPIC_BEDROCK_BASE_URL`
- `ANTHROPIC_BEDROCK_MANTLE_BASE_URL`
- `ANTHROPIC_VERTEX_BASE_URL`
- `ANTHROPIC_VERTEX_PROJECT_ID`
- `CLAUDE_CODE_USE_BEDROCK`
- `CLAUDE_CODE_USE_VERTEX`
- `CLAUDE_CODE_USE_FOUNDRY`
- `CLAUDE_CODE_USE_MANTLE`
- `ANTHROPIC_FOUNDRY_API_KEY`
- `ANTHROPIC_FOUNDRY_BASE_URL`
- `ANTHROPIC_FOUNDRY_RESOURCE`
- `AWS_BEARER_TOKEN_BEDROCK`

运行与性能：

- `API_TIMEOUT_MS`
- `BASH_MAX_TIMEOUT_MS`
- `BASH_MAX_OUTPUT_LENGTH`
- `MCP_TIMEOUT`
- `MAX_MCP_OUTPUT_TOKENS`
- `CLAUDE_CODE_MAX_OUTPUT_TOKENS`
- `CLAUDE_CODE_MAX_RETRIES`
- `CLAUDE_CODE_MAX_TOOL_USE_CONCURRENCY`
- `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE`
- `CLAUDE_CODE_AUTO_COMPACT_WINDOW`
- `DISABLE_AUTO_COMPACT`
- `DISABLE_COMPACT`

功能开关：

- `CLAUDE_CODE_SIMPLE`
- `CLAUDE_CODE_DISABLE_BACKGROUND_TASKS`
- `CLAUDE_CODE_ENABLE_TASKS`
- `ENABLE_TOOL_SEARCH`
- `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS`
- `CLAUDE_CODE_DISABLE_THINKING`
- `CLAUDE_CODE_DISABLE_ADAPTIVE_THINKING`
- `CLAUDE_CODE_DISABLE_1M_CONTEXT`
- `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS`
- `CLAUDE_CODE_DISABLE_AUTO_MEMORY`
- `CLAUDE_CODE_DISABLE_FILE_CHECKPOINTING`
- `CLAUDE_CODE_DISABLE_ATTACHMENTS`
- `CLAUDE_CODE_DISABLE_CLAUDE_MDS`
- `CLAUDE_CODE_RESUME_INTERRUPTED_TURN`

插件、MCP 与 IDE：

- `CLAUDE_CODE_DISABLE_MCP`
- `ENABLE_CLAUDEAI_MCP_SERVERS`
- `CLAUDE_CODE_PLUGIN_SEED_DIR`
- `CLAUDE_CODE_PLUGIN_GIT_TIMEOUT_MS`
- `CLAUDE_CODE_PLUGIN_CACHE_DIR`
- `CLAUDE_CODE_DISABLE_OFFICIAL_MARKETPLACE_AUTOINSTALL`
- `CLAUDE_CODE_SYNC_PLUGIN_INSTALL`
- `CLAUDE_CODE_SYNC_PLUGIN_INSTALL_TIMEOUT_MS`
- `CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL`
- `CLAUDE_CODE_AUTO_CONNECT_IDE`
- `CLAUDE_CODE_IDE_HOST_OVERRIDE`
- `CLAUDE_CODE_IDE_SKIP_VALID_CHECK`

界面与无障碍：

- `CLAUDE_CODE_NO_FLICKER`
- `CLAUDE_CODE_SCROLL_SPEED`
- `CLAUDE_CODE_DISABLE_MOUSE`
- `CLAUDE_CODE_ACCESSIBILITY`
- `CLAUDE_CODE_SYNTAX_HIGHLIGHT`
- `CLAUDE_CODE_DISABLE_TERMINAL_TITLE`

代理与会话：

- `CLAUDE_CODE_SUBAGENT_MODEL`
- `CLAUDE_CODE_TEAM_NAME`
- `CLAUDE_CODE_TASK_LIST_ID`
- `CLAUDE_CODE_MAX_TURNS`
- `CLAUDE_REMOTE_CONTROL_SESSION_NAME_PREFIX`
- `CLAUDE_CONFIG_DIR`
- `CLAUDE_CODE_TMPDIR`

网络与代理：

- `HTTP_PROXY`
- `HTTPS_PROXY`
- `NO_PROXY`
- `CLAUDE_CODE_PROXY_RESOLVES_HOSTS`

还有一些处于变更日志或 schema 中、但官方文档未完全确认的变量，例如：

- `CLAUDE_CODE_SKIP_SETTINGS_SETUP`
- `CLAUDE_CODE_PROMPT_CACHING_ENABLED`
- `CLAUDE_CODE_DISABLE_TOOLS`
- `DISABLE_NON_ESSENTIAL_MODEL_CALLS`
- `CLAUDE_CODE_HIDE_ACCOUNT_INFO`

---

## 常用命令

| 命令 | 说明 |
|---|---|
| `/model` | 切换模型并调整 effort |
| `/effort` | 直接设置 `low`、`medium`、`high` |
| `/config` | 打开交互式配置界面 |
| `/memory` | 查看 / 编辑全部记忆文件 |
| `/agents` | 管理子代理 |
| `/mcp` | 管理 MCP 服务器 |
| `/hooks` | 查看钩子 |
| `/plugin` | 管理插件 |
| `/keybindings` | 配置快捷键 |
| `/skills` | 查看与管理技能 |
| `/permissions` | 查看与管理权限规则 |
| `--doctor` | 诊断配置问题 |
| `--debug` | 启用调试模式 |

---

## 快速参考：完整示例

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",
  "model": "sonnet",
  "agent": "code-reviewer",
  "language": "english",
  "cleanupPeriodDays": 30,
  "autoUpdatesChannel": "stable",
  "alwaysThinkingEnabled": true,
  "showThinkingSummaries": true,
  "includeGitInstructions": true,
  "defaultShell": "bash",
  "plansDirectory": "./plans",
  "effortLevel": "medium",

  "worktree": {
    "symlinkDirectories": ["node_modules"],
    "sparsePaths": ["packages/my-app", "shared/utils"]
  },

  "modelOverrides": {
    "claude-opus-4-6": "arn:aws:bedrock:us-east-1:123456789:inference-profile/anthropic.claude-opus-4-6-v1:0"
  },

  "autoMode": {
    "environment": [
      "Source control: github.example.com/acme-corp and all repos under it",
      "Trusted internal domains: *.internal.example.com"
    ]
  },

  "permissions": {
    "allow": [
      "Edit(*)",
      "Write(*)",
      "Bash(npm run *)",
      "Bash(git *)",
      "WebFetch(domain:*)",
      "mcp__*",
      "Agent(*)"
    ],
    "deny": [
      "Read(.env)",
      "Read(./secrets/**)"
    ],
    "additionalDirectories": ["../shared/"],
    "defaultMode": "acceptEdits"
  },

  "enableAllProjectMcpServers": true,

  "sandbox": {
    "enabled": true,
    "excludedCommands": ["git", "docker"],
    "filesystem": {
      "denyRead": ["./secrets/"],
      "denyWrite": ["./.env"]
    }
  },

  "attribution": {
    "commit": "Generated with Claude Code",
    "pr": ""
  },

  "statusLine": {
    "type": "command",
    "command": "git branch --show-current"
  },

  "spinnerTipsEnabled": true,
  "spinnerTipsOverride": {
    "tips": ["Custom tip 1", "Custom tip 2"],
    "excludeDefault": false
  },
  "prefersReducedMotion": false,

  "env": {
    "NODE_ENV": "development",
    "CLAUDE_CODE_EFFORT_LEVEL": "medium"
  }
}
```

---

## 来源

- [Claude Code Settings Documentation](https://code.claude.com/docs/en/settings)
- [Claude Code Settings JSON Schema](https://json.schemastore.org/claude-code-settings.json)
- [Claude Code Changelog](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
- [Claude Code GitHub Settings Examples](https://github.com/feiskyer/claude-code-settings)
- [Shipyard - Claude Code CLI Cheatsheet](https://shipyard.build/blog/claude-code-cheat-sheet/)
- [Claude Code Environment Variables Reference](https://code.claude.com/docs/en/env-vars)
- [Claude Code Permissions Reference](https://code.claude.com/docs/en/permissions)
