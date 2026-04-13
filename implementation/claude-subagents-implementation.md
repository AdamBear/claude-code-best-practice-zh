# 子代理实现

![Last Updated](https://img.shields.io/badge/Last_Updated-Mar_02%2C_2026_07%3A59_PM_PKT-white?style=flat&labelColor=555)

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

<a href="#weather-agent"><img src="../!/tags/implemented-hd.svg" alt="已实现"></a>

天气代理在本仓库中被实现为 **Command → Agent → Skill** 架构模式的示例，用于展示两种不同的技能模式。

---

## Weather Agent

**文件**： [`.claude/agents/weather-agent.md`](../.claude/agents/weather-agent.md)

```yaml
---
name: weather-agent
description: Use this agent PROACTIVELY when you need to fetch weather data for
  Dubai, UAE. This agent fetches real-time temperature from Open-Meteo
  using its preloaded weather-fetcher skill.
tools: WebFetch, Read, Write, Edit
model: sonnet
color: green
maxTurns: 5
permissionMode: acceptEdits
memory: project
skills:
  - weather-fetcher
---

# Weather Agent

You are a specialized weather agent that fetches weather data for Dubai,
UAE.

## Your Task

Execute the weather workflow by following the instructions from your preloaded
skill:

1. **Fetch**: Follow the `weather-fetcher` skill instructions to fetch the
   current temperature
2. **Report**: Return the temperature value and unit to the caller
3. **Memory**: Update your agent memory with the reading details for
   historical tracking

...
```

该代理预加载了一个技能（`weather-fetcher`），其中提供了从 Open-Meteo 获取天气的说明。它会把温度值和单位返回给调用它的命令。

---

## ![How to Use](../!/tags/how-to-use.svg)

```bash
$ claude
> what is the weather in dubai?
```

---

## ![How to Implement](../!/tags/how-to-implement.svg)

你可以使用 `/agents` 命令创建一个代理：
```bash
$ claude
> /agents
```

也可以直接让 Claude 帮你创建，它会在 `.claude/agents/<name>.md` 中生成带 YAML frontmatter 和正文的 Markdown 文件。

---

<a href="https://github.com/shanraisshan/claude-code-best-practice#orchestration-workflow"><img src="../!/tags/orchestration-workflow-hd.svg" alt="编排工作流"></a>

天气代理是 **Command → Agent → Skill** 编排模式中的 **Agent**。它从 `/weather-orchestrator` 命令接收工作流，通过预加载技能 `weather-fetcher` 获取温度，然后由命令继续调用独立的 `weather-svg-creator` 技能生成可视化输出。

<p align="center">
  <img src="../orchestration-workflow/orchestration-workflow.svg" alt="命令、技能、代理的架构流程" width="100%">
</p>

| 组件 | 角色 | 本仓库中的实现 |
|------|------|----------------|
| **Command** | 入口点、用户交互 | [`/weather-orchestrator`](../.claude/commands/weather-orchestrator.md) |
| **Agent** | 使用预加载技能获取数据（Agent 技能） | [`weather-agent`](../.claude/agents/weather-agent.md) 搭配 [`weather-fetcher`](../.claude/skills/weather-fetcher/SKILL.md) |
| **Skill** | 独立创建输出（技能） | [`weather-svg-creator`](../.claude/skills/weather-svg-creator/SKILL.md) |
