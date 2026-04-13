---
description: 为功能创建完整的规划文档
argument-hint: "<feature-slug>"
---

## 用户输入

```text
$ARGUMENTS
```

你 **必须** 解析用户输入，提取 feature slug（`rpi/` 下的文件夹名）。

## 目的

该命令为一个功能请求创建完整的规划文档，在功能的 RPI 目录中生成详细规格、技术设计和实施计划。

**前置条件**：
- 功能目录存在于 `rpi/{feature-slug}/`
- 研究已完成，且 `rpi/{feature-slug}/research/RESEARCH.md` 存在

**输出位置**：`rpi/{feature-slug}/plan/`

**这是 RPI 工作流第 3 步**（Research 通过后的规划阶段）。

## 产出文件

- `pm.md`：产品需求
- `ux.md`：用户体验设计
- `eng.md`：技术规格
- `PLAN.md`：实施路线图

## 工作流程

1. 加载研究报告与项目宪章
2. 理解功能需求
3. 分析技术需求与依赖
4. 设计高层架构与 API 契约
5. 拆解为 3-5 个实施阶段
6. 生成四份规划文档
7. 检查输出是否完整且无占位内容

## 代理分工

- `product-manager`：生成 `pm.md`
- `ux-designer`：生成 `ux.md`
- `senior-software-engineer`：生成 `eng.md`
- `documentation-analyst-writer`：统一整理并生成最终文档

## 验证要求

- 四个文件都必须存在
- 每个文件都要内容完整、结构清晰
- `PLAN.md` 必须包含分阶段任务、依赖与验收标准
- 不允许残留占位文本

## 下一步

规划完成后，进入：

```bash
/rpi:implement "{feature-slug}"
```

## 完成后动作

完成规划后，始终提示用户运行：

```text
/compact
```

以压缩对话并保留规划决策。
