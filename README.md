# claude-code-best-practice

从 vibe coding 走向代理式工程，把 Claude Code 真正用起来。

![使用 Claude Code 持续更新](https://img.shields.io/badge/updated_with_Claude_Code-v2.1.101%20(Apr%2011%2C%202026%206%3A17%20PM%20PKT)-white?style=flat&labelColor=555)

这是一个围绕 Claude Code 最佳实践整理的中文仓库，聚焦三类内容：

- 概念：commands、agents、skills、hooks、memory、MCP、settings 等核心构件
- 实战：工作流编排、Agent Teams、RPI、定时任务、项目级 `CLAUDE.md` 设计
- 资料：技巧贴、视频整理、专题报告，以及与其他工作流仓库的横向对比

## 你会在这里找到什么

| 模块 | 说明 |
|---|---|
| [best-practice](best-practice/) | 各能力点的最佳实践说明 |
| [implementation](implementation/) | 对应能力在项目中的落地示例 |
| [tutorial](tutorial/) | 从入门到进阶的教学材料 |
| [orchestration-workflow](orchestration-workflow/orchestration-workflow.md) | 命令、代理、技能如何串成完整工作流 |
| [agent-teams](agent-teams/) | 多代理团队协作示例 |
| [development-workflows](development-workflows/) | 其他热门工作流仓库的横向整理 |
| [tips](tips/) | 社区与官方成员分享的使用技巧 |
| [videos](videos/) | 访谈、播客与讲解视频中文整理 |
| [reports](reports/) | 深入专题报告与图表 |
| [changelog](changelog/) | 跟踪文档和资料更新历史 |

## 核心概念

| 概念 | 位置 | 作用 |
|---|---|---|
| [Subagents](https://code.claude.com/docs/en/sub-agents) | `.claude/agents/<name>.md` | 独立上下文中的专门角色，可配置工具、模型和权限 |
| [Commands](https://code.claude.com/docs/en/slash-commands) | `.claude/commands/<name>.md` | 作为入口进行编排、提问和流程分发 |
| [Skills](https://code.claude.com/docs/en/skills) | `.claude/skills/<name>/SKILL.md` | 可复用的知识包或执行套路 |
| [Hooks](https://code.claude.com/docs/en/hooks) | `.claude/hooks/` | 在生命周期节点触发脚本、HTTP、提示词或代理处理 |
| [MCP Servers](https://code.claude.com/docs/en/mcp) | `.claude/settings.json`、`.mcp.json` | 连接数据库、浏览器、外部 API 与各类工具 |
| [Settings](https://code.claude.com/docs/en/settings) | `.claude/settings.json` | 模型、权限、沙箱、界面与团队设置 |
| [Memory](https://code.claude.com/docs/en/memory) | `CLAUDE.md`、`.claude/rules/` | 持久项目上下文与路径级规则 |
| [CLI 启动参数](https://code.claude.com/docs/en/cli-reference) | `claude [flags]` | 控制模型、交互模式、权限模式与环境行为 |

## 推荐先看

### 1. 编排工作流

先看 [orchestration-workflow/orchestration-workflow.md](orchestration-workflow/orchestration-workflow.md)。

这里展示了最关键的一条链路：

`Command -> Agent -> Skill`

配套资源：

- [结构说明](orchestration-workflow/orchestration-workflow.md)
- [工作流图](orchestration-workflow/orchestration-workflow.svg)
- [实际输出示例](orchestration-workflow/output.md)

### 2. 项目知识与规则

建议结合以下内容一起看：

- [claude-memory.md](best-practice/claude-memory.md)
- [claude-settings.md](best-practice/claude-settings.md)
- [claude-subagents.md](best-practice/claude-subagents.md)
- [claude-commands.md](best-practice/claude-commands.md)
- [claude-skills.md](best-practice/claude-skills.md)

### 3. 多代理与团队化执行

- [Agent Teams](agent-teams/)
- [Claude Agent Teams 实现](implementation/claude-agent-teams-implementation.md)
- [RPI 工作流](development-workflows/rpi/rpi-workflow.md)

## 工作流参考

这一部分收录了其他有代表性的开源工作流项目，方便横向比较：

| 项目 | 特色 |
|---|---|
| [Everything Claude Code](https://github.com/affaan-m/everything-claude-code) | 大规模规则集、AgentShield、跨语言实践 |
| [Superpowers](https://github.com/obra/superpowers) | TDD-first、计划优先、严格约束执行 |
| [Spec Kit](https://github.com/github/spec-kit) | spec-driven 工作方式与命令模板 |
| [gstack](https://github.com/garrytan/gstack) | 多角色审查、并行执行、层级化技能 |
| [Get Shit Done](https://github.com/gsd-build/get-shit-done) | 波次执行、超长上下文、批量命令 |
| [BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD) | 完整 SDLC 与技能化角色 |
| [OpenSpec](https://github.com/Fission-AI/OpenSpec) | brownfield 与 delta spec 流程 |
| [oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) | 团队编排、tmux worker、计划驱动执行 |
| [HumanLayer](https://github.com/humanlayer/humanlayer) | 大仓库协作、RPI、上下文工程 |

配套目录：

- [development-workflows/cross-model-workflow](development-workflows/cross-model-workflow/cross-model-workflow.md)
- [development-workflows/rpi](development-workflows/rpi/rpi-workflow.md)

## 技巧与经验

优先阅读这些内容：

- [How I use Claude Code - 13 tips](tips/claude-boris-13-tips-03-jan-26.md)
- [10 tips for using Claude Code from the team](tips/claude-boris-10-tips-01-feb-26.md)
- [12 ways how people are customizing their claudes](tips/claude-boris-12-tips-12-feb-26.md)
- [Lessons from Building Claude Code: How We Use Skills](tips/claude-thariq-tips-17-mar-26.md)
- [15 Hidden & Under-Utilized Features in Claude Code](tips/claude-boris-15-tips-30-mar-26.md)

常见经验总结：

- 复杂任务先进入 plan mode
- 让 Claude 自己运行终端并查看日志
- 用 `/code-review` 做回归前检查
- 使用 worktree 并行推进多个分支任务
- 长会话中及时 `/compact`
- 通过小 PR 和频繁提交降低返工成本

## 视频整理

| 标题 | 来源 | YouTube |
|---|---|---|
| [我们在 Research-Plan-Implement 上犯过的所有错误](videos/claude-dex-mlops-community-24-mar-26.md) | MLOps Community | [YouTube](https://youtu.be/YwZR6tc7qYg) |
| [与 Boris Cherny 一起拆解 Claude Code](videos/claude-boris-pragmatic-engineer-04-mar-26.md) | The Pragmatic Engineer | [YouTube](https://youtu.be/julbw1JuAz0) |
| [Claude Code 负责人：编程被解决之后会发生什么](videos/claude-boris-lennys-podcast-19-feb-26.md) | Lenny's Podcast | [YouTube](https://youtu.be/We7BZVKbCVw) |
| [与创建者 Boris Cherny 深入聊 Claude Code](videos/claude-boris-y-combinator-17-feb-26.md) | Y Combinator | [YouTube](https://youtu.be/PQU9o_5rHC4) |
| [Claude Code 团队公开的内部经验](videos/claude-cat-every-29-oct-25.md) | Every | [YouTube](https://youtu.be/IDSAMqip6ms) |

## 专题报告

推荐从这些报告开始：

- [claude-agent-sdk-vs-cli-system-prompts](reports/claude-agent-sdk-vs-cli-system-prompts.md)
- [claude-in-chrome-v-chrome-devtools-mcp](reports/claude-in-chrome-v-chrome-devtools-mcp.md)
- [claude-global-vs-project-settings](reports/claude-global-vs-project-settings.md)
- [claude-advanced-tool-use](reports/claude-advanced-tool-use.md)
- [llm-day-to-day-degradation](reports/llm-day-to-day-degradation.md)

## 如何使用这个仓库

```text
1. 先理解 commands、agents、skills、hooks 各自解决什么问题。
2. 再跑一两个示例工作流，例如 /weather-orchestrator 或 Agent Teams。
3. 回到你自己的项目，让 Claude 参考本仓库挑选最值得引入的做法。
```

## 外部社区

- Reddit: [r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/)、[r/ClaudeCode](https://www.reddit.com/r/ClaudeCode/)、[r/Anthropic](https://www.reddit.com/r/Anthropic/)
- X: [Claude](https://x.com/claudeai)、[Anthropic](https://x.com/AnthropicAI)、[Boris](https://x.com/bcherny)、[Thariq](https://x.com/trq212)
- YouTube: [Anthropic](https://www.youtube.com/@anthropic-ai)、[Lenny's Podcast](https://www.youtube.com/@LennysPodcast)、[Y Combinator](https://www.youtube.com/@ycombinator)

## 相关仓库

- [claude-code-hooks](https://github.com/shanraisshan/claude-code-hooks)
- [codex-cli-best-practice](https://github.com/shanraisshan/codex-cli-best-practice)
- [codex-cli-hooks](https://github.com/shanraisshan/codex-cli-hooks)

## 说明

本仓库以中文整理为主，但以下内容会保留英文原样：

- 路径、命令、代码块、配置键、环境变量
- URL、仓库名、产品名、模型名
- 官方文档中的关键术语，例如 Claude Code、MCP、SDK、Hooks、Skills
