创建一个代理团队，构建一个时间编排工作流，以可视化 SVG 卡片的形式展示迪拜当前时间。该工作流遵循 **Command → Agent → Skill** 架构模式：

- 由一个命令负责编排流程并处理用户交互
- 由一个代理借助预加载技能获取迪拜实时当前时间
- 由一个技能根据获取到的数据创建可视化 SVG 时间卡片

**重要**：所有文件都必须创建在 `agent-teams/.claude/` 内，
**不要** 创建到仓库根目录的 `.claude/` 中。这样可以让代理团队的产物保持自包含，并通过 `cd agent-teams && claude` 直接运行。
不要引用或复制现有的天气工作流，一切都从零开始构建。

分配以下团队成员：

1. **Command 架构师**：在 `agent-teams/.claude/commands/time-orchestrator.md` 中设计并实现 `/time-orchestrator`
   命令。该命令应当：
   - 通过 Agent 工具（**不是** bash）调用 time-agent，获取迪拜（Asia/Dubai 时区，UTC+4）的当前时间
   - 通过 Skill 工具调用 time-svg-creator 技能，根据获取到的时间数据渲染 SVG 卡片
   - 在 frontmatter 中使用 `model: haiku`
   - 写明关键要求：顺序执行、正确使用工具（代理用 Agent 工具，技能用 Skill 工具）、以及输出摘要
   通过共享任务列表与其他成员协作，约定组件之间传递的数据契约 `{time, timezone, formatted}`。

2. **Agent 工程师**：在 `agent-teams/.claude/agents/time-agent.md` 中设计并实现 `time-agent`，
   并在 `agent-teams/.claude/skills/time-fetcher/SKILL.md` 中实现其预加载技能 `time-fetcher`。该代理应当：
   - 使用 Bash 和 `TZ='Asia/Dubai' date '+%Y-%m-%d %H:%M:%S %Z'` 获取迪拜当前时间（Asia/Dubai，UTC+4）
   - 将时间值、时区名称和格式化字符串返回给命令
   - 使用 frontmatter：tools（Bash）、model: haiku、color: blue、maxTurns: 3
   - 通过 `skills:` 字段预加载 `time-fetcher` 技能
   `time-fetcher` 技能（`agent-teams/.claude/skills/time-fetcher/SKILL.md`）应包含获取迪拜时间的 bash 命令、预期输出格式，
   并设置 `user-invocable: false`，因为它只是代理专用的领域知识。
   请把已达成一致的数据契约发布到共享任务列表中，以便 Command 架构师和 Skill 设计师对齐接口。

3. **Skill 设计师**：在 `agent-teams/.claude/skills/time-svg-creator/SKILL.md` 中设计并实现
   `time-svg-creator` 技能，并补充支持文件 `reference.md`（SVG 模板 + 输出模板）和 `examples.md`
   （输入 / 输出示例对）。该技能应当：
   - 从调用上下文接收时间值、时区和格式化字符串
   - 为迪拜创建一张自包含的 SVG 时间卡片，显示当前时间
   - 将 SVG 写入 `agent-teams/output/dubai-time.svg`
   - 将 Markdown 摘要写入 `agent-teams/output/output.md`
   - 严格使用传入的时间值，**绝不** 重新抓取
   - 把模板放在 `reference.md` 中（带占位符的 SVG 标记和 Markdown 输出模板），示例对放在 `examples.md`
   另外请创建 `agent-teams/output/` 目录，用于存放输出文件。

三位成员都应在共享任务列表中创建任务，以便围绕数据契约进行协作：代理返回 `{time, timezone, formatted}`，
命令把它透传进上下文，技能消费这些字段。
请同时并行启动三位成员，因为这些组件彼此独立，
他们只需要就数据接口达成一致，不需要等待彼此完成实现。
