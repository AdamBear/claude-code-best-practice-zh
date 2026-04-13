# 技能实现

![Last Updated](https://img.shields.io/badge/Last_Updated-Mar_02%2C_2026-white?style=flat&labelColor=555)

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

<a href="#weather-svg-creator"><img src="../!/tags/implemented-hd.svg" alt="已实现"></a>

本仓库实现了两个技能，作为 **Command → Agent → Skill** 架构模式的一部分，用来展示两种不同的技能调用方式：**Agent 技能**（预加载）和 **技能**（直接调用）。

---

## Weather SVG Creator（技能）

**文件**： [`.claude/skills/weather-svg-creator/SKILL.md`](../.claude/skills/weather-svg-creator/SKILL.md)

```yaml
---
name: weather-svg-creator
description: Creates an SVG weather card showing the current temperature for
  Dubai. Writes the SVG to orchestration-workflow/weather.svg and updates
  orchestration-workflow/output.md.
---

# Weather SVG Creator Skill

This skill creates a visual SVG weather card and writes the output files.

## Task
Create an SVG weather card displaying the temperature for Dubai, UAE,
and write it along with a summary to output files.

## Instructions
You will receive the temperature value and unit (Celsius or Fahrenheit)
from the calling context.

### 1. Create SVG Weather Card
Generate a clean SVG weather card...

### 2. Write SVG File
Write the SVG content to `orchestration-workflow/weather.svg`.

### 3. Write Output Summary
Write to `orchestration-workflow/output.md`...

...
```

这是一个 **技能**，由命令通过 Skill 工具直接调用。它会从对话上下文中获取温度数据，然后创建 SVG 天气卡片和输出摘要。

---

## Weather Fetcher（Agent 技能）

**文件**： [`.claude/skills/weather-fetcher/SKILL.md`](../.claude/skills/weather-fetcher/SKILL.md)

```yaml
---
name: weather-fetcher
description: Instructions for fetching current weather temperature data
  for Dubai, UAE from Open-Meteo API
user-invocable: false
---

# Weather Fetcher Skill

This skill provides instructions for fetching current weather data.

## Task
Fetch the current temperature for Dubai, UAE in the requested unit
(Celsius or Fahrenheit).

## Instructions
1. Fetch Weather Data: Use the WebFetch tool to get current weather data
   - Celsius URL: https://api.open-meteo.com/v1/forecast?latitude=25.2048&longitude=55.2708&current=temperature_2m&temperature_unit=celsius
   - Fahrenheit URL: https://api.open-meteo.com/v1/forecast?latitude=25.2048&longitude=55.2708&current=temperature_2m&temperature_unit=fahrenheit
2. Extract Temperature: From the JSON response, extract `current.temperature_2m`
3. Return Result: Return the temperature value and unit clearly.

...
```

这是一个 **Agent 技能**，会通过 `skills:` frontmatter 字段在启动时预加载进 `weather-agent`。它不会被直接调用，而是作为注入到代理上下文里的领域知识使用。注意其中的 `user-invocable: false`，这会把它从 `/` 命令菜单中隐藏起来。

---

## 两种技能模式

| 模式 | 调用方式 | 示例 | 关键区别 |
|------|----------|------|----------|
| **技能** | `Skill(skill: "name")` | `weather-svg-creator` | 通过 Skill 工具直接调用 |
| **Agent 技能** | 通过 `skills:` 字段预加载 | `weather-fetcher` | 启动时注入代理上下文 |

---

## ![How to Use](../!/tags/how-to-use.svg)

**技能**：可通过斜杠命令直接调用：
```bash
$ claude
> /weather-svg-creator
```

---

## ![How to Implement](../!/tags/how-to-implement.svg)

你可以直接让 Claude 帮你创建，它会在 `.claude/skills/my-skill/SKILL.md` 里生成带 YAML frontmatter 和正文的 Markdown 文件。

```markdown
# My Skill

Instructions for what the skill does.
```
