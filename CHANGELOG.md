# Changelog

All notable changes to this project will be documented in this file.

## [1.1.0] - 2026-02-23

### Added

- `install_yazi()` — terminal file manager with `file(1)` dependency check, brew/apt/dnf support, and GitHub binary fallback for Linux/macOS without sudo
- `install_wezterm()` — GPU-accelerated terminal emulator with brew (macOS), apt/dnf (Linux), and AppImage fallback without sudo
- Pinned versions: `YAZI_VERSION=v26.1.22`, `WEZTERM_VERSION=20240203-110809-5046fc22`
- yazi and wezterm entries in `--check` dry-run mode
- yazi and wezterm in post-install verification summary

## [1.0.2] - 2026-02-23

### Fixed

- CRLF line endings breaking zsh on WSL (`fix_line_endings()`, `strip_cr()`, `fix_git_autocrlf()`)
- `--check` mode for marker-based targets (file-with-marker pattern)

### Changed

- Set default shell to zsh inside tmux via `TMUX_DEFAULT_SHELL` block in `tmux.conf.local`
- Use gitmoji shortcodes in commit convention examples

## [1.0.1] - 2026-02-20

### Added

- Initial release: full environment installer (`install.sh`)
- zsh + Oh My Zsh + Powerlevel10k + zsh-autosuggestions + zsh-syntax-highlighting
- tmux + oh-my-tmux with local config
- nvm + Node.js LTS
- uv with custom venv aliases (`uv activate/create/rm/env`)
- Bash-to-zsh handoff (no `chsh` required)
- Shared shell config (`~/.config/shell/common.sh`)
- Cache symlinks to `/local` for heavy directories
- `--check` dry-run and `--force` re-run modes
- Version tracking via `~/.config/shell/install-version`
- GitHub Action for auto-pack and release on version bump

[1.1.0]: https://github.com/yuanming-heygen/one-shot-install/releases/tag/v1.1.0
[1.0.2]: https://github.com/yuanming-heygen/one-shot-install/releases/tag/v1.0.2
[1.0.1]: https://github.com/yuanming-heygen/one-shot-install/releases/tag/v1.0.1
