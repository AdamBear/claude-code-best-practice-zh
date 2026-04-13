# Agent Teams 实现

![Last Updated](https://img.shields.io/badge/Last_Updated-Mar_12%2C_2026-white?style=flat&labelColor=555)

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

<a href="#time-orchestration"><img src="../!/tags/implemented-hd.svg" alt="已实现"></a>

<p align="center">
  <img src="assets/impl-agent-teams.png" alt="Agent Teams 实战，使用 tmux 分屏模式" width="100%">
</p>

Agent Teams 会启动 **多个彼此独立的 Claude Code 会话**，并通过共享任务列表协作。它不同于子代理（同一会话内隔离出来的上下文分叉）；团队中的每个成员都会自动获得完整的上下文窗口，并加载 CLAUDE.md、MCP 服务器和技能。

---

## ![How to Use](../!/tags/how-to-use.svg)

时间编排工作流完全由一个代理团队构建。要运行成品：

```bash
cd agent-teams
claude
/time-orchestrator
```

这会触发 **Command → Agent → Skill** 流水线：代理获取迪拜当前时间，技能把它渲染为 SVG 时间卡片并写入 `agent-teams/output/dubai-time.svg`。

---

## ![How to Implement](../!/tags/how-to-implement.svg)

你可以用 Agent Teams 复刻天气编排工作流。在这个示例中，时间编排工作流就是完全由代理团队搭建的。

### 1. 安装 [iTerm2](https://iterm2.com/) 和 tmux

```bash
brew install --cask iterm2
brew install tmux
```

### 2. 启动 iTerm2 → tmux → Claude

```bash
tmux new -s dev
CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1 claude
```

### 3. 使用团队结构提示词

<a id="time-orchestration"></a>

把下面这个提示词粘贴给 Claude，即可用 Agent Teams 启动完整的时间编排工作流：

主提示词：**[agent-teams-prompt.md](../agent-teams/agent-teams-prompt.md)**

### 团队协作流程

```text
+----------------------------------------------------------------------------------+
|                                   LEAD（你）                                     |
|                    “Create an agent team to build time orchestration”            |
+----------------------------------------------------------------------------------+
|                           并行启动整个团队                                       |
+----------------------+----------------------+----------------------+
| Command 架构师       | Agent 工程师         | Skill 设计师         |
| 路径：agent-teams/   | 路径：agent-teams/   | 路径：agent-teams/   |
| .claude/commands/    | .claude/agents/      | .claude/skills/      |
| time-orchestrator.md | time-agent.md        | time-svg-creator/    |
+----------------------+----------------------+----------------------+
                \                 |                 /
                 \                |                /
                  +----------------------------------------------+
                  |                 共享任务列表                 |
                  |  □ 约定数据契约：{time, tz, formatted}       |
                  |  □ Command 使用 Agent 工具（不是 bash）      |
                  |  □ Agent 预加载 time-fetcher 技能            |
                  |  □ Skill 从上下文读取时间（不重复抓取）      |
                  |  □ 所有文件都放在 agent-teams/.claude/       |
                  +----------------------------------------------+
                                      |
                                      v
                    +-------------------------------------------+
                    | cd agent-teams && claude                  |
                    |   /time-orchestrator                      |
                    |   Command -> Agent -> Skill               |
                    +-------------------------------------------+
```
