---
description: 研究并分析功能可行性 - GO/NO-GO 决策闸门
argument-hint: "<feature-slug>"
---

## 用户输入

```text
$ARGUMENTS
```

你 **必须** 解析用户输入，提取 feature slug（`rpi/` 下的文件夹名）。

**期望输入格式**：`rpi/{feature-slug}/REQUEST.md`

## 目的

该命令会在规划开始前，对功能请求进行完整研究与分析。它是一个关键的 GO/NO-GO 闸门，用来判断这个功能想法是否值得进入详细规划。

**前置条件**：
- 功能目录存在于 `rpi/{feature-slug}/`
- 功能请求文件存在于 `rpi/{feature-slug}/REQUEST.md`

**输出位置**：`rpi/{feature-slug}/research/RESEARCH.md`

**这是 RPI 工作流第 2 步**。

## 研究目标

- 评估产品价值与用户收益
- 评估技术可行性与复杂度
- 识别风险、阻塞点和替代方案
- 给出明确的 GO / NO-GO 建议

## 阶段

1. 读取 `REQUEST.md` 与项目宪章
2. 用 `requirement-parser` 提取结构化需求
3. 用 `product-manager` 做产品分析
4. 用 `Explore` 深度探索代码现状
5. 用 `senior-software-engineer` 评估技术可行性
6. 用 `technical-cto-advisor` 做战略评估
7. 用 `documentation-analyst-writer` 生成 `RESEARCH.md`

## 关键要求

- 如果需求存在关键歧义，必须先停下并向用户提问
- 技术可行性判断必须基于真实代码探索，而不是假设
- 报告必须包含风险、理由和建议的下一步

## 输出内容

最终报告至少应包含：
- 功能概览
- 需求摘要
- 产品分析
- 技术发现
- 技术分析
- 战略建议
- GO / NO-GO 结论
- 下一步

## 下一步

若结论为 GO，继续执行：

```bash
/rpi:plan "{feature-slug}"
```

## 完成后动作

完成研究后，始终提示用户运行：

```text
/compact
```

以压缩对话并保留研究结论。
