# MCP 服务器最佳实践

![Last Updated](https://img.shields.io/badge/Last_Updated-Mar%2002%2C%202026%2012%3A30%20PM%20PKT-white?style=flat&labelColor=555)<br>
[![Implemented](https://img.shields.io/badge/Implemented-2ea44f?style=flat)](../.mcp.json)

MCP（Model Context Protocol）服务器通过连接外部工具、数据库和 API，为 Claude Code 提供扩展能力。这份指南涵盖日常推荐使用的服务器，以及配置方面的最佳实践。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code 最佳实践</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 日常使用的 MCP 服务器

> *"Went overboard with 15 MCP servers thinking more = better. Ended up using only 4 daily."* - [r/mcp](https://reddit.com/r/mcp/comments/1mj0fxs/)（682 个赞）

| MCP 服务器 | 作用 | 资源 |
|------------|-------------|-----------|
| [**Context7**](https://github.com/upstash/context7) | 将最新库文档拉入上下文，避免因训练数据过旧而产生虚构 API | [Reddit: "by far the best MCP for coding"](https://reddit.com/r/mcp/comments/1qarjqm/) · [npm](https://www.npmjs.com/package/@upstash/context7-mcp) |
| [**Playwright**](https://github.com/microsoft/playwright-mcp) | 浏览器自动化，可自主实现、测试和验证 UI 功能，支持截图、导航和表单测试 | [Reddit: essential for frontend](https://reddit.com/r/mcp/comments/1m59pk0/) · [Docs](https://playwright.dev/) |
| [**Claude in Chrome**](https://github.com/nicobailon/claude-code-in-chrome-mcp) | 把 Claude 接到你真实的 Chrome 浏览器上，检查控制台、网络和 DOM，调试用户真实看到的内容 | [Reddit: "game changer" for debugging](https://reddit.com/r/mcp/comments/1qarjqm/5_mcps_that_have_genuinely_made_me_10x_faster/nza0i7t/) · [对比报告](../reports/claude-in-chrome-v-chrome-devtools-mcp.md) |
| [**DeepWiki**](https://github.com/devanshusemwal/deepwiki-mcp) | 为任意 GitHub 仓库抓取结构化的 wiki 风格文档，包括架构、API 面和关系信息 | [Reddit: "put it behind a gateway with Context7"](https://reddit.com/r/mcp/comments/1qarjqm/) |
| [**Excalidraw**](https://github.com/antonpk1/excalidraw-mcp-app) | 从提示词生成手绘风格的 Excalidraw 架构图、流程图和系统设计图 | [GitHub](https://github.com/antonpk1/excalidraw-mcp-app) |

研究（Context7 / DeepWiki）-> 调试（Playwright / Chrome）-> 文档化（Excalidraw）

---

## 配置

MCP 服务器配置通常写在项目根目录的 `.mcp.json`（项目级）或 `~/.claude.json`（用户级）中。

### 服务器类型

| 类型 | 传输方式 | 示例 |
|------|-----------|---------|
| **stdio** | 启动本地进程 | `npx`、`python`、二进制程序 |
| **http** | 连接远程 URL | HTTP / SSE 端点 |

### `.mcp.json` 示例

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"]
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp"]
    },
    "deepwiki": {
      "command": "npx",
      "args": ["-y", "deepwiki-mcp"]
    },
    "remote-api": {
      "type": "http",
      "url": "https://mcp.example.com/mcp"
    }
  }
}
```

对于密钥等敏感信息，建议使用环境变量展开，而不是把 API Key 直接提交进 `.mcp.json`：

```json
{
  "mcpServers": {
    "remote-api": {
      "type": "http",
      "url": "https://mcp.example.com/mcp?token=${MCP_API_TOKEN}"
    }
  }
}
```

### MCP 服务器相关设置

`.claude/settings.json` 中的这些设置项用于控制 MCP 服务器的审批行为：

| 键 | 类型 | 说明 |
|-----|------|-------------|
| `enableAllProjectMcpServers` | boolean | 自动批准 `.mcp.json` 中的所有服务器，无需提示 |
| `enabledMcpjsonServers` | array | 自动批准的特定服务器名称白名单 |
| `disabledMcpjsonServers` | array | 明确拒绝的特定服务器名称黑名单 |

### MCP 工具的权限规则

权限规则中，MCP 工具使用 `mcp__<server>__<tool>` 的命名约定：

```json
{
  "permissions": {
    "allow": [
      "mcp__*",
      "mcp__context7__*",
      "mcp__playwright__browser_snapshot"
    ],
    "deny": [
      "mcp__dangerous-server__*"
    ]
  }
}
```

---

## MCP 作用域

MCP 服务器可以定义在三个层级：

| 作用域 | 位置 | 用途 |
|-------|----------|---------|
| **Project** | `.mcp.json`（仓库根目录） | 团队共享的服务器，可提交到 git |
| **User** | `~/.claude.json`（`mcpServers` 键） | 个人在所有项目中复用的服务器 |
| **Subagent** | 代理 frontmatter（`mcpServers` 字段） | 仅对特定子代理生效的服务器 |

优先级：Subagent > Project > User

---

## 来源

- [MCP Servers - Claude Code Docs](https://code.claude.com/docs/en/mcp)
- [Model Context Protocol Specification](https://modelcontextprotocol.io/)
- [5 MCPs that have genuinely made me 10x faster - r/mcp](https://reddit.com/r/mcp/comments/1qarjqm/)
- [MCP Server Overload Discussion - r/mcp](https://reddit.com/r/mcp/comments/1mj0fxs/)
