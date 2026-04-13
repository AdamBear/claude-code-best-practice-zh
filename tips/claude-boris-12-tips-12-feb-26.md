# Claude Code 的 12 种自定义方式：来自 Boris Cherny 的技巧

这是 Boris Cherny（[@bcherny](https://x.com/bcherny)），Claude Code 的创造者，于 2026 年 2 月 12 日分享的自定义技巧摘要。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 背景

Boris Cherny 提到，可定制性是工程师最喜欢 Claude Code 的原因之一：钩子、插件、LSP、MCP、技能、effort、自定义代理、状态栏、输出风格等等。他分享了开发者和团队在实际使用中采用的 12 种实用定制方式。

<a href="https://x.com/bcherny/status/2021699851499798911"><img src="assets/boris-12-feb-26/0.webp" alt="Boris Cherny 介绍推文" width="50%" /></a>

---

## 1/ 配置你的终端

把终端调整到最适合 Claude Code 的状态：

- **Theme**：运行 `/config` 设置亮色或暗色模式
- **Notifications**：为 iTerm2 启用通知，或者使用自定义通知钩子
- **Newlines**：如果你是在 IDE 终端、Apple Terminal、Warp 或 Alacritty 中使用 Claude Code，运行 `/terminal-setup` 启用 `shift+enter` 换行（这样你就不用输入 `\`）
- **Vim mode**：运行 `/vim`

<a href="https://x.com/bcherny/status/2021699859359883608"><img src="assets/boris-12-feb-26/1.webp" alt="配置你的终端" width="50%" /></a>

---

## 2/ 调整 Effort 级别

运行 `/model`，选择你偏好的 effort 级别：

- **Low**：更少 token，更快响应
- **Medium**：平衡型表现
- **High**：更多 token，更强智能

Boris 的偏好是：所有事情都用 High。

<a href="https://x.com/bcherny/status/2021699860869902424"><img src="assets/boris-12-feb-26/2.webp" alt="调整 effort 级别" width="50%" /></a>

---

## 3/ 安装插件、MCP 和技能

插件可以让你安装 LSP（主流语言都支持）、MCP、技能、代理，以及自定义钩子。

你可以从 Anthropic 官方插件市场安装，也可以为自己的公司搭建私有市场。把 `settings.json` 提交进代码库后，团队成员就能自动获得这些 marketplace 配置。

运行 `/plugin` 开始配置。

<a href="https://x.com/bcherny/status/2021699862522364149"><img src="assets/boris-12-feb-26/3.webp" alt="安装插件、MCP 和技能" width="50%" /></a>

---

## 4/ 创建自定义代理

把 `.md` 文件放进 `.claude/agents`，就能创建自定义代理。每个代理都可以拥有自定义名称、颜色、工具集、预先允许和预先禁止的工具、权限模式以及模型。

你还可以通过 `settings.json` 里的 `"agent"` 字段，或者使用 `--agent` 参数，为主对话设置默认代理。

运行 `/agents` 开始配置。

<a href="https://x.com/bcherny/status/2021700144039903699"><img src="assets/boris-12-feb-26/4.webp" alt="创建自定义代理" width="50%" /></a>

---

## 5/ 预先批准常见权限

Claude Code 的权限系统结合了提示词注入检测、静态分析、沙箱以及人工监督。

开箱即用时，会默认预先批准一小部分安全命令。如果想扩展范围，可以运行 `/permissions`，把更多规则加入 allow 和 block 列表。然后把这些规则提交到团队的 `settings.json` 中。

支持完整的通配符语法，例如 `Bash(bun run *)` 或 `Edit(/docs/**)`。

<a href="https://x.com/bcherny/status/2021700332292911228"><img src="assets/boris-12-feb-26/5.webp" alt="预先批准常见权限" width="50%" /></a>

---

## 6/ 启用沙箱

使用 Claude Code 开源的沙箱运行时，可以在提升安全性的同时减少权限提示。

运行 `/sandbox` 启用它。沙箱运行在你的本机上，同时支持文件隔离与网络隔离。

<a href="https://x.com/bcherny/status/2021700506465579443"><img src="assets/boris-12-feb-26/6.webp" alt="启用沙箱" width="50%" /></a>

---

## 7/ 添加状态栏

自定义状态栏会显示在输入框下方，展示模型、目录、剩余上下文、成本，以及你希望在工作时看到的任何信息。

团队中每个人都可以有不同的 statusline。使用 `/statusline`，让 Claude 根据你的 `.bashrc` 或 `.zshrc` 帮你生成一个。

<a href="https://x.com/bcherny/status/2021700784019452195"><img src="assets/boris-12-feb-26/7.webp" alt="添加状态栏" width="50%" /></a>

---

## 8/ 自定义快捷键绑定

Claude Code 中的每一个快捷键都可以自定义。运行 `/keybindings` 重新映射任意按键。设置支持热重载，所以你可以立即体验改动效果。

<a href="https://x.com/bcherny/status/2021700883873165435"><img src="assets/boris-12-feb-26/8.webp" alt="自定义快捷键绑定" width="50%" /></a>

---

## 9/ 设置钩子

钩子可以让你以确定性的方式接入 Claude 的生命周期：

- 自动把权限请求路由到 Slack 或 Opus
- 当 Claude 一轮结束时，推动它继续执行
- 在工具调用前后进行预处理或后处理，例如加入自定义日志

直接让 Claude 帮你添加一个钩子即可开始。

<a href="https://x.com/bcherny/status/2021701059253874861"><img src="assets/boris-12-feb-26/9.webp" alt="设置钩子" width="50%" /></a>

---

## 10/ 自定义 Spinner 动词

你可以自定义 spinner verb，新增或替换默认动词列表。把 `settings.json` 提交进版本控制后，团队成员也能共享这些动词配置。

<a href="https://x.com/bcherny/status/2021701145023197516"><img src="assets/boris-12-feb-26/10.webp" alt="自定义 spinner 动词" width="50%" /></a>

---

## 11/ 使用输出风格

运行 `/config` 并设置输出风格，让 Claude 用不同语气或格式回应你。

- **Explanatory**：推荐在熟悉新代码库时使用，让 Claude 在工作过程中解释框架与代码模式
- **Learning**：让 Claude 以教练方式带你完成代码修改
- **Custom**：创建自定义输出风格，调整 Claude 的表达声音

<a href="https://x.com/bcherny/status/2021701379409273093"><img src="assets/boris-12-feb-26/11.webp" alt="使用输出风格" width="50%" /></a>

---

## 12/ 把一切都定制起来

Claude Code 开箱即用已经很好，但如果你进行了定制，最好把 `settings.json` 提交到 git，这样团队也能一起受益。配置支持多个层级：

- 针对整个代码库
- 针对子目录
- 只针对你自己
- 通过企业级策略统一下发

目前有 37 个设置项和 84 个环境变量（你可以在 `settings.json` 里使用 `"env"` 字段，避免依赖包装脚本），因此你想要的大多数行为，大概率都能配置出来。

<a href="https://x.com/bcherny/status/2021701636075458648"><img src="assets/boris-12-feb-26/12.webp" alt="把一切都定制起来" width="50%" /></a>

---

## 来源

- [Boris Cherny (@bcherny) on X — February 12, 2026](https://x.com/bcherny)
- [Claude Code Terminal Setup Docs](https://code.claude.com/docs/en/terminal)
- [Claude Code Plugins & Discovery Docs](https://code.claude.com/docs/en/discover-plugins)
- [Claude Code Sub-agents Docs](https://code.claude.com/docs/en/sub-agents)
- [Claude Code Permissions Docs](https://code.claude.com/docs/en/permissions)
- [Claude Code Sandbox Docs](https://code.claude.com/docs/en/sandbox)
- [Claude Code Status Line Docs](https://code.claude.com/docs/en/statusline)
- [Claude Code Keyboard Shortcuts Docs](https://code.claude.com/docs/en/keybindings)
- [Claude Code Hooks Reference](https://code.claude.com/docs/en/hooks)
- [Claude Code Output Styles Docs](https://code.claude.com/docs/en/output-styles)
- [Claude Code Settings Docs](https://code.claude.com/docs/en/settings)
