# 我如何使用 Claude Code：Boris Cherny 的 13 个技巧

这是 Boris Cherny（[@bcherny](https://x.com/bcherny)），Claude Code 的创造者，于 2026 年 1 月 3 日分享的个人配置技巧摘要。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 背景

Boris 分享了他个人使用 Claude Code 的配置，并特别说明这套配置“意外地朴素”。Claude Code 开箱即用已经很好，所以他其实并没有做太多定制。它没有唯一正确的使用方式：团队在设计产品时就故意让它既能直接使用，也能随你定制和折腾。Claude Code 团队里的每个人，用法都差异很大。

<a href="https://x.com/bcherny/status/2007179832300581177"><img src="assets/boris-3-jan-26/0.png" alt="Boris Cherny 介绍推文" width="50%" /></a>

---

## 1/ 并行运行 5 个 Claude

在终端里并行运行 5 个 Claude。把标签页编号为 1 到 5，并通过系统通知判断什么时候某个 Claude 需要你的输入。

参见：[Terminal Setup Docs](https://code.claude.com/docs/en/terminal)

<a href="https://x.com/bcherny/status/2007179833990885678"><img src="assets/boris-3-jan-26/1.png" alt="并行运行 5 个 Claude" width="50%" /></a>

---

## 2/ 用 claude.ai/code 获得更强并行能力

除了本地 Claude，还可以在 `claude.ai/code` 上并行运行 5 到 10 个 Claude。你可以通过 `claude.ai/code` 把本地会话移交给 Web 会话，在 Chrome 里手动启动会话，再来回“传送”。

<a href="https://x.com/bcherny/status/2007179836704600237"><img src="assets/boris-3-jan-26/2.png" alt="claude.ai/code 并行" width="50%" /></a>

---

## 3/ 所有事情都用带 Thinking 的 Opus

所有事情都使用带 thinking 的 Opus 4.5。Boris 认为这是他用过最好的编程模型。虽然它比 Sonnet 更大、更慢，但因为你需要更少地重新引导它，而且它更擅长工具使用，所以最终几乎总比使用更小模型更快。

<a href="https://x.com/bcherny/status/2007179838864666847"><img src="assets/boris-3-jan-26/3.png" alt="带 thinking 的 Opus" width="50%" /></a>

---

## 4/ 和团队共享一份 CLAUDE.md

为仓库共享一份统一的 `CLAUDE.md`。把它提交到 git，让整个团队每周多次共同维护。每当 Claude 做错一件事，就把这件事写进 `CLAUDE.md`，让 Claude 下次别再犯。

<a href="https://x.com/bcherny/status/2007179840848597422"><img src="assets/boris-3-jan-26/4.png" alt="共享 CLAUDE.md" width="50%" /></a>

---

## 5/ 在 PR 里 @claude 来更新 CLAUDE.md

在代码审查时，可以在同事的 PR 里 `@claude`，让它把某条经验补充进 `CLAUDE.md`，作为该 PR 的一部分。为此可以使用 Claude Code GitHub Action（[install-@hub-action](https://github.com/apps/claude)）。Boris 认为这就是他版本的 Compounding Engineering。

<a href="https://x.com/bcherny/status/2007179842928947333"><img src="assets/boris-3-jan-26/5.png" alt="在 PR 中 @claude" width="50%" /></a>

---

## 6/ 大多数会话都从 Plan 模式开始

大多数会话都从 Plan 模式开始（连续按两次 `shift+tab`）。如果目标是写一个 Pull Request，就先用 Plan 模式，和 Claude 来回讨论，直到你满意它的计划。然后切换到自动接受编辑模式，Claude 通常就能一次性完成。一个好计划非常重要。

<a href="https://x.com/bcherny/status/2007179845336527000"><img src="assets/boris-3-jan-26/6.png" alt="Plan 模式" width="50%" /></a>

---

## 7/ 用 Slash Command 固化内循环工作流

把你每天会重复很多次的“inner loop”工作流都做成 slash command。这样可以省去重复写提示词的麻烦，也让 Claude 自己也能调用这些工作流。命令会提交进 git，并存放在 `.claude/commands/`。

示例：`/commit-push-pr`，用于提交、推送并打开 PR。

<a href="https://x.com/bcherny/status/2007179847949500714"><img src="assets/boris-3-jan-26/7.png" alt="Slash commands" width="50%" /></a>

---

## 8/ 用子代理自动化常见工作流

定期使用几个子代理：例如 `code-simplifier` 会在 Claude 工作完成后简化代码，`verify-app` 带有详细的端到端测试说明，等等。可以把子代理理解为对高频工作流的自动化，和 slash command 很像。

子代理存放在 `.claude/agents/` 中。

<a href="https://x.com/bcherny/status/2007179850139000872"><img src="assets/boris-3-jan-26/8.png" alt="子代理" width="50%" /></a>

---

## 9/ 用 PostToolUse 钩子自动格式化代码

使用 `PostToolUse` 钩子来格式化 Claude 写出的代码。Claude 通常开箱就能生成格式不错的代码，而钩子可以把最后 10% 的收尾工作补齐，避免后续在 CI 里出现格式错误。

```json
"PostToolUse": [
  {
    "matcher": "Write|Edit",
    "hooks": [
      {
        "type": "command",
        "command": "bun run format || true"
      }
    ]
  }
]
```

<a href="https://x.com/bcherny/status/2007179852047335529"><img src="assets/boris-3-jan-26/9.png" alt="用于格式化的 PostToolUse 钩子" width="50%" /></a>

---

## 10/ 预先允许权限，而不是使用 --dangerously-skip-permissions

不要使用 `--dangerously-skip-permissions`。更好的做法是通过 `/permissions` 预先允许那些你确信在当前环境中是安全的常见 bash 命令，以减少不必要的权限提示。这些规则大多会提交到 `.claude/settings.json` 并和团队共享。

<a href="https://x.com/bcherny/status/2007179854077407667"><img src="assets/boris-3-jan-26/10.png" alt="预先允许权限" width="50%" /></a>

---

## 11/ 通过 MCP 让 Claude 使用你所有工具

Claude Code 可以调用你所有的工具。它经常会搜索并向 Slack 发消息（通过 MCP server），用 `bq` CLI 跑 BigQuery 查询来回答分析问题，从 Sentry 抓错误日志等等。Slack MCP 的配置会提交在 `.mcp.json` 中，并与团队共享。

<a href="https://x.com/bcherny/status/2007179856266789204"><img src="assets/boris-3-jan-26/11.png" alt="MCP 工具" width="50%" /></a>

---

## 12/ 用后台代理验证长时间运行的任务

对于运行时间很长的任务，你可以选择：

- 在任务完成后，提示 Claude 用一个后台代理验证它自己的工作
- 使用 agent Stop hook，以更确定性的方式完成这件事
- 或者使用 ralph-wiggum 插件（最早由 @GeoffreyHuntley 提出）

<a href="https://x.com/bcherny/status/2007179858435281082"><img src="assets/boris-3-jan-26/12.png" alt="长时间运行任务的验证" width="50%" /></a>

---

## 13/ 给 Claude 一条验证自己工作的路径

如果你想让 Claude Code 输出高质量结果，最重要的一点也许就是：给 Claude 一条验证自己工作的路径。如果 Claude 拥有这个反馈回路，最终结果的质量可能会提升 2 到 3 倍。

Claude 会测试 Boris 提交的每一个改动。

<a href="https://x.com/bcherny/status/2007179861115511237"><img src="assets/boris-3-jan-26/13.png" alt="给 Claude 一条验证路径" width="50%" /></a>

---

## 来源

- [Boris Cherny (@bcherny) on X — January 3, 2026](https://x.com/bcherny/status/2007179832300581177)
