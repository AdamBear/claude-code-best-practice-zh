---
name: time-svg-creator
description: 创建展示迪拜当前时间的 SVG 时间卡片。把 SVG 写入 agent-teams/output/dubai-time.svg，并更新 agent-teams/output/output.md。
allowed-tools: Write, Read
---

# Time SVG Creator Skill

创建一张展示迪拜（阿联酋）时间的可视化 SVG 卡片，并写出输出文件。

## 任务

你会从调用上下文中收到三个字段：`time`、`timezone` 和 `formatted`。请创建一张 SVG 时间卡片，并同时写出 SVG 和 Markdown 摘要。

## 说明

1. **创建 SVG**：使用 [reference.md](reference.md) 中的 SVG 模板，将占位符替换成真实值
2. **写入 SVG 文件**：写入 `agent-teams/output/dubai-time.svg`
3. **写入摘要**：使用 [reference.md](reference.md) 中的 Markdown 模板，写入 `agent-teams/output/output.md`

## 规则

- 严格使用传入的时间值，**绝不要** 重新抓取或重新计算
- SVG 必须是自包含且有效的
- 两个输出文件都必须写入 `agent-teams/output/` 目录

## 附加资源

- SVG 模板、输出模板和设计规格见 [reference.md](reference.md)
- 输入 / 输出示例见 [examples.md](examples.md)
