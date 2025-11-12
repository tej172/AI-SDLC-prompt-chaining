# Clone this repository using VS Code's Integrated Terminal (Windows, macOS, Linux)

This guide shows how to clone the repository inside VS Code using the built-in terminal.

Repository URL:

- HTTPS: https://github.com/pengbin2015/AI-SDLC-prompt-chaining.git
- SSH: git@github.com:pengbin2015/AI-SDLC-prompt-chaining.git

## Prerequisites

- Visual Studio Code installed: https://code.visualstudio.com/
- Git installed: https://git-scm.com/downloads

## Steps

1) Open a terminal in VS Code
- Menu: Terminal > New Terminal
- Shortcut: Ctrl+` (Windows/Linux) or Cmd+` (macOS)

2) Choose the shell for your OS
- Windows: PowerShell (default in VS Code)
- macOS/Linux: bash or zsh

3) Navigate to the parent folder where you want the project

- Windows (PowerShell):
```powershell
New-Item -Type Directory -Path "$HOME\Projects" -Force | Out-Null
Set-Location "$HOME\Projects"
```

- macOS/Linux (bash/zsh):
```bash
mkdir -p ~/Projects
cd ~/Projects
```

4) Clone the repository (pick HTTPS or SSH)

- Windows (PowerShell):
```powershell
# HTTPS
git clone https://github.com/pengbin2015/AI-SDLC-prompt-chaining.git
# SSH
git clone git@github.com:pengbin2015/AI-SDLC-prompt-chaining.git
```

- macOS/Linux (bash/zsh):
```bash
# HTTPS
git clone https://github.com/pengbin2015/AI-SDLC-prompt-chaining.git
# SSH
git clone git@github.com:pengbin2015/AI-SDLC-prompt-chaining.git
```

5) Enter the project and verify the remote

- Windows (PowerShell):
```powershell
Set-Location "AI-SDLC-prompt-chaining"
git remote -v
```

- macOS/Linux (bash/zsh):
```bash
cd AI-SDLC-prompt-chaining
git remote -v
```