# 定时任务实现

![Last Updated](https://img.shields.io/badge/Last_Updated-Mar_10%2C_2026-white?style=flat&labelColor=555)

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

<a href="#loop-demo"><img src="../!/tags/implemented-hd.svg" alt="已实现"></a>

`/loop` 技能可用于按 cron 间隔调度周期性任务。下面展示的是 `/loop 1m "tell current time"` 的示例：一个每分钟触发一次的简单循环任务。

---

## Loop 演示

### 1. 调度任务

<p align="center">
  <img src="assets/impl-loop-1.png" alt="/loop 1m tell current time 的调度与 cron 配置" width="100%">
</p>

`/loop 1m "tell current time"` 会解析间隔（`1m` → 每 1 分钟一次）、创建 cron 任务，并确认调度结果。几个关键点：

- Cron 的最小粒度是 **1 分钟**，所以 `1m` 会映射为 `*/1 * * * *`
- 循环任务会在 **3 天后自动过期**
- 任务是 **会话级** 的，只存在于记忆中，Claude 退出后就会停止
- 随时可以用 `cron cancel <job-id>` 取消

---

### 2. Loop 运行中

<p align="center">
  <img src="assets/impl-loop-2.png" alt="每分钟触发一次的循环任务" width="100%">
</p>

该任务每分钟触发一次，运行 `date` 并汇报当前时间。每次迭代都会触发异步 **UserPromptSubmit** 和 **Stop** 钩子，这与本仓库中用于声音通知的是同一套钩子系统。

---

## ![How to Use](../!/tags/how-to-use.svg)

```bash
$ claude
> /loop 1m "tell current time"
> /loop 5m /simplify
> /loop 10m "check deploy status"
```

---

## ![How to Implement](../!/tags/how-to-implement.svg)

`/loop` 是 Claude Code 内置技能，无需额外设置。它底层使用 cron 工具（`CronCreate`、`CronList`、`CronDelete`）来管理周期性调度。
