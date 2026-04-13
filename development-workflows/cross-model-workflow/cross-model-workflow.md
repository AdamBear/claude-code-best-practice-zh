# 跨模型（Claude Code + Codex）工作流

基于 [claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice) 和 [codex-cli-best-practice](https://github.com/shanraisshan/codex-cli-best-practice)

## 工作流

```text
+----------------------------------------------------------------------------------+
|                    跨模型 CLAUDE CODE + CODEX 工作流                              |
+----------------------------------------------------------------------------------+
|                                                                                  |
| 步骤 1：规划                                                  Claude Code        |
| 打开 Claude Code 的 plan mode（终端 1）。                     Opus 4.6 / 规划模式 |
| Claude 通过 AskUserQuestion 访谈你。                                              |
| 产出带测试闸门的分阶段计划。                                                      |
| 输出：plans/{feature-name}.md                                                     |
|                                                                                  |
|                                      v                                           |
|                                                                                  |
| 步骤 2：QA 审查                                                Codex CLI         |
| 在另一个终端打开 Codex CLI（终端 2）。                         GPT-5.4           |
| Codex 会结合真实代码库审查计划。                                                 |
| 插入中间阶段（例如 “Phase 2.5”），并使用 “Codex Finding” 标题。                  |
| 它只补充计划，不会重写原有阶段。                                                  |
| 输出：plans/{feature-name}.md（已更新）                                           |
|                                                                                  |
|                                      v                                           |
|                                                                                  |
| 步骤 3：实施                                                  Claude Code        |
| 开启新的 Claude Code 会话（终端 1）。                         Opus 4.6           |
| 你按阶段逐步实现，且每个阶段都带测试闸门。                                        |
|                                                                                  |
|                                      v                                           |
|                                                                                  |
| 步骤 4：验证                                                  Codex CLI         |
| 开启新的 Codex CLI 会话（终端 2）。                           GPT-5.4           |
| Codex 会根据计划验证实现结果。                                                   |
+----------------------------------------------------------------------------------+
```

## 生产环境中的跨模型工作流长什么样

![跨模型工作流](assets/cross-model-workflow.png)

*最后更新：2026-03-06*
