# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

omalarkey2 is a personal setup installer that copies [omarchy](https://omarchy.org) configs to `~/.config/` and installs missing CLI tools. The main deliverable is the `install` bash script.

## Testing the installer

There is no automated test suite. To test:

```bash
bash install          # run the full installer interactively
bash -n install       # syntax check only
```

## Architecture

### `install` (single script)

The installer runs in sequence:

1. **Bootstrap** — detects a package manager (brew/pacman/apt-get/dnf/yum); installs `gum` if missing
2. **Configs** — copies `omarchy/config/{btop,ghostty,git,lazygit,opencode,tmux}` to `~/.config/`, backing up any existing non-symlink dirs to `~/.omalarkey-backups/{iso_datetime}/`
3. **Tools** — checks which recommended/optional tools are missing, presents a `gum choose` multi-select (recommended tools pre-selected), then installs via PM batch or custom curl installers

Key internal functions:

- `pkg_name(tool, pm)` — maps tool names to package manager package names (returns empty if unavailable for that PM)
- `custom_install_cmd(tool)` — returns a self-contained bash snippet for tools not in a PM (starship, zoxide, lazydocker, lazygit, try)
- `is_installed(tool)` — handles command name differences (e.g. neovim→nvim, ripgrep→rg, fd→fdfind)

### `bin/` (theme management scripts)

Local overrides/extensions of omarchy's theme commands. All scripts look up themes from two locations: `~/.config/omarchy/themes/` (user-installed) and `$OMARCHY_PATH/themes/` (built-in, defaults to `~/.local/share/omarchy/themes/`).

- `omarchy-theme-list` — lists all available themes, formatted as title-case with spaces
- `omarchy-theme-current` — prints the active theme name, formatted the same way
- `omarchy-theme-set <name>` — activates a theme: merges built-in + user theme dirs into `~/.config/omarchy/current/theme/`, runs `omarchy-theme-set-templates`, calls `omarchy-hook theme-set`
- `omarchy-theme-set-templates` — processes `.tpl` files in `omarchy/default/themed/` and `~/.config/omarchy/themed/` using color variables from `colors.toml`; supports `{{ key }}`, `{{ key_strip }}`, `{{ key_rgb }}` substitutions
- `omarchy-theme-install <git-url>` — clones a theme repo into `~/.config/omarchy/themes/` and activates it
- `omarchy-theme-remove [name]` — removes a user-installed theme (interactive `gum choose` if no arg)
- `omarchy-theme-refresh` — re-applies the current theme (reruns `omarchy-theme-set` with the saved theme name)
- `omarchy-theme-update` — `git pull` on all git-cloned themes in `~/.config/omarchy/themes/`

### `omarchy/` submodule

Upstream omarchy project. Key paths used by the installer:

- `omarchy/config/` — configs copied to `~/.config/`
- `omarchy/default/` — symlinked to `~/.local/share/omarchy/default`

## Bash conventions (from `omarchy/AGENTS.md`)

- Shebang: `#!/bin/bash` (not `#!/usr/bin/env bash`)
- Indent: 2 spaces, no tabs
- Conditionals: `[[ ]]` for strings/files, `(( ))` for numbers
- In `[[ ]]`: don't quote variables; quote string literals in comparisons
- Quote paths with spaces rather than escaping with `\`
- Prefer `awk` over `sed` for text transforms — macOS ships BSD sed which doesn't support GNU extensions like `\u` (uppercase next char); `awk` with `toupper()` is portable
