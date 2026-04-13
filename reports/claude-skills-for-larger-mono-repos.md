# 大型 Monorepo 中 Claude 技能发现机制解析

当你在 monorepo 中使用 Claude Code 时，理解技能是如何被发现、以及如何加载进上下文，对高效组织项目专属能力非常关键。

<table width="100%">
<tr>
<td><a href="../">返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

## 与 CLAUDE.md 的一个重要区别

**技能的加载行为和 CLAUDE.md 不一样。** CLAUDE.md 会沿目录树**向上**查找祖先目录，而技能采用的是另一套发现机制，更关注项目内部嵌套目录中的技能位置。

## 技能是如何被发现的

### 1. 标准技能位置

技能会按作用域从以下固定位置加载：

| 位置 | 路径 | 作用范围 |
|----------|------|------------|
| Enterprise | Managed settings | 组织内所有用户 |
| Personal | `~/.claude/skills/<skill-name>/SKILL.md` | 你的所有项目 |
| Project | `.claude/skills/<skill-name>/SKILL.md` | 仅当前项目 |
| Plugin | `<plugin>/skills/<skill-name>/SKILL.md` | 该 plugin 启用的位置 |

### 2. 从嵌套目录自动发现

当你处理子目录中的文件时，Claude Code 还会自动从嵌套的 `.claude/skills/` 目录里发现技能。比如，当你编辑 `packages/frontend/` 下的文件时，Claude Code 也会去查找 `packages/frontend/.claude/skills/`。

这对 monorepo 很有用，因为不同 package 可以拥有各自的技能。

## Monorepo 结构示例

下面是一个典型的多 package monorepo：

```
/mymonorepo/
├── .claude/
│   └── skills/
│       └── shared-conventions/SKILL.md    # 项目级技能
├── packages/
│   ├── frontend/
│   │   ├── .claude/
│   │   │   └── skills/
│   │   │       └── react-patterns/SKILL.md  # 前端专属技能
│   │   └── src/
│   │       └── App.tsx
│   ├── backend/
│   │   ├── .claude/
│   │   │   └── skills/
│   │   │       └── api-design/SKILL.md      # 后端专属技能
│   │   └── src/
│   └── shared/
│       ├── .claude/
│       │   └── skills/
│       │       └── utils-patterns/SKILL.md  # 共享工具技能
│       └── src/
```

## 场景 1：刚在仓库根目录启动 Claude（还没编辑任何文件）

当你在 `/mymonorepo/` 下运行 Claude Code，并且还没让它处理任何文件时：

```bash
cd /mymonorepo
claude
# 刚启动，还没有编辑任何文件
```

| 技能 | 是否进入上下文？ | 原因 |
|-------|-------------|--------|
| `shared-conventions` | **是** | 位于根目录 `.claude/skills/` 中的项目级技能 |
| `react-patterns` | **否** | 还没处理 `packages/frontend/` 下的文件，因此不会被发现 |
| `api-design` | **否** | 还没处理 `packages/backend/` 下的文件，因此不会被发现 |
| `utils-patterns` | **否** | 还没处理 `packages/shared/` 下的文件，因此不会被发现 |

## 场景 2：处理某个 package 下的文件之后

如果你让 Claude 去编辑 `packages/frontend/src/App.tsx`：

| 技能 | 是否进入上下文？ | 原因 |
|-------|-------------|--------|
| `shared-conventions` | **是** | 位于根目录 `.claude/skills/` 中的项目级技能 |
| `react-patterns` | **是** | 在处理 `packages/frontend/` 文件时被自动发现 |
| `api-design` | **否** | 还没处理 `packages/backend/` 下的文件 |
| `utils-patterns` | **否** | 还没处理 `packages/shared/` 下的文件 |

**关键点**：嵌套技能是在你处理对应目录文件时，才会**按需发现**的。它们不会在会话启动时预加载。

## 关键行为：描述 vs 完整内容

技能描述会被加载进上下文，让 Claude 知道有哪些技能可用；但**完整技能内容只有在真正调用时才会加载**。这是一个重要优化：

- **Descriptions**：始终会进入上下文（受字符预算限制）
- **Full content**：只有在技能被调用时才按需加载

> 注意：预加载了技能的子代理行为不同，完整技能内容会在子代理启动时直接注入。

## 优先级顺序（当技能同名时）

如果不同层级存在同名技能，优先级更高的位置会胜出：

| 优先级 | 位置 | 作用域 |
|----------|----------|-------|
| 1（最高） | Enterprise | 全组织 |
| 2 | Personal（`~/.claude/skills/`） | 你的所有项目 |
| 3（最低） | Project（`.claude/skills/`） | 当前项目 |

Plugin 技能会使用 `plugin-name:skill-name` 命名空间，因此不会与其他层级冲突。

## 为什么这种设计适合 Monorepo

- **按 package 隔离技能**：在 `packages/frontend/` 工作的前端开发者，只会获得前端相关技能，而不会让后端技能污染上下文。
- **自动发现减少配置负担**：不用显式注册 package 级技能，只要开始处理对应目录的文件，就会自动发现。
- **上下文更节省**：初始只加载技能描述，嵌套技能也按需发现。
- **团队可各自维护技能**：每个 package 团队都能维护自己的领域技能，而不必和其他团队集中协调。

## 字符预算注意事项

技能描述会在字符预算范围内加载进上下文（默认 15,000 字符）。如果 monorepo 中 package 和技能很多，就可能碰到这个上限。

- 运行 `/context`，查看是否有技能因超出预算而被排除的警告
- 通过设置环境变量 `SLASH_COMMAND_TOOL_CHAR_BUDGET` 来提高上限

## 最佳实践

1. **把共享工作流放在根目录 `.claude/skills/`**
   适合仓库级约定、提交工作流和通用模式。

2. **把 package 专属技能放在各 package 的 `.claude/skills/`**
   适合框架专属模式、组件约定、某个 package 独有的测试工具。

3. **对高风险技能使用 `disable-model-invocation: true`**
   例如部署类或破坏性技能，应强制要求用户显式触发。

4. **保持技能描述简洁**
   描述始终会进入上下文（直到字符预算上限），太长的描述会浪费上下文空间。

5. **在技能命名中做命名空间区分**
   可以考虑带上 package 前缀，例如 `frontend-review`、`backend-deploy`，避免歧义。

## 对比：Skills 与 CLAUDE.md 的加载方式

| 行为 | CLAUDE.md | Skills |
|----------|-----------|--------|
| 祖先加载（沿目录树向上） | 是 | 否 |
| 嵌套/子目录发现（沿目录树向下） | 是（惰性） | 是（自动发现） |
| 全局位置 | `~/.claude/CLAUDE.md` | `~/.claude/skills/` |
| 项目位置 | `.claude/` 或仓库根目录 | `.claude/skills/` |
| 内容加载方式 | 完整内容 | 仅描述（调用时再加载完整内容） |

---

## 资料来源

- [Claude Code Documentation - Extend Claude with Skills](https://code.claude.com/docs/en/skills)
- [Claude Code Documentation - Automatic Discovery from Nested Directories](https://code.claude.com/docs/en/skills#automatic-discovery-from-nested-directories)
