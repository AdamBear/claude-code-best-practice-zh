---
description: 执行带验证闸门的分阶段实施
argument-hint: "<feature-slug> [--phase N] [--validate-only]"
---

## 用户输入

```text
$ARGUMENTS
```

你 **必须** 解析用户输入，提取 feature slug（`rpi/` 下的文件夹名）。

## 目的

该命令根据规划文档分阶段执行功能实现。它会编排专门代理、执行验证闸门，并确保整个实施过程持续符合项目宪章。

**前置条件**：
- 功能目录存在于 `rpi/{feature-slug}/`
- 规划已完成（`rpi/{feature-slug}/plan/PLAN.md` 存在）

**输出位置**：`rpi/{feature-slug}/implement/`

**这是 RPI 工作流第 4 步**（真正执行实现的最后一步）。

## 标志

- `--phase N`：执行指定阶段（1-8），省略时从第 1 阶段开始
- `--validate-only`：只验证当前阶段，不执行实现
- `--skip-validation`：跳过验证闸门继续执行（谨慎使用）

## 可用代理

### 实现代理
- `senior-software-engineer`：负责所有实现任务

### 支持代理
- `Explore`：实现前探索代码
- `code-reviewer`：做代码审查和质量验证
- `constitutional-validator`：按项目宪章做一致性校验
- `documentation-analyst-writer`：生成或更新文档

## 阶段循环

每个阶段都遵循以下顺序：
1. 代码发现（Explore）
2. 实现（senior-software-engineer）
3. 自我验证
4. 代码审查（code-reviewer）
5. 用户验证闸门
6. 更新文档

## 实施要求

- 修改前先理解现有代码模式
- 遵守项目宪章与领域规则
- 为新增功能补测试
- 做好日志与错误处理
- 每个阶段结束后更新状态

## 用户验证闸门

该步骤 **必须暂停并等待用户决定**。

用户可给出：
- **PASS**：进入下一阶段
- **CONDITIONAL PASS**：记录问题后继续
- **FAIL**：修复后重新验证

## 质量闸门

每个阶段完成前必须满足：
- 所有交付物已实现
- Lint 通过
- 测试通过
- 构建成功
- 代码审查通过
- 获得用户验证
- 文档已更新

## 命令示例

```bash
/rpi:implement "my-feature"
/rpi:implement "my-feature" --phase 3
/rpi:implement "my-feature" --phase 2 --validate-only
```

## 备注

- Bug 修复或很小的改动不适合使用该命令
- 不要跳过验证闸门
- 卡住时应升级给用户，而不是带着不确定性继续

## 完成后动作

在完成实现后，始终提示用户运行：

```text
/compact
```

以压缩对话并保留实施状态。
