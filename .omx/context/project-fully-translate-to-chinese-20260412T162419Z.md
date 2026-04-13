## Task Statement

将 `D:\apps\claude-code-best-practice-zh` 项目完全翻译为中文，并形成可执行的实施计划。

## Desired Outcome

- 仓库面向中文读者发布时，核心文档、导航、说明文字、标题、表格内容、alt 文本、必要 UI 文案均为自然、统一的简体中文。
- 不破坏现有文档结构、相对链接、资源引用、锚点导航、徽章展示与图片路径。
- 为术语、专有名词、命令、路径、版本号、外链标题建立一致的翻译策略。
- 明确哪些内容保留英文原文，哪些需要中英并置，哪些需要只译不改路径。
- 明确编码修复与回归验证要求。

## Known Facts / Evidence

- 仓库主要由 Markdown 文档组成，当前统计约有 `106` 个 `.md` 文件、`3` 个 `.html` 文件、`40` 个 `.svg` 文件。
- 根目录存在高权重入口文档 `README.md` 和 `CLAUDE.md`，并按专题分布在 `best-practice/`、`reports/`、`tips/`、`tutorial/`、`development-workflows/`、`implementation/`、`orchestration-workflow/`、`agent-teams/`、`videos/`、`changelog/`。
- `README.md` 仍以英文为主，且已经混入部分中文与编码异常字符，说明本任务既包含翻译，也包含字符编码和文档一致性治理。
- 内容中大量出现官方产品名、命令名、目录名、路径、文件名、外部链接标题、徽章文本、图片 alt 文本、表格标题与锚点链接。
- 仓库说明表明这是“Claude Code 最佳实践”类知识仓库，而非应用程序代码库，因此工作重点是文档内容与信息架构，而不是业务逻辑。

## Constraints

- 需遵循仓库既有结构，尽量避免改动文件路径和资源文件名。
- 应保持 Markdown 相对链接可用。
- 翻译后仍需便于同步上游英文更新，因此术语策略要可持续。
- 不应默认修改所有二进制资源；只有当 SVG/HTML 中存在用户可见英文文本且确有必要时才纳入。
- 任务范围大，适合分阶段推进并设置验证门。

## Unknowns / Open Questions

- “完全翻译”是否包括所有 SVG 内嵌文本、HTML 页面文案、徽章文案与截图中的英文。
- 是否要求保留英文术语括注，还是目标为纯中文优先。
- 是否接受分批合入，还是要求单次完成全仓翻译。
- 现有编码异常是源文件编码问题、终端显示问题，还是历史混排所致，需要进一步验证。

## Likely Touchpoints

- `README.md`
- `CLAUDE.md`
- `best-practice/*.md`
- `reports/*.md`
- `tips/*.md`
- `tutorial/**/*.md`
- `development-workflows/**/*.md`
- `implementation/*.md`
- `orchestration-workflow/*.md`
- `agent-teams/**/*.md`
- `videos/*.md`
- `presentation/index.html`
- `orchestration-workflow/*.svg`
- `reports/assets/*.svg`
