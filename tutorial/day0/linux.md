# Linux 安装

[返回第 0 天](README.md)

## 前置要求

你需要 **Node.js v18 或更高版本**以及 **npm**。

## 第 1 步：安装 Node.js

### 方案 A：通过 nodejs.org 下载页配合 fnm 安装（推荐）

**fnm**（Fast Node Manager）是 Node.js 官方推荐的工具。它速度快、轻量，而且如果以后需要切换 Node 版本也很方便。

1. 打开浏览器，访问 [nodejs.org/en/download](https://nodejs.org/en/download)。

2. 你会看到一排下拉框，内容类似：**"Get Node.js® vXX.XX.X (LTS) for __ using __ with __"**。请按下面设置：

   | 下拉项 | 选择 |
   |----------|--------|
   | Version | **vXX.XX.X (LTS)**，保持默认 LTS 版本，不要修改 |
   | OS | **Linux** |
   | Package Manager | **fnm**（位于 "Recommended (Official)" 下） |
   | Package Format | **npm**，保持默认即可 |

3. 页面会显示需要执行的准确命令。打开终端并复制粘贴这些命令。它们大致会像这样：

   ```bash
   # Step 1 - Install fnm
   curl -fsSL https://fnm.vercel.app/install | bash

   # Step 2 - Restart your terminal or reload your shell profile
   source ~/.bashrc   # or: source ~/.zshrc (if you use zsh)

   # Step 3 - Install Node.js
   fnm install 24   # The page will show the exact version number
   ```

   > 上面的版本号可能不同，请始终以网站显示的版本为准。

4. **关闭并重新打开终端**（或者执行上面的 `source` 命令），这样 `fnm`、`node` 和 `npm` 才会生效。

> **为什么选 fnm？** 它在 Node.js 下载页里属于 "Recommended (Official)"。和 nvm 一样，它会把 Node 安装到你的主目录里，因此全局安装 npm 包时通常不需要 `sudo`。但 fnm 更快（它用 Rust 编写），并且在 Windows、macOS 和 Linux 上的使用方式都一致。

### 方案 B：使用你的发行版包管理器

这种方式更快，但安装到的 Node.js 版本可能偏旧。**安装后请务必检查版本**，如果低于 v18，请改用方案 A。

**Ubuntu / Debian：**

```bash
sudo apt update
sudo apt install -y nodejs npm

# Check the version
node --version   # Must be v18 or higher
```

**Fedora：**

```bash
sudo dnf install -y nodejs npm
```

**Arch Linux：**

```bash
sudo pacman -S nodejs npm
```

### 方案 C：NodeSource（通过 apt 安装最新 LTS，不使用 nvm）

适合希望在 Ubuntu / Debian 上安装最新 LTS，但又不想使用 nvm 的用户：

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
```

## 第 2 步：验证 Node.js

```bash
node --version
npm --version
```

这两个命令都应该输出版本号。`node --version` 必须显示 v18.x 或更高版本。

## 第 3 步：安装 Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

> **遇到权限错误？**
> - 如果你使用的是 **fnm** 或 **nvm**：通常不应该出现这个问题。请检查它是否已经生效（`which node` 应该指向你主目录中的路径，而不是 `/usr/...`）。
> - 如果你使用的是系统级安装：要么执行 `sudo npm install -g @anthropic-ai/claude-code`，要么修复 npm 全局目录权限：
>   ```bash
>   mkdir -p ~/.npm-global
>   npm config set prefix '~/.npm-global'
>   echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
>   source ~/.bashrc
>   ```

## 第 4 步：验证 Claude Code

```bash
claude --version
```

你应该会看到 Claude Code 的版本号。然后回到 [README.md](README.md) 完成认证设置。

---

## 说明

- **WSL（Windows Subsystem for Linux）**：这份指南在 WSL 中同样适用，直接在你的 WSL 终端里按步骤执行即可。
- **PATH 问题**：如果安装后找不到 `claude`，请确认 npm 的全局 `bin` 目录已经加入 PATH。运行 `npm config get prefix`，然后把该路径下的 `bin/` 子目录加入你的 PATH。
