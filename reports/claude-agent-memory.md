# Claude Code：Agent Memory Frontmatter

用于子代理的持久记忆，让 agent 能在跨会话过程中学习、记住并积累知识。

<table width="100%">
<tr>
<td><a href="../">返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 概览

`memory` frontmatter 字段在 **Claude Code v2.1.33**（2026 年 2 月）引入，它为每个子代理提供了独立的、基于 Markdown 的持久知识存储。在此之前，每次 agent 调用都要从零开始。

```yaml
---
name: code-reviewer
description: Reviews code for quality and best practices
tools: Read, Write, Edit, Bash
model: sonnet
memory: user
---

You are a code reviewer. As you review code, update your agent memory with
patterns, conventions, and recurring issues you discover.
```

---

## 记忆作用域

| 作用域 | 存储位置 | 版本控制 | 共享性 | 适用场景 |
|-------|-----------------|-------------------|--------|----------|
| `user` | `~/.claude/agent-memory/<agent-name>/` | 否 | 否 | 跨项目知识（推荐默认值） |
| `project` | `.claude/agent-memory/<agent-name>/` | 是 | 是 | 团队应共享的项目级知识 |
| `local` | `.claude/agent-memory-local/<agent-name>/` | 否（git 忽略） | 否 | 个人专用的项目级知识 |

这些作用域与设置层级相呼应：`~/.claude/settings.json` → `.claude/settings.json` → `.claude/settings.local.json`。

---

## 工作方式

1. **启动时**：会将 `MEMORY.md` 的前 200 行注入到 agent 的系统提示中
2. **工具访问**：会自动启用 `Read`、`Write`、`Edit`，以便 agent 自主管理记忆
3. **执行期间**：agent 可以自由读写自己的记忆目录
4. **整理机制**：如果 `MEMORY.md` 超过 200 行，agent 会把细节迁移到按主题拆分的文件中

```
~/.claude/agent-memory/code-reviewer/     # user 作用域示例
├── MEMORY.md                              # 主文件（前 200 行会被加载）
├── react-patterns.md                      # 按主题拆分的文件
└── security-checklist.md                  # 按主题拆分的文件
```

---

## Agent Memory 与其他记忆系统的区别

| 系统 | 谁来写 | 谁来读 | 作用域 |
|--------|-----------|-----------|-------|
| **CLAUDE.md** | 你手动维护 | 主 Claude + 所有 agent | 项目 |
| **Auto-memory** | 主 Claude 自动写入 | 仅主 Claude | 每项目、每用户 |
| **`/memory` 命令** | 你通过编辑器修改 | 仅主 Claude | 每项目、每用户 |
| **Agent memory** | agent 自己写 | 仅对应的那个 agent | 可配置（user/project/local） |

这些系统是**互补的**。一个 agent 会同时读取 CLAUDE.md（项目上下文）和它自己的记忆（agent 专属知识）。

---

## 实际示例

```yaml
---
name: api-developer
description: Implement API endpoints following team conventions
tools: Read, Write, Edit, Bash
model: sonnet
memory: project
skills:
  - api-conventions
  - error-handling-patterns
---

Implement API endpoints. Follow the conventions from your preloaded skills.
As you work, save architectural decisions and patterns to your memory.
```

这里把 **技能**（启动时加载的静态知识）与 **记忆**（随着时间积累的动态知识）结合起来了。

---

## 建议

- **在提示中明确要求使用记忆**：例如 `"Before starting, review your memory. After completing, update your memory with what you learned."`
- **调用 agent 时要求检查记忆**：例如 `"Review this PR, and check your memory for patterns you've seen before."`
- **选对作用域**：`user` 适合跨项目，`project` 适合团队共享，`local` 适合个人专用

---

## 资料来源

- [Create custom subagents - Claude Code Docs](https://code.claude.com/docs/en/sub-agents)
- [Manage Claude's memory - Claude Code Docs](https://code.claude.com/docs/en/memory)
- [Claude Code v2.1.33 Release Notes](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
