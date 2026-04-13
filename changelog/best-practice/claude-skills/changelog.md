# 技能报告变更历史

**状态图例：**

| 状态 | 含义 |
|--------|---------|
| `COMPLETE (reason)` | 已执行并成功解决 |
| `INVALID (reason)` | 结论不正确、不适用，或当前状态属预期 |
| `ON HOLD (reason)` | 已暂缓处理，等待外部依赖或用户决定 |

---

## [2026-03-13 04:22 PM PKT] Claude Code v2.1.74

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | MED | 多余的内置技能 | 本地报告里有 `keybindings-help`，但官方文档的 bundled skills 列表中没有，需要调查是移除还是保留 | COMPLETE（已从 bundled skills 表移除，它是本仓库的本地自定义技能，不是官方内置技能；`/keybindings` 是 CLI 内置命令） |

---

## [2026-03-15 12:49 PM PKT] Claude Code v2.1.76

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | LOW | 字段准确性 | 本地报告里 `name` 字段的 Required 列写成 “Recommended”，而官方文档现在标为 “No”（可选），需要同步 | COMPLETE（已将 `name` 的 Required 从 “Recommended” 改为 “No”，以匹配官方文档） |

---

## [2026-03-17 12:42 PM PKT] Claude Code v2.1.77

未发现漂移，frontmatter 字段（10）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-03-18 11:38 PM PKT] Claude Code v2.1.78

未发现漂移，frontmatter 字段（10）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-03-19 11:54 AM PKT] Claude Code v2.1.79

未发现漂移，frontmatter 字段（10）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-03-20 08:32 AM PKT] Claude Code v2.1.80

未发现漂移，frontmatter 字段（10）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-03-21 09:07 PM PKT] Claude Code v2.1.81

未发现漂移，frontmatter 字段（11）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-03-23 09:48 PM PKT] Claude Code v2.1.81

未发现漂移，frontmatter 字段（11）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-03-25 08:06 PM PKT] Claude Code v2.1.83

未发现漂移，frontmatter 字段（11）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-03-26 12:59 PM PKT] Claude Code v2.1.84

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 在 frontmatter 表中加入 `shell` 字段，接受 `bash`（默认）或 `powershell`，用于控制技能内容中 `!command` 代码块所使用的 shell | COMPLETE（已添加到 frontmatter 表，计数从 11 更新为 12） |

---

## [2026-03-27 06:25 PM PKT] Claude Code v2.1.85

| # | 优先级 | 类型 | 操作 | 状态 |
|---|----------|------|--------|--------|
| 1 | HIGH | 新字段 | 在 frontmatter 表中加入 `paths` 字段，接受 glob 模式（字符串或 YAML 列表），用于限制技能何时自动激活 | COMPLETE（已添加到 frontmatter 表，计数从 12 更新为 13） |

---

## [2026-03-28 05:59 PM PKT] Claude Code v2.1.86

未发现漂移，frontmatter 字段（13）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-03-31 06:51 PM PKT] Claude Code v2.1.88

未发现漂移，frontmatter 字段（13）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-04-01 12:27 PM PKT] Claude Code v2.1.89

未发现漂移，frontmatter 字段（13）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-04-02 09:11 PM PKT] Claude Code v2.1.90

未发现漂移，frontmatter 字段（13）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-04-03 08:28 PM PKT] Claude Code v2.1.91

未发现漂移，frontmatter 字段（13）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-04-04 10:38 PM PKT] Claude Code v2.1.92

未发现漂移，frontmatter 字段（13）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-04-08 09:33 PM PKT] Claude Code v2.1.96

未发现漂移，frontmatter 字段（13）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-04-09 11:30 PM PKT] Claude Code v2.1.97

未发现漂移，frontmatter 字段（13）与 bundled skills（5）已与官方文档完全同步。

---

## [2026-04-11 06:08 PM PKT] Claude Code v2.1.101

未发现漂移，frontmatter 字段（13）与 bundled skills（5）已与官方文档完全同步。
