# CLAUDE.md

本文件为 Claude Code（claude.ai/code）在处理本仓库时提供工作指引。

## 仓库概览

这是一个面向 Claude Code 配置与使用方式的最佳实践仓库，用来展示技能、子代理、钩子和命令的组织模式。它是一个参考实现仓库，而不是传统的应用代码仓库。

## 关键组成部分

### 天气系统（示例工作流）

这里通过 **命令 -> 代理 -> 技能** 架构，演示了两种不同的技能模式：

- `/weather-orchestrator` 命令（`.claude/commands/weather-orchestrator.md`）
  入口命令，会先询问用户使用摄氏度还是华氏度，然后调用代理，再调用 SVG 技能。
- `weather-agent` 代理（`.claude/agents/weather-agent.md`）
  使用预加载的 `weather-fetcher` 技能获取温度数据，这属于“代理技能”模式。
- `weather-fetcher` 技能（`.claude/skills/weather-fetcher/SKILL.md`）
  预加载到代理中，负责指导如何从 Open-Meteo 获取天气数据。
- `weather-svg-creator` 技能（`.claude/skills/weather-svg-creator/SKILL.md`）
  独立调用的技能，用于生成天气 SVG 卡片，并写入 `orchestration-workflow/weather.svg` 与 `orchestration-workflow/output.md`。

两种技能模式分别是：
- 代理技能：通过 `skills:` 字段预加载到代理上下文中
- 独立技能：通过 `Skill` 工具直接调用

完整流程图请参见 `orchestration-workflow/orchestration-workflow.md`。

### 技能定义结构

`.claude/skills/<name>/SKILL.md` 下的技能使用 YAML frontmatter，常见字段包括：

- `name`：显示名称和 `/slash-command` 名称，默认取目录名
- `description`：触发时机说明，建议写成便于自动发现的触发语
- `argument-hint`：自动补全提示，例如 `[issue-number]`
- `disable-model-invocation`：设为 `true` 可阻止模型自动调用
- `user-invocable`：设为 `false` 时不会出现在 `/` 菜单中
- `allowed-tools`：技能激活后可直接使用、无需额外许可的工具
- `model`：技能激活时使用的模型
- `context`：设为 `fork` 时在隔离子代理上下文中运行
- `agent`：与 `context: fork` 配套使用的子代理类型，默认是 `general-purpose`
- `hooks`：绑定到该技能的生命周期钩子

### 演示文稿系统

见 `.claude/rules/presentation.md`。所有演示文稿相关工作都会委派给 `presentation-curator` 代理。

### 钩子系统

`.claude/hooks/` 下提供了跨平台声音通知系统：

- `scripts/hooks.py`：Claude Code 钩子事件的主处理脚本
- `config/hooks-config.json`：团队共享配置
- `config/hooks-config.local.json`：个人覆盖配置，已被 git 忽略
- `sounds/`：按钩子事件分类的音频文件，由 ElevenLabs TTS 生成

`.claude/settings.json` 中已配置的钩子事件包括：
`PreToolUse`、`PostToolUse`、`UserPromptSubmit`、`Notification`、`Stop`、`SubagentStart`、`SubagentStop`、`PreCompact`、`SessionStart`、`SessionEnd`、`Setup`、`PermissionRequest`、`TeammateIdle`、`TaskCompleted`、`ConfigChange`。

特殊处理：
Git 提交会触发 `pretooluse-git-committing` 声音。

## 关键模式

### 子代理编排

子代理 **不能** 通过 bash 命令再次调用其他子代理。请使用 Agent 工具（自 v2.1.63 起由 Task 更名而来，`Task(...)` 仍可作为别名使用）：

```text
Agent(subagent_type="agent-name", description="...", prompt="...", model="haiku")
```

在子代理定义中要明确说明工具用途，避免使用 “launch” 这类容易被误解成 shell 启动命令的模糊措辞。

### 子代理定义结构

`.claude/agents/*.md` 下的子代理使用 YAML frontmatter，常见字段包括：

- `name`：子代理标识符
- `description`：触发时机说明；若希望自动调用，可使用 `PROACTIVELY`
- `tools`：逗号分隔的允许工具列表；若省略则继承全部工具，支持 `Agent(agent_type)` 语法
- `disallowedTools`：显式禁用的工具
- `model`：模型别名，如 `haiku`、`sonnet`、`opus` 或 `inherit`
- `permissionMode`：权限模式，例如 `"acceptEdits"`、`"plan"`、`"bypassPermissions"`
- `maxTurns`：最大代理回合数
- `skills`：预加载到代理上下文的技能列表
- `mcpServers`：该子代理使用的 MCP 服务器
- `hooks`：绑定到该子代理的生命周期钩子
- `memory`：持久记忆作用域，支持 `user`、`project`、`local`
- `background`：设为 `true` 时始终后台运行
- `effort`：推理强度覆盖，支持 `low`、`medium`、`high`、`max`
- `isolation`：设为 `"worktree"` 时在临时 git worktree 中运行
- `color`：CLI 输出颜色

### 配置层级

1. **Managed**（`managed-settings.json` / MDM plist / Registry）
   组织级强制配置，无法覆盖
2. 命令行参数
   仅影响当前会话
3. `.claude/settings.local.json`
   个人项目级设置，已被 git 忽略
4. `.claude/settings.json`
   团队共享设置
5. `~/.claude/settings.json`
   全局个人默认设置
6. `hooks-config.local.json` 会覆盖 `hooks-config.json`

### 禁用钩子

可在 `.claude/settings.local.json` 中设置 `"disableAllHooks": true`，也可以在 `hooks-config.json` 中单独关闭特定钩子。

## 回答最佳实践问题时的规则

当用户询问 Claude Code 相关最佳实践问题时，**必须优先搜索本仓库** 中的内容，例如：

- `best-practice/`
- `reports/`
- `tips/`
- `implementation/`
- `README.md`

本仓库是此类问题的首选权威来源。只有在这里找不到答案时，才回退到外部资料或网络搜索。

## 工作流最佳实践

根据本仓库的实践经验：

- 每个 `CLAUDE.md` 文件尽量控制在 200 行以内，以提高遵循稳定性
- 优先用命令来定义工作流，而不是单独依赖代理
- 优先建立面向具体功能的子代理，并配套技能做渐进式披露，而不是使用过于泛化的代理
- 在上下文使用量约 50% 时手动执行 `/compact`
- 复杂任务应从计划模式开始
- 多步骤任务优先使用人工把关的任务清单工作流
- 子任务应尽量拆小，保证单次上下文消耗低于 50%

### 调试建议

- 使用 `/doctor` 做诊断
- 运行长时间终端命令时，优先以后台任务方式执行，便于查看日志
- 可使用浏览器自动化 MCP（如 Claude in Chrome、Playwright、Chrome DevTools）让 Claude 自行检查控制台日志
- 反馈视觉问题时，尽量提供截图

## Git 提交规则

提交修改时，**每个文件单独提交一次**。不要把多个文件的改动打包进同一个提交。

例如，若同时修改了 `README.md`、`best-practice/claude-subagents.md` 和某个技能文件，应分别提交：

- 提交 1：`git add README.md`
  提交说明应只描述 README 的改动
- 提交 2：`git add best-practice/claude-subagents.md`
  提交说明应只描述子代理文档的改动
- 提交 3：`git add .claude/skills/weather-fetcher/SKILL.md`
  提交说明应只描述该技能文件的改动

这样能让 git 历史更清晰，也更容易审阅、回退或按文件粒度 cherry-pick。

## 文档

文档规范见 `.claude/rules/markdown-docs.md`。关键文档包括：

- `best-practice/claude-subagents.md`
  介绍子代理 frontmatter、钩子与仓库内代理
- `best-practice/claude-commands.md`
  介绍 slash command 模式与内置命令参考
- `orchestration-workflow/orchestration-workflow.md`
  介绍天气系统流程图
