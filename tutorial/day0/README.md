# 第 0 天：Claude Code 安装

这份指南会带你在自己的电脑上安装 Claude Code，并完成登录认证，以便开始使用它。

## 第 1 步：安装 Claude Code

请选择你的操作系统：

| 操作系统 | 指南 |
|----|-------|
| Windows | [windows.md](windows.md) |
| Linux | [linux.md](linux.md) |
| macOS | [mac.md](mac.md) |

先按照对应系统的指南完成安装，然后回到这里进行认证。

---

## 第 2 步：验证安装

完成系统对应的安装步骤后，确认一切运行正常：

```bash
node --version    # 应显示 v18.x 或更高版本
claude --version  # 应显示已安装的 Claude Code 版本
```

---

## 第 3 步：登录

<img src="assets/login.png" alt="Claude Code 登录界面" width="50%">

在终端中运行 `claude`。首次启动时，它会要求你选择登录方式。

### 方法 1：订阅账号（Claude Pro / Max）

- 选择 **Claude.ai account**
- 浏览器会打开，完成登录并授权
- 回到终端后，你就已经登录完成

### 方法 2a：API Key（团队邀请）

你的团队管理员会在 Anthropic 控制台中邀请你加入。

- 你会收到一封**邀请邮件**，接受邀请并创建你的 Anthropic 账号
- 在终端中运行 `claude`
- 选择 **Anthropic API Key**
- 你的密钥会在控制台中**自动生成**，无需手动配置
- Claude Code 会立即开始工作

### 方法 2b：API Key（你已经有密钥）

如果别人已经把密钥发给你了（通过 Slack、邮件等），或者你自己已经创建了密钥：

- 在终端中运行 `claude`
- 选择 **Anthropic API Key**
- 粘贴你的密钥（以 `sk-ant-` 开头）
- 该密钥会被**永久保存**，之后不会再次要求输入

---
