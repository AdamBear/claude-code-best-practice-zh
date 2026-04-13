---
model: haiku
---

# Time Orchestrator Command

获取迪拜（Asia/Dubai，UTC+4）当前时间，并生成一张可视化 SVG 时间卡片。

## 工作流

### 步骤 1：获取迪拜当前时间

使用 Agent 工具调用时间代理：
- subagent_type: time-agent
- description: 获取迪拜当前时间
- prompt: 获取迪拜（Asia/Dubai，UTC+4）当前时间。请严格返回三个字段：`time`（仅时间部分，例如 "14:30:45"）、`timezone`（"GST (UTC+4)"）和 `formatted`（完整格式化字符串，例如 "2026-03-12 14:30:45 +04"）。该代理已预加载一个技能（time-fetcher），其中包含详细说明。
- model: haiku

等待代理完成，并捕获返回的时间数据。

### 数据契约

time-agent **必须** 返回这三个字段：
- **time**：时间部分（例如 `"14:30:45"`）
- **timezone**：`"GST (UTC+4)"`
- **formatted**：完整格式化字符串（例如 `"2026-03-12 14:30:45 +04"`）

### 步骤 2：创建 SVG 时间卡片

使用 Skill 工具调用 time-svg-creator 技能：
- skill: time-svg-creator
- args: 传入步骤 1 返回的时间数据，包含 `time`、`timezone` 和 `formatted`

该技能会使用步骤 1 已提供的时间数据（在当前上下文中可用）来创建 SVG 卡片并写出输出文件。

## 关键要求

1. **time-agent 必须用 Agent 工具调用**：不要用 bash 命令调用代理。必须使用 Agent 工具，并设置 `subagent_type: "time-agent"`。
2. **SVG 创建器必须用 Skill 工具调用**：应通过 `skill: "time-svg-creator"` 调用，而不是使用 Agent 工具。
3. **顺序执行**：必须先等待代理完成并返回时间数据，再调用技能。不要并行执行。
4. **数据传递**：调用技能时，确保代理返回的三个字段（`time`、`timezone`、`formatted`）都在上下文中可用。

## 输出摘要

两个步骤完成后，向用户清晰汇报：
- 获取到的当前迪拜时间
- 时区：GST (UTC+4)
- 完整格式化时间戳
- SVG 卡片已创建：`agent-teams/output/dubai-time.svg`
- 摘要已写入：`agent-teams/output/output.md`
