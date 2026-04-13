# Claude Code 中 15 个隐藏且被低估的功能：来自 Boris Cherny

这是 Boris Cherny（[@bcherny](https://x.com/bcherny)），Claude Code 的创造者，于 2026 年 3 月 30 日分享的技巧摘要。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 背景

Boris 分享了一批他最喜欢、但常常被忽视或使用不足的 Claude Code 功能，重点聚焦在他自己最常使用的那些能力。

<a href="https://x.com/bcherny/status/2038454336355999749"><img src="assets/boris-30-mar-26/0.png" alt="Boris Cherny 介绍推文" width="50%" /></a>

---

## 1/ Claude Code 有移动端应用

你知道 Claude Code 有移动端应用吗？Boris 有很多代码就是通过 iOS 应用写的。这是一种不打开笔记本也能快速改动代码的方便方式。

- 下载 Claude iOS 或 Android 应用
- 进入左侧的 **Code** 标签页
- 你可以直接在手机上审查改动、批准 PR、甚至写代码

<a href="https://x.com/bcherny/status/2038454337811386436"><img src="assets/boris-30-mar-26/1.png" alt="Claude Code 移动端应用" width="50%" /></a>

---

## 2/ 在移动端、Web、桌面端和终端之间迁移会话

运行 `claude --teleport` 或 `/teleport`，把一个云端会话继续接到你的本地机器上。或者运行 `/remote-control`，从手机或 Web 端远程控制一个本地运行中的会话。

- **Teleport**：把云端会话拉回到本地终端
- **Remote Control**：让你从任意设备控制本地会话
- Boris 在 `/config` 里开启了 **"Enable Remote Control for all sessions"**

<a href="https://x.com/bcherny/status/2038454339933548804"><img src="assets/boris-30-mar-26/2.png" alt="Teleport 和 Remote Control" width="50%" /></a>

---

## 3/ `/loop` 和 `/schedule`：最强大的两个功能之一

使用它们可以按固定间隔自动安排 Claude 运行，最长可持续一整周。Boris 本地常驻运行了很多 loop：

- `/loop 5m /babysit`：自动处理代码审查、自动 rebase，并把 PR 一路护送到生产
- `/loop 30m /slack-feedback`：每 30 分钟自动发起一个 PR，用于收集 Slack 反馈
- `/loop /post-merge-sweeper`：自动发 PR 处理他遗漏的代码审查评论
- `/loop 1h /pr-pruner`：关闭陈旧、已无必要的 PR
- ……以及更多

可以多尝试把工作流做成技能，再和 loop 结合起来，威力非常大。

<a href="https://x.com/bcherny/status/2038454341884154269"><img src="assets/boris-30-mar-26/3.png" alt="/loop 和 /schedule" width="50%" /></a>

---

## 4/ 用钩子以确定性方式运行逻辑

通过钩子，你可以把逻辑挂到代理生命周期里。例如：

- 每次启动 Claude 时，**动态加载**上下文（`SessionStart`）
- **记录模型执行的每一条 bash 命令**（`PreToolUse`）
- 把**权限提示**路由到 WhatsApp，由你批准或拒绝（`PermissionRequest`）
- 在 Claude 停下来时**戳它继续工作**（`Stop`）

<a href="https://x.com/bcherny/status/2038454343519932844"><img src="assets/boris-30-mar-26/4.png" alt="使用钩子" width="50%" /></a>

---

## 5/ Cowork Dispatch

Boris 每天都会用 Dispatch 来追 Slack 和邮件、管理文件，以及在离开电脑时远程处理笔记本上的事情。不写代码时，他就在 dispatch。

- Dispatch 是 Claude Desktop 应用的一个**安全远程控制**能力
- 它可以在你授权的前提下使用你的 MCP、浏览器和电脑
- 你可以把它理解为：无论身在何处，都能把非编码任务委托给 Claude

<a href="https://x.com/bcherny/status/2038454345419936040"><img src="assets/boris-30-mar-26/5.png" alt="Cowork Dispatch" width="50%" /></a>

---

## 6/ 前端工作请使用 Chrome 扩展

使用 Claude Code 最重要的一条建议是：**给 Claude 一条验证自己输出结果的路径。** 一旦做到这一点，Claude 就会持续迭代，直到结果足够好。

- 就像让一个人做网站，却不允许他打开浏览器，结果大概率不会好
- 给 Claude 一个浏览器，它就会写代码、反复迭代，直到页面效果变好
- Boris 每次做 Web 代码都会用 Chrome 扩展，它通常比其他类似的 MCP 更稳定

<a href="https://x.com/bcherny/status/2038454347156398333"><img src="assets/boris-30-mar-26/6.png" alt="用于前端工作的 Chrome 扩展" width="50%" /></a>

---

## 7/ 用 Claude Desktop 应用自动启动并测试 Web Server

同样的思路，Desktop 应用内置了让 Claude **自动运行你的 Web Server，甚至在内建浏览器里完成测试** 的能力。

- 在 CLI 或 VSCode 中，你也可以借助 Chrome 扩展实现类似能力
- 但如果你想要一体化体验，直接用 Desktop 应用会更方便

<a href="https://x.com/bcherny/status/2038454348804714642"><img src="assets/boris-30-mar-26/7.png" alt="Desktop 应用中的 Web Server 测试" width="50%" /></a>

---

## 8/ Fork 你的会话

很多人会问，怎样从一个已有会话分叉。两种方式：

1. 在会话中运行 `/branch`
2. 在 CLI 中运行 `claude --resume <session-id> --fork-session`

`/branch` 会创建一个分支会话，而且你会直接进入这个分支。如果要回到原始会话，使用 `claude -r <original-session-id>`。

<a href="https://x.com/bcherny/status/2038454350214041740"><img src="assets/boris-30-mar-26/8.png" alt="Fork 你的会话" width="50%" /></a>

---

## 9/ 用 `/btw` 处理旁路问题

Boris 经常用它来在代理工作时顺手回答一些小问题。`/btw` 允许你提出一个旁路问题，而不会打断代理当前的主任务。

示例：
```
/btw how do I spell dachshund?
> dachshund — German for "badger dog" (dachs + badger, hund + dog).
→→to scroll · Space, Enter, or Escape to dismiss
```

<a href="https://x.com/bcherny/status/2038454351849787485"><img src="assets/boris-30-mar-26/9.png" alt="/btw 处理旁路问题" width="50%" /></a>

---

## 10/ 使用 Git Worktree

Claude Code 对 git worktree 提供了深度支持。想在同一仓库里并行做大量工作，worktree 几乎是必需品。Boris 常年**同时运行几十个 Claude**，而这正是他的实现方式。

- 使用 `claude -w` 在一个 worktree 中启动新会话
- 或者在 Claude Desktop 应用里勾选 **"worktree" checkbox**
- 如果你用的是非 git 的版本控制系统，可以利用 `WorktreeCreate` 钩子加入自己的创建逻辑

<a href="https://x.com/bcherny/status/2038454353787519164"><img src="assets/boris-30-mar-26/10.png" alt="Git worktree" width="50%" /></a>

---

## 11/ 使用 `/batch` 扇出超大规模改动

`/batch` 会先和你对需求做一轮访谈，然后让 Claude 把工作扇出给足够多的 **worktree agent** 去完成，可能是几十个、几百个，甚至上千个。

- 适合大型代码迁移，以及其他可并行化的大规模工作
- 每个 worktree agent 都会在自己独立的代码库副本里工作

<a href="https://x.com/bcherny/status/2038454355469484142"><img src="assets/boris-30-mar-26/11.png" alt="/batch 处理大规模改动" width="50%" /></a>

---

## 12/ 用 `--bare` 让 SDK 启动速度提升最多 10 倍

默认情况下，当你运行 `claude -p`（或 TypeScript / Python SDK）时，Claude 会搜索本地的 `CLAUDE.md`、设置和 MCP。但在非交互式场景里，大多数时候你其实更想通过 `--system-prompt`、`--mcp-config`、`--settings` 等参数显式指定加载内容。

- 这是 SDK 初版设计时留下的一个问题
- 未来版本里，默认行为会切换为 `--bare`
- 当前可以先通过这个 flag 主动启用，从而获得最高 **10 倍更快的启动速度**

```bash
claude -p "summarize this codebase" \
    --output-format=stream-json \
    --verbose \
    --bare
```

<a href="https://x.com/bcherny/status/2038454357088457168"><img src="assets/boris-30-mar-26/12.png" alt="用于 SDK 启动的 --bare 参数" width="50%" /></a>

---

## 13/ 用 `--add-dir` 让 Claude 访问更多文件夹

在多个仓库之间协作时，Boris 通常会在一个仓库里启动 Claude，然后用 `--add-dir`（或 `/add-dir`）让 Claude 同时看到另一个仓库。

- 这不仅会告诉 Claude 另一个仓库的存在，还会**赋予它在该仓库中工作的权限**
- 或者，你也可以在团队的 `settings.json` 里加入 `"additionalDirectories"`，让 Claude Code 启动时总是自动加载这些附加目录

<a href="https://x.com/bcherny/status/2038454359047156203"><img src="assets/boris-30-mar-26/13.png" alt="用于多仓库的 --add-dir" width="50%" /></a>

---

## 14/ 用 `--agent` 给 Claude Code 自定义系统提示词与工具

自定义代理是一个非常强大、但经常被忽略的基础能力。使用方式很简单：先在 `.claude/agents/` 中定义一个新代理，然后运行：

```bash
claude --agent=<your agent's name>
```

- 代理可以拥有受限工具、自定义描述以及特定模型
- 很适合用来构建只读代理、专用审查代理或领域专属工具

<a href="https://x.com/bcherny/status/2038454360418787764"><img src="assets/boris-30-mar-26/14.png" alt="用于自定义系统提示词的 --agent" width="50%" /></a>

---

## 15/ 用 `/voice` 启用语音输入

一个有趣的事实是：Boris 大多数时候不是打字写代码，而是直接对 Claude 说话。

- 在 CLI 中运行 `/voice`，然后按住空格键说话
- 在 Desktop 上点击语音按钮
- 或者在 iOS 设置中启用听写

<a href="https://x.com/bcherny/status/2038454362226467112"><img src="assets/boris-30-mar-26/15.png" alt="用于语音输入的 /voice" width="50%" /></a>

---

## 来源

- [Boris Cherny (@bcherny) on X — March 30, 2026](https://x.com/bcherny/status/2038454336355999749)
