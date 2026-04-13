# 使用 Claude Code 的 10 个技巧：来自 Claude Code 团队

这是 Boris Cherny（[@bcherny](https://x.com/bcherny)），Claude Code 的创造者，于 2026 年 2 月 1 日分享的团队技巧摘要。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 背景

Boris 分享了一些直接来自 Claude Code 团队内部的使用技巧。团队成员使用 Claude 的方式，与 Boris 个人的用法并不完全相同。请记住：Claude Code 没有唯一正确的使用方式，每个人的配置和习惯都不同。你需要自己多尝试，找到最适合你的方式。

<a href="https://x.com/bcherny/status/2017742741636321619"><img src="assets/boris-1-feb-26/0.png" alt="Boris Cherny 介绍推文" width="50%" /></a>

---

## 1/ 做更多并行工作

同时开 3 到 5 个 git worktree，让每个 worktree 各自并行运行一个 Claude 会话。这是团队公认最能释放生产力的做法，也是他们最重要的一条建议。Boris 个人更常用多个 git checkout，但 Claude Code 团队大多数人更偏爱 worktree，这也是 `@amorisscode` 会在 Claude Desktop 应用里为它加入原生支持的原因。

有些人还会给 worktree 命名，并配置 shell alias（例如 `2a`、`2b`、`2c`），这样就能一键在它们之间切换。还有人会专门保留一个“analysis” worktree，只用来读日志和跑 BigQuery。

参见：[Worktrees Docs](https://code.claude.com/docs/en/common...)

<a href="https://x.com/bcherny/status/2017742743125299476"><img src="assets/boris-1-feb-26/1.png" alt="做更多并行工作" width="50%" /></a>

---

## 2/ 每个复杂任务都先进入 Plan 模式

把精力投入到计划阶段，这样 Claude 才更有机会一次性完成实现。

有人会先让一个 Claude 写计划，再拉起第二个 Claude，按资深工程师的标准去审查这份计划。

还有人说，只要事情开始偏离预期，他们就会立刻切回 Plan 模式重新规划，而不是硬着头皮往前推。他们也会明确要求 Claude 在验证阶段进入 Plan 模式，而不只是构建阶段。

<a href="https://x.com/bcherny/status/2017742745365057733"><img src="assets/boris-1-feb-26/2.png" alt="每个复杂任务都先进入 Plan 模式" width="50%" /></a>

---

## 3/ 持续投入你的 CLAUDE.md

每次纠正完 Claude 之后，都补上一句：“Update your CLAUDE.md so you don't make that mistake again.” Claude 非常擅长为自己写规则。

随着时间推移，要毫不留情地编辑你的 `CLAUDE.md`。持续迭代，直到你能明显感觉到 Claude 的出错率下降。

有位工程师会让 Claude 为每个任务或项目维护一个 notes 目录，并在每次 PR 之后更新；然后再让 `CLAUDE.md` 指向这个目录。

<a href="https://x.com/bcherny/status/2017742747067945390"><img src="assets/boris-1-feb-26/3.png" alt="持续投入你的 CLAUDE.md" width="50%" /></a>

---

## 4/ 创建你自己的技能，并提交到 Git

这样你就能在所有项目里复用。以下是团队给出的建议：

- 如果一件事你每天会做不止一次，就把它做成一个技能或命令
- 写一个 `/techdebt` slash command，在每次会话结束时运行，用来发现并清理重复代码
- 配一个 slash command，把最近 7 天的 Slack、GDrive、Asana 和 GitHub 同步成一份上下文汇总
- 构建 analytics-engineer 风格的智能体，用来写 dbt model、审查代码，并在 dev 环境测试改动

参见：[Extend Claude with Skills — Claude Code Docs](https://code.claude.com/docs/en/skills)

<a href="https://x.com/bcherny/status/2017742748984742078"><img src="assets/boris-1-feb-26/4.png" alt="创建你自己的技能" width="50%" /></a>

---

## 5/ Claude 能自己修掉大多数 Bug

团队是这样做的：

先启用 Slack MCP，然后把 Slack 上的 bug 讨论串直接贴给 Claude，只说一句 “fix.”。完全不需要切换上下文。

或者，直接说 “Go fix the failing CI tests.”，不要对过程做微观管理。

还可以把 docker 日志交给 Claude 来排查分布式系统问题，它在这方面的能力强得出人意料。

<a href="https://x.com/bcherny/status/2017742750473720121"><img src="assets/boris-1-feb-26/5.png" alt="Claude 能自己修掉大多数 Bug" width="50%" /></a>

---

## 6/ 提升你的提示词能力

a. **挑战 Claude。** 你可以说：“Grill me on these changes and don't make a PR until I pass your test.” 让 Claude 充当你的审查者。或者说：“Prove to me this works”，让 Claude 对比 `main` 和你的功能分支之间的行为差异。

b. **在得到一个平庸修复之后，** 可以这样说：“Knowing everything you know now, scrap this and implement the elegant solution.”

c. **编写详细规格说明，** 在交给 Claude 之前尽量消除歧义。你越具体，输出通常就越好。

<a href="https://x.com/bcherny/status/2017742752566632544"><img src="assets/boris-1-feb-26/6.png" alt="提升你的提示词能力" width="50%" /></a>

---

## 7/ 终端与环境配置

团队非常喜欢 Ghostty。很多人欣赏它的同步渲染、24 位色彩和完善的 unicode 支持。

为了更方便地同时驾驭多个 Claude，可以使用 `/statusline` 自定义状态栏，让它始终显示上下文使用量和当前 git 分支。很多人还会给终端标签页命名并做颜色区分，有时会配合 tmux 使用，每个任务或 worktree 一个标签页。

可以使用语音输入。你说话的速度大约是打字的 3 倍，因此提示词会自然变得更详细。（macOS 上双击 `fn`）

参见：[Terminal Setup Docs](https://code.claude.com/docs/en/termin...)

<a href="https://x.com/bcherny/status/2017742753971769626"><img src="assets/boris-1-feb-26/7.png" alt="终端与环境配置" width="50%" /></a>

---

## 8/ 使用子代理

a. 在任何你希望 Claude 投入更多算力的问题后面，加上一句“use subagents”。

b. 把单独的任务卸载给子代理，让主代理的上下文窗口保持干净、聚焦。

c. 通过钩子把权限请求路由给 Opus 4.5，让它扫描攻击风险并自动批准安全请求。参见：[Hooks Docs](https://code.claude.com/docs/en/hooks#...)

<a href="https://x.com/bcherny/status/2017742755737555434"><img src="assets/boris-1-feb-26/8.png" alt="使用子代理" width="50%" /></a>

---

## 9/ 用 Claude 做数据与分析

让 Claude Code 使用 `bq` CLI 即时拉取并分析指标。团队把 BigQuery 技能直接提交进代码库，大家都在 Claude Code 里直接跑分析查询。Boris 个人已经有半年多没手写过一行 SQL 了。

只要某个数据库提供 CLI、MCP 或 API，这种做法通常都适用。

<a href="https://x.com/bcherny/status/2017742757666902374"><img src="assets/boris-1-feb-26/9.png" alt="用 Claude 做数据与分析" width="50%" /></a>

---

## 10/ 用 Claude 学习

以下是团队用 Claude Code 学习的一些做法：

a. 在 `/config` 中启用 “Explanatory” 或 “Learning” 输出风格，让 Claude 在改代码时顺带解释“为什么这么做”。

b. 让 Claude 生成一个可视化的 HTML 演示文稿，用来解释你不熟悉的代码。它做幻灯片的效果意外地不错。

c. 让 Claude 画出新协议或代码库的 ASCII 图示，帮助你理解结构。

d. 构建一个间隔重复学习技能：你先讲述自己的理解，Claude 再通过追问补齐知识空缺，并把结果保存下来。

<a href="https://x.com/bcherny/status/2017742759218794768"><img src="assets/boris-1-feb-26/10.png" alt="用 Claude 学习" width="50%" /></a>

---

## 来源

- [Boris Cherny (@bcherny) on X — February 1, 2026](https://x.com/bcherny/status/2017742741636321619)
