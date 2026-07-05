# Installation Guide — Claude for Science on WSL

YouTube video: https://youtu.be/DntCMpE7vtA?si=G9wi3hatOJOCa6Ee

## Steps

1. **Check your eligibility**
   Claude Science is in beta, available for Pro, Max, Team, and Enterprise plans. If you're on a Team/Enterprise account, ask your admin to enable Claude Science for your organization.

2. **Update WSL** (in PowerShell, on the Windows side)
   ```powershell
   wsl --update
   wsl -l -v
   ```
   Make sure you're using WSL2 with a distribution such as Ubuntu.

3. **Download the Linux binary** from your WSL terminal
   ```bash
   curl -LO https://downloads.claude.ai/claude-science/latest/linux-x64 -o claude-science
   ```

4. **Install dependencies**
   ```bash
   sudo apt update && sudo apt install -y bubblewrap
   ```
   Once installed, verify with:
   ```bash
   bwrap --version
   ```
   Then install:
   ```bash
   sudo apt-get install -y socat
   ```

5. **Make the binary executable and launch it**
   ```bash
   chmod +x claude-science
   ./claude-science
   ```
   Sign in with your Anthropic account (Pro/Max/Team/Enterprise) on first launch — authentication likely happens via the browser (as with Claude Code).

6. **Configure compute access** (optional, depending on your needs)
   - For an existing HPC cluster: set up your SSH keys in WSL (`~/.ssh/`) to connect to your login node.
   - For on-demand compute: link your Modal account.

7. **Connect your scientific tools**
   Claude Science integrates with specialized models (Evo 2, Boltz-2, OpenFold3) via NVIDIA's BioNeMo Agent Toolkit — these connectors are configured from the app's interface once launched.

8. ⚠️ **One-time login link**
   The login link is a one-time password valid for 3 minutes — if it expires before you open it, regenerate one with:
   ```bash
   claude-science url
   ```
   Once the page is opened and authenticated, the tab stays connected until the daemon restarts. The `pidIsOperonDaemon` warning is benign (just an internal process-detection quirk for `operon stop` — it doesn't affect normal operation).
