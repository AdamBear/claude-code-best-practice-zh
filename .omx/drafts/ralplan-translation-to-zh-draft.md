# 将本项目完全翻译为中文 - 共识计划草案

## Requirements Summary

目标是在尽量不改动路径、资源文件名和信息架构的前提下，将仓库 `D:\apps\claude-code-best-practice-zh` 的用户可见内容完整中文化，并保证文档可读性、术语一致性、编码正确性、链接可用性以及锚点兼容性。

范围按“用户可见文本”定义，而不是仅按文件后缀定义：
- 必含：所有 `.md` 文档中的英文正文、标题、表格、列表、图注、提示文案、图片 `alt` 文本。
- 高优先级入口：`README.md`、`CLAUDE.md`。
- 高密度内容目录：`best-practice/`、`reports/`、`tips/`、`tutorial/`、`development-workflows/`、`implementation/`、`orchestration-workflow/`、`agent-teams/`、`videos/`、`changelog/`。
- 条件纳入：`.html` 中的可见文本、`title`、meta 描述、导航与辅助文案。
- 条件纳入：`.svg` 中直接面向读者渲染的文本。
- 默认不翻译：代码块内代码、内联代码、命令、URL、文件路径、资源文件名、外部项目名、不可安全本地化的标识符。
- 必做修复：`README.md` 中已知中文混入与编码异常字符。
- 必做保护：相对链接、锚点跳转、图片引用、目录结构、引用关系。

本计划直接锁定“完全翻译”的最终边界为：
- 所有读者可见英文最终都必须消除，包括高风险 SVG 的重绘或替代资源制作。

这意味着：
- A 类 SVG：必须在本期中文化。
- B 类 SVG：必须在本期完成翻译与必要重排。
- C 类 SVG：不能只登记例外，必须在本期通过重绘、替代资产或等效改造消除可见英文。

允许保留英文的内容仅限非用户可见或不应翻译项：代码、命令、URL、路径、资源文件名、专有标识符、品牌名原词首次括注等。

## Acceptance Criteria

- `README.md` 与 `CLAUDE.md` 同时满足：
  - 非白名单可见英文命中数 = `0`
  - 乱码扫描命中数 = `0`
  - 站内相对链接未解析数量 = `0`
  - 已知 fragment 入链未解析数量 = `0`
- 目标目录中的全部 `.md` 文件同时满足：
  - 非白名单可见英文命中数 = `0`
  - 仅以下内容允许保留英文：代码块、内联代码、命令、URL、路径、资源文件名、专有名词原词括注、白名单记录项
- `3` 个 `.html` 文件
  - `presentation/index.html`
  - `!/video-presentation-transcript/1-video-workflow.html`
  - `!/thumbnail/daily-workflows.html`
  同时满足：
  - 存在机读验收清单 `docs/html-verification-manifest.json`
  - `title` 文本非空，且非白名单可见英文命中数 = `0`
  - 每个 HTML 文件都在 manifest 中定义固定的 `hero_selectors`、`cta_selectors`、`required_text_selectors`
  - manifest 中每个选择器的查询结果非空，且其文本的非白名单可见英文命中数 = `0`
  - 原有 `id`、`class`、资源引用路径不变
  - manifest 中定义的全部关键节点查询结果非空
- 全部 `.svg` 资源同时满足：
  - 存在机读资产清单 `docs/svg-localization-manifest.json`
  - 非白名单可见英文命中数 = `0`
  - 每个 SVG 文件都在 manifest 中声明 `classification` 与 `completion_mode`
  - `classification` 只能为 `A`、`B`、`C`
  - `completion_mode` 只能为 `translated`、`reflowed`、`replaced`
  - `A` 类文件的 `completion_mode` = `translated`
  - `B` 类文件的 `completion_mode` = `reflowed`
  - `C` 类文件的 `completion_mode` = `replaced`
  - 所有文本节点边界框均位于 `viewBox` 或画布边界内
  - 文本节点边界框重叠检测命中数 = `0`
- 所有站内相对链接仍可解析，不因标题翻译或锚点变化导致失效。
- 对存在入链依赖的标题，已采用明确的锚点兼容策略并通过验证：
  - 入链扫描范围包含仓库内 Markdown、HTML 中的 `](#...)`、`href="#..."`、`<a href="#...">`、指向仓库文档的带 fragment URL
  - 若某标题存在入链依赖，则在翻译后的标题前保留旧锚点别名，例如插入 `<a id="old-slug"></a>` 兼容旧 fragment
  - 若标题无入链依赖，则允许仅保留中文标题锚点
  - 验证标准为仓库内已知 fragment 引用的未解析数量 = `0`
- 建立并应用统一术语表，至少覆盖高频术语、工作流词汇、代理角色词汇、验证词汇。
- 建立白名单与例外清单 schema，并将所有合理残留英文纳入治理。每条记录至少包含：
  - 文件
  - 位置
  - 原文
  - 保留原因
  - 类型
  - 是否需后续处理
- 全仓以 UTF-8 正常保存，无新增编码异常字符。
- 除白名单记录外，仓库中不再存在面向读者的可见英文文本。

## RALPLAN-DR Summary

### Principles

- 优先定义兼容规则和例外治理，再批量翻译，避免后期返工。
- 以读者体验为中心，但不能用可读性换取导航失效。
- 保持结构稳定，尽量不改路径、文件名和资源命名。
- 对 Markdown、HTML、SVG 采用不同边界与验证策略，避免一刀切。
- 每个阶段必须自带验证门，机制先试点，再扩到批量目录。

### Decision Drivers

- 链接与锚点稳定性：文档仓库最核心风险是导航失效与引用断裂。
- 规模与一致性：约 `106` 个 Markdown 文件，没有术语表和白名单治理会迅速失控。
- 资产类型差异：`.md`、`.html`、`.svg` 的翻译风险和编辑方式不同，必须差异化处理。

### Viable Options

#### Option A：入口优先 + 兼容策略先行 + 目录分批 + 资源分级翻译

- 做法：先定义锚点、白名单、例外治理和 SVG 完成定义，再处理 `README.md`、`CLAUDE.md` 作为机制试点，之后按目录批量翻译 Markdown，最后处理 HTML、SVG 与仓库级收口。
- 优点：最符合当前约束；能把全局规则前置；适合大规模文档仓库；每阶段可验证。
- 缺点：推进周期较长；在收口前会短期处于部分中文、部分英文的过渡状态。

#### Option B：全仓一次性翻译后统一修链修锚

- 做法：先对全部可见文本做全量翻译，再统一处理链接、锚点、术语和编码。
- 优点：理论上整体推进速度快，能一次性建立中文基线。
- 缺点：回归面大；术语漂移概率高；很难追溯锚点与交叉引用问题；不适合当前“尽量不改路径和资源名”的约束。

#### Option C：Markdown 全量中文，HTML/SVG 延后

- 做法：只翻译 `.md`，将 `.html` 和 `.svg` 视为后续资产工作。
- 优点：主文档收益最大，最快看到结果。
- 缺点：不满足“完全翻译”的严格目标，读者仍会遇到英文界面与图示。

### Recommended Option

推荐 Option A 作为执行路径，并在其内部强制达成“零英文可见资产”的最终验收目标。也就是说，采用分阶段实现方式，但最终验收不接受“高风险 SVG 留待后续”的结果。

## Implementation Steps

### 阶段 0：盘点与基线冻结

- 建立内容清单，按文件类型与目录汇总：
  - 根入口：`README.md`、`CLAUDE.md`
  - 目录：`best-practice/`、`reports/`、`tips/`、`tutorial/`、`development-workflows/`、`implementation/`、`orchestration-workflow/`、`agent-teams/`、`videos/`、`changelog/`
  - 资产：所有 `.html`、`.svg`
- 生成四个基线报告：
  - 英文残留基线
  - 乱码与编码异常基线
  - 相对链接基线
  - 入链锚点基线
- 初步识别不应翻译的内容类型：
  - 代码块
  - 内联代码
  - 命令
  - 路径
  - URL
  - 标识符
  - 品牌名、模型名、协议名

### 阶段 1：兼容策略设计与治理结构定稿

- 新增统一规范文档，建议位置：
  - `docs/localization-style-guide.md`
  - `docs/translation-glossary.md`
  - `docs/localization-exceptions-schema.md`
  - `docs/html-verification-manifest.json`
  - `docs/svg-localization-manifest.json`
- 定义并冻结以下规则：
  - 标题翻译规则
  - 锚点兼容规则
  - 入链映射与高风险标题识别规则
  - Markdown 可翻译边界规则
  - HTML 可翻译边界规则
  - SVG A/B/C 分类标准与完成定义
  - HTML 验收选择器清单 schema
  - SVG 资产清单 schema
  - 英文残留扫描白名单规则
  - 例外清单 schema
- 例外记录最少字段固定为：
  - 文件
  - 位置
  - 原文
  - 保留原因
  - 类型
  - 是否需后续处理
- HTML 验收清单最少字段固定为：
  - 文件
  - `hero_selectors`
  - `cta_selectors`
  - `required_text_selectors`
- SVG 资产清单最少字段固定为：
  - 文件
  - `classification`
  - `completion_mode`
  - `source_text_nodes`
  - `verification_required`
- 锚点兼容机制固定为：
  - 扫描仓库内所有 fragment 入链
  - 对存在入链的原英文标题，保留旧 slug 别名锚点
  - 中文标题继续生成新的中文锚点
  - 兼容覆盖对象包含站内目录跳转、文档内跳转、跨文档带 fragment 的相对链接与显式仓库 URL

### 阶段 2：入口文档机制试点

- 先处理 `README.md`：
  - 翻译英文主体
  - 修复乱码与异常字符
  - 保持目录结构与相对链接
  - 对被引用标题采用锚点兼容策略
- 再处理 `CLAUDE.md`：
  - 在不改变指令含义的前提下中文化用户可见说明
  - 对必须保持原样的命令与标识符保留英文
- 这两个文件不只是风格样板，也是机制试点，必须验证：
  - 旧锚点兼容生效
  - 手写目录跳转正常
  - 链接检查能够识别真实问题
  - 白名单规则固定后不再临时扩张
  - 所有已知 fragment 入链解析成功

### 阶段 3：按目录批量翻译 Markdown 主体

- 建议分批顺序：
  1. `tutorial/`、`best-practice/`、`tips/`
  2. `development-workflows/`、`implementation/`、`orchestration-workflow/`
  3. `agent-teams/`、`reports/`、`videos/`、`changelog/`
- 每批执行相同流程：
  - 逐文件翻译可见文本
  - 统一术语替换
  - 保留代码、命令、路径、URL
  - 处理图片 `alt` 文本，不改 URL
  - 检查相对链接文本与目标一致性
  - 扫描新增乱码与异常残留英文
- 每批完成后立即跑验证，不累计到最后。

### 阶段 4：处理 HTML 可见文本与行为耦合属性

- 识别 `3` 个 `.html` 文件中的：
  - `<title>`
  - meta 描述
  - 正文可见文本
  - 按钮与链接标签
  - `alt`、`aria-label`、`title`
- 保持 DOM 结构、类名、ID、脚本引用不变。
- 区分“纯展示文案”与“行为耦合文本或属性”。
- 对 HTML 至少做 DOM 级 smoke check。最低检查对象为：
  - `docs/html-verification-manifest.json` 已存在
  - manifest 中列出的全部选择器查询结果非空
  - manifest 中列出的全部节点文本非白名单可见英文命中数 = `0`

### 阶段 5：处理 SVG 可见文本

- 将 `.svg` 分为三类：
  - A 类：纯文本节点，可直接安全翻译
  - B 类：文本可改但需要重新排版
  - C 类：文本转路径或不可安全编辑，需要重绘或替代
- 处理策略：
  - A 类必须翻译并在 manifest 中标记为 `translated`
  - B 类必须翻译并在 manifest 中标记为 `reflowed`
  - C 类必须在本期通过重绘、替代资产或等效改造并在 manifest 中标记为 `replaced`
- 对修改后的 SVG 做几何检测，确认：
  - 文本节点边界框未超出画布边界
  - 文本节点边界框未发生重叠

### 阶段 6：仓库级收口

- 仓库级扫描：
  - 失效相对链接
  - 受标题变化影响的内部锚点
  - 非预期英文残留
  - Unicode 异常字符和替换符
- 生成白名单与例外清单定稿：
  - 品牌名
  - 命令行参数
  - API 名
  - 模型名
  - 文件路径
  - 外链标题
  - 不可本地化但非用户可见的保留项

### 阶段 7：最终审校与发布准备

- 对高权重入口和每个主目录至少抽检一个代表文件。
- 复核术语一致性、锚点兼容性和中文可读性。
- 输出最终报告：
  - 已翻译范围
  - 保留英文白名单
  - 已完成重绘或替代的 SVG 清单
  - 链接、锚点与编码验证结果
  - 剩余风险说明

## Risks and Mitigations

### 风险：标题翻译导致锚点变化，内部跳转失效

- 缓解：在阶段 1 明确定义锚点兼容机制；先做入链映射；在 `README.md`、`CLAUDE.md` 机制试点验证通过后才允许批量翻译。

### 风险：同一术语在不同目录出现多种译法

- 缓解：先建立术语表；批次结束后做全仓一致性替换；入口文档作为风格基准。

### 风险：README 中既有乱码与中英混排，修复时误伤链接或标记

- 缓解：优先单独处理 `README.md`；保留结构；修改后做定向 diff、链接验证与锚点验证。

### 风险：SVG 文本改动导致布局破坏

- 缓解：先分类；A/B/C 分流；高风险资产不能靠“顺手改一下”处理；必要时进入重绘或替代资产流程；本期结束时不允许存在待重绘且仍含可见英文的 SVG。

### 风险：HTML 文案与脚本或属性耦合，翻译后页面异常

- 缓解：区分纯展示文案与行为耦合文本；不改类名、ID 和逻辑键；执行 DOM 级 smoke check。

### 风险：误将代码、命令、路径、链接目标翻译，造成示例失真

- 缓解：建立 parser-aware 边界规则；优先保留代码块、内联代码、链接目标和引用式链接定义原样。

### 风险：白名单变成“扫描不过就加”的逃逸口

- 缓解：冻结 schema；所有例外都必须记录文件、位置、原文、原因、类型和后续动作。

## Verification Steps

- 扫描 Markdown、HTML、SVG 中的非白名单可见英文，验证命中数 = `0`。
- 扫描乱码字符、替换符、异常编码片段，验证命中数 = `0`，重点复查 `README.md`。
- 验证所有相对链接、图片链接、文档交叉引用，确认未解析数量 = `0`。
- 基于入链映射检查标题变更引起的锚点引用变化，确认已知 fragment 入链未解析数量 = `0`。
- 对 `README.md` 与 `CLAUDE.md` 机制试点执行验证门：
  - 旧锚点兼容成立
  - 手写目录可跳转
  - 白名单规则固定后不再临时扩张
  - 已知 fragment 入链全部解析成功
- 对 `3` 个 `.html` 做最小渲染验证与 DOM 级 smoke check，依据 `docs/html-verification-manifest.json` 确认全部选择器查询结果非空，且对应节点文本中的非白名单可见英文命中数 = `0`。
- 对全部已修改 `.svg` 依据 `docs/svg-localization-manifest.json` 执行验证，确认：
  - 每个文件均存在机读分类与完成状态
  - `classification` 与 `completion_mode` 组合合法
  - 非白名单可见英文命中数 = `0`
  - 超出画布命中数 = `0`
  - 重叠命中数 = `0`
- 抽检每个主要目录至少 `1-2` 个代表文件，确认正文已中文化且术语一致。
- 输出最终白名单与例外清单，证明残留英文均属合理保留。若出现需要后续动作的例外，必须是非用户可见项，而不是可见资产残留。

## ADR

### Decision

采用“兼容策略先行、入口文档机制试点、Markdown 分目录批量推进、HTML 与 SVG 分级处理、每阶段带验证门”的本地化方案。

### Drivers

- 仓库是文档项目，价值核心在可读性、导航和引用稳定性。
- 文件规模较大，必须先控制术语一致性、锚点兼容和例外治理。
- `README.md` 当前存在乱码与中英混杂，需要先建立试点与修复基线。
- `.html`、`.svg` 的编辑风险明显高于 `.md`，需差异化处理。

### Alternatives Considered

- 一次性全仓翻译后统一修复
  - 否决原因：回归面太大，难以定位锚点和链接问题。
- 仅翻译 Markdown，忽略 HTML、SVG
  - 否决原因：不满足“完全翻译”的目标。
- 先改路径或文件名为中文再同步文案
  - 否决原因：与“尽量不改路径和资源文件名”的约束冲突，破坏链接风险最高。

### Why Chosen

- 推荐方案最符合现有约束，且最适合文档仓库的可验证渐进式交付。
- 把兼容规则前置，能避免批量翻译建立在未验证机制之上。
- 对 SVG 与 HTML 分类处理可以在“完整性”与“安全性”之间取得平衡，同时不放弃最终“零英文可见资产”的目标。

### Consequences

- 项目会经历一段阶段性中英混合状态，直到所有批次完成。
- 需要额外维护术语表、白名单和例外清单。
- 高风险 SVG 被正式纳入本期工作量，整体成本和工期都会上升。
- 本期结束时不允许存在待重绘且仍含可见英文的 SVG。

### Follow-ups

- 建立并维护术语表、本地化风格指南、例外 schema。
- 增加自动化扫描脚本或最小验证脚本，支持残留英文、链接、锚点与乱码检查。
- 对已完成重绘或替代的高风险 SVG 记录实现说明，供后续维护使用。

## Available-Agent-Types Roster

- `planner`：拆分阶段、定义交付物、维护批次计划。
- `architect`：约束建模、锚点与链接稳定性策略、HTML 与 SVG 风险边界。
- `critic`：审查计划完整性、可验证性、例外处理是否充分。
- `explore`：盘点文件、统计英文残留、定位链接和锚点敏感点。
- `executor`：执行翻译、编码修复、文档与资源编辑。
- `verifier`：链接检查、乱码检查、残留英文扫描、抽检验证。
- `writer`：润色中文表达、统一语气、维护术语表与说明文档。
- `style-reviewer`：检查术语统一、格式一致、标题风格一致。
- `qa-tester`：对 HTML、SVG 和关键入口做人工或半自动可视验证。
- `code-simplifier`：用于收口阶段清理冗余说明或重复术语，不改变含义。

## Follow-up Staffing Guidance

### Ralph 路径

- 适用场景：希望单线程、强一致、逐阶段闭环推进。
- 推荐分工：
  - `planner` 与 `architect` 先补全术语表、锚点兼容策略和例外 schema
  - `executor` 逐阶段实施
  - `verifier` 每阶段结束验证
  - `writer` 在阶段收口时润色高权重入口
- 推荐顺序：
  1. 基线盘点
  2. 兼容策略与术语表
  3. `README.md` 与 `CLAUDE.md` 机制试点
  4. Markdown 分目录批次
  5. HTML
  6. SVG
  7. 仓库级收口验证
- 推荐推理强度：
  - 规划与架构：high
  - 执行翻译：medium/high
  - 验证：high

### Team 路径

- 适用场景：希望并行推进多个目录或资源类型，缩短总工期。
- 推荐并行车道：
  - Lane A：入口与规则
    - `README.md`、`CLAUDE.md`、术语表、风格指南、例外 schema
  - Lane B：Markdown 主目录批次 1
    - `tutorial/`、`best-practice/`、`tips/`
  - Lane C：Markdown 主目录批次 2
    - `development-workflows/`、`implementation/`、`orchestration-workflow/`
  - Lane D：Markdown 主目录批次 3
    - `agent-teams/`、`reports/`、`videos/`、`changelog/`
  - Lane E：HTML、SVG 盘点、分类与资产处理
- Team 约束：
  - 所有 lane 共用同一术语表
  - 共享例外白名单与 schema
  - 禁止并行修改同一文件
  - 批量目录 lane 只有在机制试点验证通过后才能启动
  - 每个 lane 完成后必须交给统一 `verifier` 做合流验证
- 推荐推理强度：
  - Lane lead：high
  - 批量翻译执行：medium
  - 合流验证：high

## Team Verification Path

- 第一步：统一基线
  - 由 `explore` 与 `verifier` 先生成全仓英文残留、乱码、链接和入链锚点基线，作为团队共同参照。
- 第二步：机制试点验证
  - 对 `README.md` 与 `CLAUDE.md` 验证：
    - 旧锚点兼容
    - 手写目录跳转
    - 白名单规则固定
    - 链接检查有效
- 第三步：lane 内验证
  - 每个 lane 完成后独立运行：
    - 残留英文扫描
    - 链接检查
    - 编码异常扫描
    - 代表文件抽检
- 第四步：合流验证
  - 合并 lane 成果后，由集中 `verifier` 执行仓库级检查：
    - 全部相对链接
    - 全部入口页
    - 目录索引页
    - 入链锚点兼容
    - HTML 渲染检查
    - SVG 可视抽检
- 第五步：术语一致性复核
  - `writer` 与 `style-reviewer` 对高频术语做全仓一致性审校。
- 第六步：发布前审阅
  - 对 `README.md`、`CLAUDE.md`、每个主目录代表页进行最终人工阅读。
- 第七步：证据归档
  - 输出最终验证报告，至少包含：
    - 已翻译文件范围
    - 合理保留英文白名单
    - 已完成重绘或替代的 SVG 清单
    - 链接、锚点与编码验证结果
    - 剩余风险说明
