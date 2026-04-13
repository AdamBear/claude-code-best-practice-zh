# Windows 安装

[返回第 0 天](README.md)

---

**Node.js**
- 前往 [nodejs.org](https://nodejs.org)
- 点击 **"Download Node.js (LTS)"** 按钮，这会下载 `.msi` 安装程序
- 运行这个 `.msi` 文件，在安装向导中一路点击 **Next**
- 保持默认设置，点击 **Install**，等待安装完成

**验证 Node.js**
- 打开一个**新的**终端窗口（PowerShell 或 Windows Terminal），运行：
  ```powershell
  node --version
  npm --version
  ```

**Claude Code**
- ```powershell
  npm install -g @anthropic-ai/claude-code
  ```
- 如果遇到权限错误，请以**管理员身份**运行终端（右键 > Run as administrator）

**验证**
- ```powershell
  claude --version
  ```

---

现在回到 [README.md](README.md) 继续进行认证设置。
