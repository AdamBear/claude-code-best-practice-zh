# Power-ups 最佳实践

![Last Updated](https://img.shields.io/badge/Last_Updated-Apr%2002%2C%202026-white?style=flat&labelColor=555)

通过带动画演示的交互式课程讲解 Claude Code 的功能。每个 Power-up 都聚焦一项很多人容易忽略、但 Claude Code 实际能做到的事情。该功能在 v2.1.90 引入。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 用法

```bash
claude
/powerup
```

---

## Power-ups（10）

<p align="center">
  <img src="assets/claude-power-ups/powerup-menu.png" alt="展示 10 节课程的 Power-ups 菜单" width="700">
</p>

| # | Power-up | 主题 |
|---|----------|--------|
| 1 | Talk to your codebase | `@` 文件、行引用 |
| 2 | Steer with modes | `shift+tab`、plan、auto |
| 3 | Undo anything | `/rewind`、`Esc-Esc` |
| 4 | Run in the background | tasks、`/tasks` |
| 5 | Teach Claude your rules | `CLAUDE.md`、`/memory` |
| 6 | Extend with tools | MCP、`/mcp` |
| 7 | Automate your workflow | 技能、钩子 |
| 8 | Multiply yourself | 子代理、`/agents` |
| 9 | Code from anywhere | `/remote-control`、`/teleport` |
| 10 | Dial the model | `/model`、`/effort` |

---

## 示例：Dial the model

最后一个 Power-up 会通过动画演示模型切换与 effort 控制。

<p align="center">
  <img src="assets/claude-power-ups/dial-the-model-1.png" alt="Dial the model：演示深度思考" width="700">
</p>

<p align="center">
  <img src="assets/claude-power-ups/dial-the-model-2.png" alt="Dial the model：演示假设展开" width="700">
</p>

<p align="center">
  <img src="assets/claude-power-ups/dial-the-model-3.png" alt="Dial the model：将 effort 设为 high" width="700">
</p>

---

## 来源

- [Changelog - v2.1.90](https://code.claude.com/docs/en/changelog)
