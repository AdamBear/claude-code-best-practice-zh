# 验证清单：子代理报告

规则会随着时间累积。每次运行 workflow-changelog 时，都必须按指定深度执行全部规则。当某种新漂移被发现，而现有规则本应捕获却因不存在或过浅而漏掉时，就把新规则补到这里。

## 深度等级

| 深度 | 含义 | 示例 |
|-------|------|------|
| `exists` | 检查章节、表格或文件是否存在 | “报告里是否有 Memory Scopes 表？” |
| `presence-check` | 检查具体项是否存在或缺失 | “Frontmatter Fields 表里是否有 `color` 字段？” |
| `content-match` | 将实际值与来源逐字比对 | “`model` 字段说明是否与官方文档一致？” |
| `field-level` | 验证每个单独字段都已覆盖 | “官方文档中的每个 frontmatter 字段是否都出现在表格里？” |
| `cross-file` | 同一个值在多个文件中必须一致 | “CLAUDE.md 的 agent 部分是否与报告中的字段列表一致？” |

---

## 1. Frontmatter 字段表

用于按官方文档核对 Frontmatter Fields 表的规则。

| # | 类别 | 检查项 | 深度 | 对照来源 | 添加时间 | 来源说明 |
|---|------|--------|------|----------|----------|----------|
| 1A | 字段完整性 | 对官方文档中的每个 agent frontmatter 字段，验证它是否出现在报告的 Frontmatter Fields 表中 | field-level | sub-agents reference 页面 | 2026-02-28 | 初始清单，确保不会漏掉新字段 |
| 1B | 字段类型 | 对表中的每个字段，验证 Type 列是否与官方文档一致 | content-match | sub-agents reference 页面 | 2026-02-28 | 初始清单，类型错误会误导用户 |
| 1C | 必填状态 | 对每个字段，验证 Required 列是否与官方文档一致 | content-match | sub-agents reference 页面 | 2026-02-28 | 初始清单，必填状态错误会导致 agent 配置失效 |
| 1D | 字段说明 | 对每个字段，验证 Description 列是否准确反映官方文档行为 | content-match | sub-agents reference 页面 | 2026-02-28 | 初始清单，过时说明会误导用户 |

---

## 2. 记忆作用域

用于核对 Memory Scopes 表的规则。

| # | 类别 | 检查项 | 深度 | 对照来源 | 添加时间 | 来源说明 |
|---|------|--------|------|----------|----------|----------|
| 2A | 作用域完整性 | 验证官方文档中的所有 memory scope 是否都出现在 Memory Scopes 表中 | field-level | sub-agents reference 页面 | 2026-02-28 | 初始清单，后续可能新增作用域 |
| 2B | 存储位置 | 对每个作用域，验证 Storage Location 列是否与官方文档一致 | content-match | sub-agents reference 页面 | 2026-02-28 | 初始清单，路径错误会导致数据丢失 |

---

## 3. 示例

用于验证示例准确性的规则。

| # | 类别 | 检查项 | 深度 | 对照来源 | 添加时间 | 来源说明 |
|---|------|--------|------|----------|----------|----------|
| 3A | 最小示例 | 验证最小示例只使用必填字段，且语法有效 | content-match | sub-agents reference 页面 | 2026-02-28 | 初始清单，最小示例应保持最小化 |
| 3B | 全功能示例 | 验证全功能示例展示了所有可用 frontmatter 字段 | field-level | sub-agents reference 页面 | 2026-02-28 | 初始清单，完整示例必须覆盖全部字段 |

---

## 4. 作用域与优先级

用于验证作用域和优先级信息的规则。

| # | 类别 | 检查项 | 深度 | 对照来源 | 添加时间 | 来源说明 |
|---|------|--------|------|----------|----------|----------|
| 4A | 优先级顺序 | 验证 Scope and Priority 表是否按正确优先级顺序列出所有 agent 位置 | content-match | sub-agents reference 页面 + CLI reference 页面 | 2026-02-28 | 初始清单，优先级顺序错误会导致解析问题 |
| 4B | 调用方式 | 验证调用方式表是否列出 CLI reference 与 sub-agents 文档中的所有调用方式，包括 `--agent`（单数）、`--agents`（复数）、`/agents`、`claude agents`、Agent 工具和 agent 恢复 | field-level | CLI reference 页面 + sub-agents reference 页面 | 2026-03-07 | 调用方式表缺少 `--agent` CLI 标志，它是以特定 agent 运行 Claude 的独立入口 |

---

## 5. 跨文件一致性

用于验证报告与仓库其他文件之间一致性的规则。

| # | 类别 | 检查项 | 深度 | 对照来源 | 添加时间 | 来源说明 |
|---|------|--------|------|----------|----------|----------|
| 5A | CLAUDE.md 同步 | 验证 CLAUDE.md 的 Subagent Definition Structure 章节是否列出与报告 Frontmatter Fields 表相同的字段 | cross-file | CLAUDE.md vs 报告 | 2026-02-28 | 初始清单，CLAUDE.md 可能与报告漂移 |

---

## 6. 流程

关于工作流验证流程本身的元规则。

| # | 类别 | 检查项 | 深度 | 对照来源 | 添加时间 | 来源说明 |
|---|------|--------|------|----------|----------|----------|
| 6A | 来源可信度守卫 | 只有在官方来源确认后才可标记为漂移（sub-agents reference 页、CLI reference 页、GitHub changelog）。第三方博客只能作为线索，最终仍须回官方文档验证 | content-match | 仅官方文档 | 2026-02-28 | 从 hooks 工作流沿用，避免第三方博客带来误报 |

---

## 7. Agent 表格

用于核对 Official Claude Agents 与 Agents in This Repository 两张表的规则。

| # | 类别 | 检查项 | 深度 | 对照来源 | 添加时间 | 来源说明 |
|---|------|--------|------|----------|----------|----------|
| 7A | 内置 Agent 完整性 | 验证 “Official Claude Agents” 表是否列出全部内置 agent 类型，以及正确的 model、tools 和 description | field-level | sub-agents reference 页面 + changelog | 2026-02-28 | 报告最初只有 5 个中的 3 个内置 agent，缺少 `claude-code-guide` 和 `statusline-setup` |
| 7B | 仓库 Agent 完整性 | 扫描 `.claude/agents/**/*.md`，验证每个 agent 文件都出现在 “Agents in This Repository” 表中，且 model、color、tools、skills、memory 列正确 | field-level | `.claude/agents/**/*.md` 的 frontmatter | 2026-02-28 | 仓库内 agent 原本是手工维护的，新 agent 加入后没有同步到报告 |
| 7C | 仓库 Agent 链接 | 验证 “Agents in This Repository” 表中的每个 agent 名称都带有可点击链接，并能解析到正确的 `.md` 文件 | exists | 从 `best-practice/` 解析后的文件路径 | 2026-02-28 | agent 名称后来被改成可点击，文件移动后必须持续验证链接有效 |

---

## 8. 超链接

用于验证报告中所有链接是否有效的规则。

| # | 类别 | 检查项 | 深度 | 对照来源 | 添加时间 | 来源说明 |
|---|------|--------|------|----------|----------|----------|
| 8A | 本地文件链接 | 验证所有相对文件链接（如 `../.claude/agents/weather-agent.md`）都能解析到真实存在的文件 | exists | 本地文件系统 | 2026-02-28 | 文件从 `reports/` 移到 `best-practice/` 时曾导致相对链接失效，后续必须防止再次发生 |
| 8B | 外部 URL 链接 | 验证所有外部 URL（如 `https://code.claude.com/docs/en/sub-agents`）都返回有效页面 | exists | HTTP 响应 | 2026-02-28 | 外部文档页可能改版或删除，每次运行都要验证 |
| 8C | 跨文件引用链接 | 验证指向其他报告文件的链接（如 `../reports/claude-agent-memory.md`）都能解析到真实存在的文件 | exists | 本地文件系统 | 2026-02-28 | 报告可能被移动或重命名，交叉引用必须保持同步 |
