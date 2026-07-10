# 安装指南 — 在 WSL 上使用 Claude for Science

YouTube 视频：https://youtu.be/DntCMpE7vtA?si=G9wi3hatOJOCa6Ee

## 步骤

1. **确认资格**
   Claude Science 目前处于测试阶段（beta），适用于 Pro、Max、Team 和 Enterprise 套餐。如果您使用的是 Team/Enterprise 账户，请让管理员为您的组织启用 Claude Science。

2. **更新 WSL**（在 Windows 端的 PowerShell 中执行）
   ```powershell
   wsl --update
   wsl -l -v
   ```
   请确保使用的是 WSL2，并搭配 Ubuntu 等发行版。

3. **下载 Linux 二进制文件**（在 WSL 终端中执行）
   ```bash
   curl -LO https://downloads.claude.ai/claude-science/latest/linux-x64
   mv linux-x64 claude-science
   ```

4. **安装依赖项**
   ```bash
   sudo apt update && sudo apt install -y bubblewrap
   ```
   安装完成后，运行以下命令验证：
   ```bash
   bwrap --version
   ```
   然后安装：
   ```bash
   sudo apt-get install -y socat
   ```

5. **赋予二进制文件可执行权限并启动**
   ```bash
   chmod +x claude-science
   ./claude-science
   ```
   首次启动时，使用您的 Anthropic 账户（Pro/Max/Team/Enterprise）登录 —— 身份验证很可能通过浏览器完成（与 Claude Code 类似）。

6. **配置计算资源访问**（可选，根据您的需求）
   - 若使用现有的 HPC 集群：在 WSL 中配置您的 SSH 密钥（`~/.ssh/`），以连接到登录节点（login node）。
   - 若使用按需计算资源：关联您的 Modal 账户。

7. **连接您的科研工具**
   Claude Science 通过 NVIDIA 的 BioNeMo Agent Toolkit 与专业模型（Evo 2、Boltz-2、OpenFold3）集成 —— 这些连接器在应用启动后可从界面中进行配置。

8. ⚠️ **一次性登录链接**
   登录链接是一次性密码，有效期为 3 分钟 —— 如果在打开之前已过期，请使用以下命令重新生成：
   ```bash
   claude-science url
   ```
   页面打开并完成身份验证后，该标签页将保持连接状态，直到守护进程（daemon）重启。`pidIsOperonDaemon` 警告是无害的（只是 `operon stop` 内部进程检测的一个小问题 —— 不影响正常使用）。
