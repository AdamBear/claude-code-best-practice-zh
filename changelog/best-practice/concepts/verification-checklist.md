# 验证清单：README 的 CONCEPTS 部分

用于验证 CONCEPTS 表准确性的规则。每次工作流运行时都要检查全部规则。

## 规则

### 1. 外部 URL 可用性
- **类别**：URL 准确性
- **检查内容**：CONCEPTS 表中的每个外部 URL（文档链接）都能返回有效页面
- **检查深度**：抓取每个 URL，确认它加载的是预期页面，而不是跳到错误页面
- **对照来源**：`https://code.claude.com/docs/llms.txt` 中的规范 URL 列表
- **添加日期**：2026-03-02
- **来源**：Permissions 的 URL `/iam` 被发现会跳到 Authentication 页面，而不是 Permissions 页面

### 2. 锚点片段有效性
- **类别**：URL 准确性
- **检查内容**：所有带锚点片段（`#section-name`）的 URL，锚点都必须对应目标页面上的真实标题
- **检查深度**：抓取页面并验证对应标题确实存在，且锚点名称符合预期
- **对照来源**：抓取到的页面内容
- **添加日期**：2026-03-02
- **来源**：Rules 的锚点 `#modular-rules-with-clauderules` 已过时；章节改名为 `#organize-rules-with-clauderules`

### 3. 缺失的文档页面
- **类别**：缺失概念
- **检查内容**：官方文档索引（`llms.txt`）中代表用户可见功能的每个页面，都应在 CONCEPTS 表中有对应行
- **检查深度**：将完整文档索引与 CONCEPTS 表条目逐一对比
- **对照来源**：`https://code.claude.com/docs/llms.txt`
- **添加日期**：2026-03-02
- **来源**：最初发现多个缺失概念（Agent Teams、Keybindings、Model Configuration 等）

### 4. 本地徽章链接有效性
- **类别**：徽章准确性
- **检查内容**：CONCEPTS 表中的每个徽章目标路径（`best-practice/*.md`、`implementation/*.md`、`.claude/*/`）都指向真实存在的文件或目录
- **检查深度**：使用 Read/Glob 验证文件是否存在
- **对照来源**：本地文件系统
- **添加日期**：2026-03-02
- **来源**：初始清单建立时加入

### 5. 描述是否最新
- **类别**：描述准确性
- **检查内容**：每个概念的描述都应准确反映当前官方文档中的定义
- **检查深度**：将 README 中的描述与官方页面的 meta description 或首段文字进行对比
- **对照来源**：官方文档页面内容
- **添加日期**：2026-03-02
- **来源**：Memory 的描述曾遗漏 auto memory，MCP Servers 的位置也曾遗漏 `.mcp.json`
