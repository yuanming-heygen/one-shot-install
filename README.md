# one-shot-install

A single-command shell environment installer for Linux and macOS. Sets up zsh, Oh My Zsh, Powerlevel10k, tmux, nvm, Node.js, and uv — without requiring sudo or changing your login shell.

Designed for shared servers where you can't run `chsh` or don't have root access.

## What Gets Installed

| Tool | Purpose |
|------|---------|
| [zsh](https://www.zsh.org/) | Shell (used via bash handoff, no `chsh` needed) |
| [Oh My Zsh](https://ohmyz.sh/) | Zsh framework |
| [Powerlevel10k](https://github.com/romkatv/powerlevel10k) | Zsh theme |
| [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) | Fish-like suggestions |
| [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) | Command highlighting |
| [oh-my-tmux](https://github.com/gpakosz/.tmux) | Tmux configuration |
| [nvm](https://github.com/nvm-sh/nvm) + Node.js LTS | Node version manager |
| [uv](https://github.com/astral-sh/uv) | Python package manager (with custom venv aliases) |

## Quick Start

### From a Gist / URL (standalone)

```bash
curl -fsSL <url-to-install-standalone.sh> | bash
```

### From the repo

```bash
git clone <repo-url>
cd one-shot-install
bash install.sh
```

### Options

```bash
bash install.sh --check   # Dry-run: show what would be done
bash install.sh --force   # Re-run even if current version is already installed
```

## How It Works

**No password, no `chsh`**: bash stays as your login shell. When you open an interactive terminal, bash automatically `exec`s into `zsh -l`. This is transparent — your shell experience is zsh, but no system configuration changes are needed.

**Config sourcing chain**:
```
~/.bash_profile → ~/.bashrc → ~/.config/shell/common.sh
~/.zshrc → ~/.config/shell/common.sh (also sources ~/.bashrc, guarded)
```

Shared settings (PATH, nvm, timezone, uv aliases) live in `~/.config/shell/common.sh` so both shells stay in sync.

**Idempotent**: every modification uses marker comments to prevent duplicate entries. Running the installer multiple times is safe. Version tracking (`~/.config/shell/install-version`) skips redundant re-runs automatically.

**Cache symlinks**: on machines with small home drives and a `/local` partition, heavy caches (uv, pip, huggingface, torch, npm, conda, triton) are symlinked to `/local/$USER/`.

## Custom uv Commands

The installer adds a `uv` wrapper function with extra subcommands for managing virtual environments in a shared location (`/local/$USER/.uv_venv/`):

```bash
uv create <name> [python_version]   # Create a new venv
uv activate <name>                  # Activate a venv
uv deactivate                       # Deactivate current venv
uv rm <name>                        # Remove a venv
uv env list                         # List available venvs
uv env path <name>                  # Print venv path
```

All other `uv` subcommands pass through to the real `uv` binary.

## Configuration

### Config files

| File | Description |
|------|-------------|
| `p10k.zsh` | Powerlevel10k prompt config. Replace with your own or run `p10k configure` after install. |
| `tmux.config.local` | oh-my-tmux local overrides. |

### Environment variable overrides

You can override config file paths before running the installer:

```bash
P10K_CONFIG_PATH=/path/to/my/p10k.zsh bash install.sh
TMUX_LOCAL_CONFIG_PATH=/path/to/my/tmux.conf.local bash install.sh
```

Or use URLs:

```bash
P10K_CONFIG_URL=https://example.com/p10k.zsh bash install.sh
TMUX_LOCAL_CONFIG_URL=https://example.com/tmux.conf.local bash install.sh
```

## Building the Standalone Script

`pack.sh` bundles `install.sh` and the config files into a single self-extracting script:

```bash
bash pack.sh > install-standalone.sh
```

The output base64-encodes each file and embeds them into a script that extracts to a temp directory and runs `install.sh`. Suitable for uploading to a gist for `curl | bash` usage.

## Requirements

- bash (to run the installer)
- curl or wget (for downloading tools)
- git (for cloning Oh My Zsh plugins; installed automatically if possible)
