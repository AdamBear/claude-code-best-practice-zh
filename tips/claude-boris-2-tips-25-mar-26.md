# Squash Merge 与 PR 大小分布：来自 Boris Cherny 的技巧

这是 Boris Cherny（[@bcherny](https://x.com/bcherny)），Claude Code 的创造者，于 2026 年 3 月 25 日分享的洞见摘要。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 1/ 一天 266 次贡献：始终使用 Squash

Boris 分享了他的 GitHub contribution graph：**3 月 24 日这一天共有 266 次贡献**，它们来自 **141 个 PR，且全部采用 squash merge**，每个 PR 的中位数大小是 **118 行**。

- Squash merge 会把一个分支上的所有提交压成目标分支上的一个提交，从而保持历史干净、线性
- 每个 PR 对应一个提交，这让回滚整个功能更简单，也让 `git bisect` 更容易使用
- 在高速度的 AI 辅助工作流中（例如每天 141 个 PR），squash 是更务实的选择，因为分支里那些“fix lint”“try this”之类的小提交本质上只是噪音

<a href="https://x.com/bcherny/status/2038552880018538749"><img src="assets/boris-25-mar-26/1.png" alt="Boris Cherny：266 次贡献，全部 squash" width="50%" /></a>

---

## 2/ PR 大小分布：保持 PR 小而可审

Boris 还分享了这 141 个 PR 的大小分布，总计改动 **45,032 行**（新增 + 删除）：

| 指标 | 行数（新增+删除） | 含义 |
|--------|---------------:|---------|
| **p50** | **118** | PR 大小中位数：一半 PR 不超过 118 行 |
| p90 | 498 | 90% 的 PR 少于 500 行 |
| **p99** | **2,978** | 只有约 1 个 PR 超过约 3000 行 |
| min | 2 | 最小的 PR，只是一个 2 行修复 |
| max | 10,459 | 最大的单个 PR，可能是迁移或生成代码 |

- **118 行的中位数** 说明大多数 PR 都很聚焦、易于审查，即使在每天 141 个 PR 的节奏下也是如此
- 这个分布明显右偏：偶尔出现较大的 PR 是不可避免的（例如批量重命名、迁移），但常态仍然是小而紧凑
- 小 PR 可以降低合并冲突风险，更容易审查，也与 squash merge 形成了理想配合，让回滚更干净

<a href="https://x.com/bcherny/status/2038552880018538749"><img src="assets/boris-25-mar-26/2.png" alt="Boris Cherny：PR 大小分布表" width="50%" /></a>

---

## 来源

- [Boris Cherny (@bcherny) on X — March 25, 2026](https://x.com/bcherny)
