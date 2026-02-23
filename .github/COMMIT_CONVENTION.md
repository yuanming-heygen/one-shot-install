# Commit Message Convention

## Format

```
<emoji> [<scope>] <short description>

- <detail 1>
- <detail 2>
```

## Emojis

| Emoji | Code | Usage |
|-------|------|-------|
| ✨ | `:sparkles:` | New feature |
| 🐛 | `:bug:` | Bug fix |
| 📝 | `:memo:` | Documentation |
| ♻️ | `:recycle:` | Refactor |
| ⬆️ | `:arrow_up:` | Upgrade dependency / version bump |
| ⬇️ | `:arrow_down:` | Downgrade dependency |
| 🔧 | `:wrench:` | Configuration change |
| 🔒 | `:lock:` | Security fix |
| 🚀 | `:rocket:` | Performance improvement |
| 🎨 | `:art:` | Style / formatting |
| 🔥 | `:fire:` | Remove code or files |
| 🚑 | `:ambulance:` | Critical hotfix |
| ✅ | `:white_check_mark:` | Add or update tests |
| 📦 | `:package:` | Build / packaging |
| 🏗️ | `:building_construction:` | Architectural change |
| 🍱 | `:bento:` | Add or update assets |

## Examples

```
:sparkles: [uv] Add custom venv management aliases

- Add uv activate/deactivate/create/rm subcommands
- Add tab completion for zsh and bash
- Venvs stored in /local/$USER/.uv_venv/
```

```
:bug: [tmux] Fix oh-my-tmux config symlink overwrite

- Remove destructive ln -sf that overwrote tmux.conf
- Reload from tmux.conf.local path instead
```

```
:memo: [docs] Add README and CLAUDE.md

- Add project README with install instructions
- Add CLAUDE.md for Claude Code context
```

```
:arrow_up: [nvm] Bump nvm to v0.40.4

- Update NVM_VERSION pin
- No breaking changes
```

```
:wrench: [shell] Set default timezone to Asia/Singapore

- Append TZ export to shared shell config
```
