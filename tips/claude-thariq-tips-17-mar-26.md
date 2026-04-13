# 从构建 Claude Code 学到的经验：我们如何使用技能

这是 Thariq（[@trq212](https://x.com/trq212)）于 2026 年 3 月 17 日分享的一份完整指南，介绍 Anthropic 如何在内部使用技能。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 背景

技能已经成为 Claude Code 中最常用的扩展点之一。它们灵活、易于创建，也容易分发。但正因为灵活，什么样的技能才真正有效反而不总是清晰。Thariq 分享了 Anthropic 在内部大规模使用技能后总结出的经验，他们目前活跃使用的技能已经达到数百个。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/1.png" alt="Thariq 介绍推文" width="50%" /></a>

---

## 什么是技能？

一个常见误解是，技能“只是 Markdown 文件”。但其实最有意思的部分在于，它们本质上是**文件夹**，里面可以包含脚本、资源、数据等各种内容，也就是代理能够发现、探索并操作的东西。技能还有很多配置选项，其中包括注册动态钩子。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/2.png" alt="什么是技能？" width="50%" /></a>

---

## 技能的类型

在对所有技能做分类之后，团队发现它们大致会聚集成 9 个反复出现的类别。最好的技能通常能清晰地落在其中一种；最让人困惑的技能往往横跨多个类别。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/3.png" alt="技能类型总览" width="50%" /></a>

---

### 1/ 库与 API 参考

这类技能用来说明如何正确使用某个库、CLI 或 SDK。它们既可以面向内部库，也可以面向 Claude Code 有时不太擅长的常见库。通常还会附带一组参考代码片段，以及一份写脚本时需要避开的坑点清单。

**示例：** billing-lib、internal-platform-cli、frontend-design

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/4.png" alt="库与 API 参考" width="50%" /></a>

---

### 2/ 产品验证

这类技能描述如何测试或验证你的代码是否正常工作。它们常常会与 Playwright、tmux 等外部工具配合使用。验证类技能对于确保 Claude 输出正确非常有用，甚至值得让一位工程师专门花一周时间把这类技能打磨到优秀。

**示例：** signup-flow-driver、checkout-verifier、tmux-cli-driver

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/5.png" alt="产品验证" width="50%" /></a>

---

### 3/ 数据获取与分析

这类技能连接你的数据和监控系统。它们可能包括用于带凭证拉取数据的库、特定 dashboard ID，以及一些常见分析工作流或数据获取方式的说明。

**示例：** funnel-query、cohort-compare、grafana

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/6.png" alt="数据获取与分析" width="50%" /></a>

---

### 4/ 业务流程与团队自动化

这类技能把重复性工作流压缩成一条命令。通常它们的说明相对简单，但可能会依赖其他技能或 MCP。把之前的执行结果保存进日志文件，有助于模型保持一致性，并反思过去执行工作流时发生了什么。

**示例：** standup-post、create-<ticket-system>-ticket、weekly-recap

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/7.png" alt="业务流程与团队自动化" width="50%" /></a>

---

### 5/ 代码脚手架与模板

这类技能会为代码库中特定类型的功能生成框架样板。它们常会配合可组合的脚本一起使用。当你的脚手架里包含很多无法完全靠代码表达的自然语言要求时，这类技能尤其有价值。

**示例：** new-<framework>-workflow、new-migration、create-app

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/8.png" alt="代码脚手架与模板" width="50%" /></a>

---

### 6/ 代码质量与审查

这类技能用于在组织内部落实代码质量标准，并辅助代码审查。为了最大程度提高稳健性，它们可以包含确定性的脚本或工具。你也可以考虑通过钩子或 GitHub Action 自动运行这些技能。

**示例：** adversarial-review、code-style、testing-practices

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/10.png" alt="代码质量与审查" width="50%" /></a>

---

### 7/ CI/CD 与部署

这类技能帮助你在代码库内部拉取、推送和部署代码。它们可能会引用其他技能来收集所需数据。

**示例：** babysit-pr、deploy-<service>、cherry-pick-prod

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/11.png" alt="CI/CD 与部署" width="50%" /></a>

---

### 8/ Runbook

这类技能会从某个症状出发（例如 Slack 讨论串、告警或错误特征），带着你走完一个多工具排查过程，并输出结构化报告。

**示例：** <service>-debugging、oncall-runner、log-correlator

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/12.png" alt="Runbook" width="50%" /></a>

---

### 9/ 基础设施运维

这类技能执行日常维护和运维流程，其中有些步骤可能具有破坏性，因此非常适合加上防护栏。它们能帮助工程师更容易遵循关键操作中的最佳实践。

**示例：** <resource>-orphans、dependency-management、cost-investigation

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/13.png" alt="基础设施运维" width="50%" /></a>

---

## 编写技能的建议

这里总结了 9 条编写高质量技能的最佳实践，以及关于分发和衡量效果的建议。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/14.png" alt="编写技能的建议总览" width="50%" /></a>

---

### 建议 1：不要写显而易见的内容

Claude Code 已经很了解你的代码库，Claude 也已经懂大量编程知识，并自带很多默认倾向。如果你发布的技能主要是知识型内容，那么重点应该放在那些能把 Claude 从默认思路中“推开”的信息上。前端设计技能就是很好的例子，它是在和客户一起反复打磨 Claude 的设计品味后形成的，明确避开了像 Inter 字体和紫色渐变这样的经典套路。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/15.png" alt="不要写显而易见的内容" width="50%" /></a>

---

### 建议 2：一定要有 Gotchas 部分

任何技能里信号密度最高的内容，往往就是 Gotchas 部分。这些章节应该从 Claude 在实际使用技能时反复遇到的失败点中积累出来。理想状态下，你会持续更新技能，把这些 gotcha 不断收集进去。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/16.png" alt="编写 Gotchas 部分" width="50%" /></a>

---

### 建议 3：利用文件系统与渐进披露

技能是一个文件夹，而不只是一个 Markdown 文件。你应该把整个文件系统当作一种上下文工程和渐进披露机制。告诉 Claude 这个技能目录里有哪些文件，它会在合适的时候去读取它们。最简单的方式是指向其他 Markdown 文件，例如把详细函数签名和用法示例拆到 `references/api.md` 中。你也可以放入 references、scripts、examples 等目录。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/17.png" alt="渐进披露" width="50%" /></a>

---

### 建议 4：不要过度“轨道化” Claude

Claude 通常会尽量遵守你的指令，而技能又是高度可复用的，因此你需要小心不要把它限制得过于具体。应该给 Claude 必要的信息，但同时保留它根据情境调整的灵活性。与其写成硬邦邦的逐步指令，不如交代目标和约束。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/18.png" alt="不要过度轨道化 Claude" width="50%" /></a>

---

### 建议 5：把初始化过程想清楚

有些技能需要先从用户那里拿到一些上下文信息。一个很好的模式，是把这些初始化信息存到技能目录里的 `config.json`。如果配置尚未完成，代理就可以再向用户提问。你也可以指示 Claude 使用 AskUserQuestion 工具，以结构化、多选题的形式发问。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/19.png" alt="想清楚初始化流程" width="50%" /></a>

---

### 建议 6：Description 字段是写给模型看的

当 Claude Code 启动一个会话时，它会构建一份所有可用技能的列表，并附带 description。Claude 会扫这份列表，判断“这个请求有没有对应技能”。所以 description 不是摘要，而是说明**在什么情况下应该触发这个技能**。这段话应该写给模型，而不是写给人看。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/20.png" alt="Description 等于触发条件" width="50%" /></a>

---

### 建议 7：记忆与数据存储

有些技能可以通过存储数据，形成某种“记忆”能力。你可以把数据存成最简单的追加文本日志、JSON 文件，甚至复杂到 SQLite 数据库。需要注意的是，技能目录中的数据在升级技能时可能被删除，因此更稳定的做法是使用 `${CLAUDE_PLUGIN_DATA}` 作为每个插件独立的数据目录。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/21.png" alt="记忆与数据存储" width="50%" /></a>

---

### 建议 8：保存脚本，并让 Claude 生成代码

你能给 Claude 的最强工具之一，其实就是代码本身。提供脚本和库之后，Claude 的轮次可以更多花在组合能力、判断下一步做什么上，而不是反复重建样板。随后 Claude 还可以按需临时生成脚本，把这些能力再组合起来，完成更高级的分析。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/22.png" alt="保存脚本并生成代码" width="50%" /></a>

---

### 建议 9：按需激活的钩子

技能可以包含钩子，但这些钩子只会在技能被调用时激活，并持续到当前会话结束。对于那些你不想一直开启、但某些场景下非常有用的强意见钩子，这种做法特别合适。

**示例：**
- `/careful`：通过 Bash 的 PreToolUse matcher 阻止 `rm -rf`、`DROP TABLE`、force-push、`kubectl delete`
- `/freeze`：阻止所有不在特定目录内的 Edit 或 Write

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/23.png" alt="按需激活的钩子" width="50%" /></a>

---

## 分发技能

把技能分享给团队主要有两种方式：

- **直接提交进仓库**（放在 `.claude/skills` 下）：适合跨仓库数量相对较少的小团队
- **做成插件**，并建立一个 Claude Code Plugin marketplace，供用户上传和安装插件

每一个被提交进仓库的技能，都会额外占用模型的一点上下文。随着规模扩大，内部插件市场能让团队分发技能，同时把安装决策交还给具体使用者。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/24.png" alt="分发技能" width="50%" /></a>

---

## 管理 Marketplace

并不存在一个中央团队来决定哪些技能应该进入 marketplace。更好的做法是让有用的技能自然浮现：先上传到 GitHub 中的一个 sandbox 目录，再通过 Slack 或其他渠道分享给大家。一旦某个技能获得了足够牵引力（由技能作者自己判断），就可以发起一个 PR，把它正式移入 marketplace。在正式发布前做好策展非常重要，这样可以避免出现大量冗余技能。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/25.png" alt="管理 Marketplace" width="50%" /></a>

---

## 组合技能

你可能会需要让技能之间互相依赖。例如，一个文件上传技能负责上传文件，另一个 CSV 生成技能负责先生成 CSV 再上传。此类依赖管理目前还不是 marketplace 或技能系统的原生能力，但你完全可以在说明里直接引用其他技能的名字，只要它们已安装，模型就会调用它们。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/26.png" alt="组合技能" width="50%" /></a>

---

## 衡量技能效果

如果你想了解某个技能实际表现如何，可以使用一个 PreToolUse 钩子，把技能使用情况记录到公司内部。这样你就能找出哪些技能很受欢迎，哪些技能相比预期触发得太少。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/27.png" alt="衡量技能效果" width="50%" /></a>

---

## 总结

技能对代理来说是非常强大、非常灵活的工具，但这个领域仍然很早期，大家都还在摸索最佳实践。与其把这份内容看作一套终极指南，不如把它当作一袋已经被验证有效的经验。真正理解技能的最好方式，就是立刻开始、亲自实验、看看什么对你有效。Anthropic 的很多技能最初只是几行说明和一个 gotcha，后来之所以越来越好，是因为人们不断往里补充新边界情况。

<a href="https://x.com/trq212/status/2033949937936085378"><img src="assets/thariq-17-mar-26/28.png" alt="总结" width="50%" /></a>

---

## 来源

- [Thariq (@trq212) on X — March 17, 2026](https://x.com/trq212/status/2033949937936085378)
- [Skilljar — Agent Skills course](https://code.claude.com/docs/en/skills)
- [Skill Creator](https://code.claude.com/docs/en/skills)
