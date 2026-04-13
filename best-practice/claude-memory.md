# Claude 记忆

通过 `CLAUDE.md` 文件提供持久上下文：如何编写，以及它们在 monorepo 中如何加载。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 1. 如何写出高质量的 CLAUDE.md

一个结构良好的 `CLAUDE.md`，往往是提升 Claude Code 在项目中输出质量最有效的方式。Humanlayer 有一篇非常好的指南，介绍了应该写什么、如何组织结构，以及常见陷阱。

- [Humanlayer - Writing a good Claude.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md)

---

## 2. 大型 Monorepo 中的 CLAUDE.md

在 monorepo 中使用 Claude Code 时，理解 `CLAUDE.md` 文件是如何被加载进上下文的，对于组织项目指令非常关键。

<p align="center">
  <a href="https://x.com/bcherny/status/2016339448863355206"><img src="assets/claude-memory/claude-memory-monorepo.jpg" alt="CLAUDE.md 在 monorepo 中的加载方式" width="600"></a>
</p>

### 两种加载机制

Claude Code 使用两种不同机制来加载 `CLAUDE.md` 文件：

#### 向上加载（沿目录树向上）

当你启动 Claude Code 时，它会从当前工作目录开始，**沿着目录树向上**一直走到文件系统根目录，并加载沿途找到的每一个 `CLAUDE.md`。这些文件会在**启动时立即**被加载。

#### 向下加载（沿目录树向下）

位于当前工作目录下级子目录中的 `CLAUDE.md` 文件，**不会在启动时加载**。只有当 Claude 在会话中读取这些子目录下的文件时，它们才会被纳入上下文。这种方式被称为**懒加载**。

### Monorepo 结构示例

考虑一个典型的 monorepo，它用不同目录承载不同组件：

```
/mymonorepo/
├── CLAUDE.md          # 根级说明（所有组件共享）
├── frontend/
│   ├── CLAUDE.md      # 前端专属说明
├── backend/
│   ├── CLAUDE.md      # 后端专属说明
└── api/
    ├── CLAUDE.md      # API 专属说明
```

### 场景 1：从根目录运行 Claude Code

当你在 `/mymonorepo/` 中运行 Claude Code：

```bash
cd /mymonorepo
claude
```

| 文件 | 启动时加载？ | 原因 |
|------|-------------------|--------|
| `/mymonorepo/CLAUDE.md` | 是 | 它就是当前工作目录 |
| `/mymonorepo/frontend/CLAUDE.md` | 否 | 只有在读写 `frontend/` 中的文件时才会加载 |
| `/mymonorepo/backend/CLAUDE.md` | 否 | 只有在读写 `backend/` 中的文件时才会加载 |
| `/mymonorepo/api/CLAUDE.md` | 否 | 只有在读写 `api/` 中的文件时才会加载 |

### 场景 2：从组件目录运行 Claude Code

当你在 `/mymonorepo/frontend/` 中运行 Claude Code：

```bash
cd /mymonorepo/frontend
claude
```

| 文件 | 启动时加载？ | 原因 |
|------|-------------------|--------|
| `/mymonorepo/CLAUDE.md` | 是 | 它是祖先目录中的文件 |
| `/mymonorepo/frontend/CLAUDE.md` | 是 | 它就在当前工作目录中 |
| `/mymonorepo/backend/CLAUDE.md` | 否 | 位于目录树的另一个分支 |
| `/mymonorepo/api/CLAUDE.md` | 否 | 位于目录树的另一个分支 |

### 关键结论

1. **祖先目录总会在启动时加载**：Claude 会沿目录树向上查找，并加载找到的全部 `CLAUDE.md`。这样你始终能拿到仓库根级的通用说明。

2. **子目录采用懒加载**：子目录里的 `CLAUDE.md` 只有在你与该目录内文件交互时才会加载，避免无关上下文把会话撑大。

3. **同级目录不会被加载**：如果你正在 `frontend/` 中工作，就不会自动把 `backend/CLAUDE.md` 或 `api/CLAUDE.md` 拉进上下文。

4. **全局 CLAUDE.md**：你还可以把 `CLAUDE.md` 放在主目录的 `~/.claude/CLAUDE.md`，它会对所有 Claude Code 会话生效，与具体项目无关。

### 为什么这种设计适合 Monorepo

- **共享说明会向下传播**：根目录的 `CLAUDE.md` 可以承载整个仓库通用的约定、编码规范和公共模式。

- **组件专属说明保持隔离**：前端开发者不需要把后端特有说明塞进上下文，反之亦然。

- **上下文得到优化**：通过对子目录 `CLAUDE.md` 采用懒加载，Claude Code 避免在启动时一次性读入可能多达数百 KB 的无关说明。

### 最佳实践

1. **把共享约定写在根级 `CLAUDE.md`**：例如编码规范、提交信息格式、PR 模板和其他仓库通用指南。

2. **把组件专属说明写在对应组件的 `CLAUDE.md`**：例如框架特有模式、组件架构、只对该组件适用的测试约定。

3. **用 `CLAUDE.local.md` 存放个人偏好**：并把它加入 `.gitignore`，用于存放不需要与团队共享的个人说明。

---

## 来源

- [Claude Code Documentation - How Claude Looks Up Memories](https://code.claude.com/docs/en/memory#how-claude-looks-up-memories)
- [Boris Cherny on X - Clarification on CLAUDE.md Loading](https://x.com/bcherny/status/2016339448863355206)
- [Humanlayer - Writing a good Claude.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md)
