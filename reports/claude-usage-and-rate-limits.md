# Claude Code：使用量、速率限制与额外用量

理解 Claude Code 的使用限制如何工作，以及在触发限制后如何继续工作。

<table width="100%">
<tr>
<td><a href="../">返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 概览

订阅版 Claude Code（Pro、Max 5x、Max 20x）都带有基于滚动时间窗重置的使用限制。系统内置了 3 个 slash 命令，帮助你监控和管理使用量：

| 命令 | 说明 | 适用对象 |
|---------|-------------|--------------|
| `/usage` | 查看套餐额度与当前速率限制状态 | Pro、Max 5x、Max 20x |
| `/extra-usage` | 在触发限制后配置按量付费溢出使用 | Pro、Max 5x、Max 20x |
| `/cost` | 查看当前会话的 token 使用量与花费 | API key 用户 |

---

## `/usage`：查看你的额度

显示你当前套餐的使用限制和速率限制状态。适合在快要触发限制前，先确认自己还剩多少容量。

---

## `/extra-usage`：超出限制后继续工作

`/extra-usage` 用于配置 **按量付费的溢出计费**。这样当你触发套餐速率限制时，Claude Code 不会直接阻塞，而是可以无缝继续工作。

### 它是怎么工作的

1. 你先触发了套餐的速率限制（额度每 5 小时重置一次）
2. 如果已启用 extra usage 且账户中有可用余额，Claude Code 会继续运行，不会中断
3. 超出的 token 会按 **标准 API 价格** 单独计费，不包含在订阅费里

### 如何配置

CLI 中的 `/extra-usage` 命令会引导你完成配置。你也可以直接在 claude.ai 的 **Settings > Usage** 页面里设置：

1. 启用 extra usage
2. 添加支付方式
3. 设置**月度支出上限**（也可以选择无限制）
4. 可选：加入**预充值余额**，并在余额低于阈值时自动充值

### 关键细节

| 项目 | 数值 |
|--------|-------|
| 每日兑换上限 | $2,000/day |
| 计费方式 | 独立于订阅费，按标准 API 价格计费 |
| 限制重置窗口 | 每 5 小时一次 |

### 已知问题

截至 2026 年 2 月，CLI 里的 `/extra-usage` 命令仍处于[未文档化](https://github.com/anthropics/claude-code/issues/12396)状态，可能只会弹出一个登录窗口，却没有清晰的配置选项。当前更可靠的方式，仍然是直接通过 **claude.ai 网页端**配置。

---

## `/cost`：会话花费（API 用户）

如果你是通过 API key 认证，而不是订阅套餐，那么 `/cost` 会显示：

- 当前会话的总花费
- API 持续时间与实际墙钟时间
- token 使用拆分
- 本次会话产生的代码改动

这个命令与 Pro/Max 订阅用户无关。

---

## Fast Mode 与 Extra Usage 的关系

Fast mode（`/fast`）会使用输出更快的 Claude Opus 4.6。它和 extra usage 之间有一个特殊的计费关系：

- Fast mode 的使用**从第一个 token 开始就始终计入 extra usage**
- 即使你的订阅套餐额度还有剩余，也是如此
- Fast mode 不会消耗套餐内自带的速率限制额度

这意味着，如果你要使用 `/fast`，就必须先启用并充值 extra usage。

---

## CLI 启动参数

有两个启动参数与使用预算相关（仅 API key 用户、print mode 生效）：

| 参数 | 说明 |
|------|-------------|
| `--max-budget-usd <AMOUNT>` | 在 API 调用花费达到某个美元上限后停止 |
| `--max-turns <NUMBER>` | 限制智能体回合数 |

完整列表见 [CLI Startup Flags Reference](claude-cli-startup-flags.md)。

---

## 资料来源

- [Extra usage for paid Claude plans - Claude Help Center](https://support.claude.com/en/articles/12429409-extra-usage-for-paid-claude-plans)
- [Using Claude Code with your Pro or Max plan - Claude Help Center](https://support.claude.com/en/articles/11145838-using-claude-code-with-your-pro-or-max-plan)
- [/extra-usage slash command is undocumented - GitHub Issue #12396](https://github.com/anthropics/claude-code/issues/12396)
- [Claude Code CLI Reference](https://code.claude.com/docs/en/cli-reference)
