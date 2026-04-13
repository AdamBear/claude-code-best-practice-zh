# Agents、Commands 与 Skills：分别该在什么时候用

对 Claude Code 三种扩展机制的对比：子代理、命令和技能。

<table width="100%">
<tr>
<td><a href="../">返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

![Slash 菜单中展示 time-skill、time-command 和 time-agent](assets/agent-command-skill-1.jpg)

---

## 一图速览

| | Agent | Command | Skill |
|---|---|---|---|
| **位置** | `.claude/agents/<name>.md` | `.claude/commands/<name>.md` | `.claude/skills/<name>/SKILL.md` |
| **上下文** | 独立的子代理进程 | 内联（主对话中） | 内联（主对话中） |
| **用户可直接调用** | 否，没有 `/` 菜单，只能由 Claude 或 Agent 工具触发 | 是，`/command-name` | 是，`/skill-name`（除非 `user-invocable: false`） |
| **可被 Claude 自动触发** | 是，通过 `description` 字段 | 否 | 是，通过 `description` 字段（除非 `disable-model-invocation: true`） |
| **接受参数** | 通过 `prompt` 参数 | `$ARGUMENTS`、`$0`、`$1` | `$ARGUMENTS`、`$0`、`$1` |
| **动态上下文注入** | 否 | 是，`` !`command` `` | 是，`` !`command` `` |
| **独立上下文窗口** | 是，隔离运行 | 否，共享主上下文 | 否，共享主上下文（除非 `context: fork`） |
| **模型覆盖** | `model:` frontmatter | `model:` frontmatter | `model:` frontmatter |
| **工具限制** | `tools:` / `disallowedTools:` | `allowed-tools:` | `allowed-tools:` |
| **钩子** | `hooks:` frontmatter | 无 | `hooks:` frontmatter |
| **记忆** | `memory:` frontmatter（user/project/local） | 无 | 无 |
| **可预加载技能** | 是，`skills:` frontmatter | 无 | 无 |
| **MCP servers** | `mcpServers:` frontmatter | 无 | 无 |

---

## 什么时候用哪一种

### 在这些场景下用 Agent

- 任务是**自主且多步骤**的，agent 需要自行探索、判断并执行，而不是持续等待主对话指挥
- 你需要**上下文隔离**，不希望这项工作污染主对话窗口
- agent 需要跨会话保留**持久记忆**，例如能逐渐学习项目习惯的代码审查 agent
- 你希望通过技能**预加载领域知识**，又不想把这些内容塞进主上下文
- 任务适合**后台运行**，或者适合放在 **git worktree** 里执行
- 你需要**工具权限限制**，或需要不同的**权限模式**（例如 `acceptEdits`、`plan`）

**示例**：`weather-agent` 会自主拉取天气数据，预加载了 `weather-fetcher` 技能，在隔离上下文中运行，并带有受限工具权限。

### 在这些场景下用 Command

- 你需要一个**用户主动触发的入口**，也就是用户明确发起的工作流
- 这个工作流需要**编排**其他 agent 或技能
- 你希望**保持上下文精简**，因为命令内容在用户真正触发前不会注入到会话上下文中

**示例**：`weather-orchestrator` 由用户手动触发，先询问摄氏/华氏偏好，再调用 agent，最后再调用 SVG 技能生成结果。

### 在这些场景下用 Skill

- 你希望 **Claude 能根据用户意图自动触发**，因为技能描述会被注入会话上下文用于语义匹配
- 任务本身是一个**可复用流程**，可以被命令、agent 或 Claude 自身复用
- 你需要**agent 预加载**，让某个 agent 在启动时就带上领域知识

**示例**：`weather-svg-creator` 会在用户要求天气卡片时被 Claude 自动调用，也可以被命令显式调用。

---

## Command → Agent → Skill 分层架构

这个仓库展示了一种分层编排模式：

```
用户触发 /command
    ↓
Command 负责编排整个流程
    ↓
Command 调用 Agent（独立上下文，自主执行）
    ↓
Agent 使用预加载的 Skill（领域知识）
    ↓
Command 再调用 Skill（内联生成输出）
```

**具体例子**：天气系统

```
/weather-orchestrator（command：入口，询问 C/F）
    ↓
weather-agent（agent：自主获取温度）
    └── weather-fetcher（agent skill：预加载的 API 指令）
    ↓
weather-svg-creator（skill：内联生成 SVG）
```

---

## Frontmatter 对比

### Agent Frontmatter

```yaml
---
name: my-agent
description: Use this agent PROACTIVELY when...
tools: Read, Write, Edit, Bash
model: sonnet
maxTurns: 10
permissionMode: acceptEdits
memory: user
skills:
  - my-skill
---
```

### Command Frontmatter

```yaml
---
description: Do something useful
argument-hint: [issue-number]
allowed-tools: Read, Edit, Bash(gh *)
model: sonnet
---
```

### Skill Frontmatter

```yaml
---
name: my-skill
description: Do something when the user asks for...
argument-hint: [file-path]
disable-model-invocation: false
user-invocable: true
allowed-tools: Read, Grep, Glob
model: sonnet
context: fork
agent: general-purpose
---
```

---

## 关键区别

### 自动触发能力

| 机制 | Claude 能自动触发吗？ | 如何阻止 |
|-----------|------------------------|----------------|
| Agent | 可以，通过 `description`（写 “PROACTIVELY” 会更容易触发） | 删除或弱化描述 |
| Command | 不可以，始终由用户通过 `/` 手动触发 | 不适用 |
| Skill | 可以，通过 `description` | 设置 `disable-model-invocation: true` |

### `/` 菜单中的可见性

| 机制 | 会出现在 `/` 菜单里吗？ | 如何隐藏 |
|-----------|---------------------|-------------|
| Agent | 不会 | 不适用 |
| Command | 一定会出现 | 无法隐藏 |
| Skill | 默认会出现 | 设置 `user-invocable: false` |

### 上下文隔离

| 机制 | 是否在独立上下文中运行？ | 如何配置 |
|-----------|---------------------|-----------------|
| Agent | 始终是 | 内建行为 |
| Command | 不是 | 不适用 |
| Skill | 可选 | 设置 `context: fork` |

---

## 示例问题：“现在几点了？”

这个仓库里为同一个任务都定义了三种机制：在 PKT 显示当前时间。假设用户直接输入 **“What is the current time?”**，而没有显式调用任何 `/` 命令，那么会发生什么？

| 机制 | 会触发吗？ | 原因 |
|-----------|--------------|---------------|
| `time-command` | 不会 | Command **永远不会被自动触发**。用户必须显式输入 `/time-command` 才会运行。Command 没有自动发现路径，严格属于用户主动入口。 |
| `time-agent` | **可能会** | 该 agent 的 `description` 写着 *"Use this agent to display the current time in Pakistan Standard Time"*。Claude 可能基于用户意图匹配后，用 Agent 工具拉起它。但 agent 会运行在**独立上下文窗口**中，对这么简单的任务来说通常显得偏重。 |
| `time-skill` | **最有可能会** | 该 skill 的 `description` 写着 *"Display the current time in Pakistan Standard Time (PKT, UTC+5). Use when the user asks for the current time, Pakistan time, or PKT."* Claude 很容易匹配这个意图，并通过 Skill 工具调用它。因为它是**内联运行**，没有额外上下文开销，所以是最轻量的匹配方式。 |

### 触发优先级

当多个机制同时匹配同一意图时，Claude 倾向于选择**满足需求的最轻量方案**：

```
1. Skill（内联、无上下文额外开销）     → 优先
2. Agent（独立上下文、自主执行）      → 当 skill 不可用或任务更复杂时使用
3. Command（永远不会自动触发）        → 只有用户手动输入 /time-command 才会运行
```

### 如果 skill 上设置了 `disable-model-invocation: true` 会怎样？

那 Claude **就不能自动触发这个 skill**。此时，agent 会变成唯一还能自动触发的机制，所以 Claude 会退而求其次地启动 `time-agent`，代价是为了一个一行 bash 命令也要额外开一个上下文窗口。

### 如果 skill 和 agent 都禁用了自动触发呢？

那就**不会自动触发任何扩展机制**。Claude 会退回到自己的通用能力，很可能直接运行 `TZ='Asia/Karachi' date`，而不会用到任何扩展。此时如果用户想走扩展机制，只能显式输入 `/time-command` 或 `/time-skill`。

![当用户问 “What is the current time?” 时，Claude 自动触发 time-skill](assets/agent-command-skill-2.png)

---

## 资料来源

- [Claude Code Skills - Docs](https://code.claude.com/docs/en/skills)
- [Claude Code Sub-agents - Docs](https://code.claude.com/docs/en/sub-agents)
- [Claude Code Slash Commands - Docs](https://code.claude.com/docs/en/slash-commands)
- [Skills Best Practice](../best-practice/claude-skills.md)
- [Commands Best Practice](../best-practice/claude-commands.md)
- [Sub-agents Best Practice](../best-practice/claude-subagents.md)
