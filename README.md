# Omalarkey

You love your terminal. You've found [Omarchy](https://omarchy.org) and its beautifully
curated defaults, and you want that life. But your employer has handed you a MacBook,
an Ubuntu VM, or a CentOS box (all fine options, but just not what you want) — and
told you Arch is not an option.

Enter omalarkey.

This project brings Omarchy's excellent terminal defaults to wherever you're actually
forced to use: macOS, Ubuntu, CentOS/RHEL, and beyond. Same great tools. Same thoughtful
configs. Zero Arch required.

The name is a nod to Omarchy itself — close enough that you'll feel at home, different
enough to acknowledge the absurdity of the situation.

---

## What gets installed

**Configs** (leave it to the chef):

- All the opinionated defaults from Omarchy for your terminal
- Modern `bash` setup packed with productivity improvements and an elegant `starship`
- Omarchy's defaults for the following tools: `btop`, `ghostty`, `git`, `lazygit`,
  `opencode`, `tmux`
- Existing configs are backed up to `~/.omalarkey-backups/<timestamp>/` before anything
  is overwritten.

**Recommended tools** (pre-selected):

| Tool | What it does |
|---|---|
| [neovim](https://neovim.io) | Modern Vim |
| [tmux](https://github.com/tmux/tmux) | Terminal multiplexer |
| [starship](https://starship.rs) | Cross-shell prompt |
| [eza](https://eza.rocks) | `ls` but good |
| [fzf](https://github.com/junegunn/fzf) | Fuzzy finder |
| [bat](https://github.com/sharkdp/bat) | `cat` with syntax highlighting |
| [ripgrep](https://github.com/BurntSushi/ripgrep) | Fast grep |
| [fd](https://github.com/sharkdp/fd) | Fast find |
| [zoxide](https://github.com/ajeetdsouza/zoxide) | Smarter `cd` |
| [try](https://github.com/tobi/try) | fresh directories for every vibe |

**Optional tools** (you choose):

| Tool | What it does |
|---|---|
| [btop](https://github.com/aristocratos/btop) | TUI resource monitor |
| [lazydocker](https://github.com/jesseduffield/lazydocker) | TUI for Docker |
| [lazygit](https://github.com/jesseduffield/lazygit) | TUI for git |

---

## Installation

```bash
git clone --recurse-submodules https://github.com/jpiccari/omalarkey.git
cd omalarkey
bash install
```

---

## Terminal recommendation: Ghostty

If you have any say in your terminal emulator, use [Ghostty](https://ghostty.org).
It's fast, it's native, and the config Omarchy (and Omalarkey) ships for it is
excellent. It works especially well on macOS where other terminals feel like
afterthoughts or bloated with features.

---

## macOS: get a real Bash

macOS ships Bash 3.2 (from 2007, for licensing reasons). This project requires
**Bash 4.2+**.

```bash
brew install bash
```

To check what you have:

```bash
bash --version
```

---

## Theme management

The following omarchy scripts are patched to be posix-compliant and manage themes.
They are installed to `~/.local/bin/` and should mostly work (not well tested across
distros currently). At some point it would be ideal to see if we can get the changes
ported back into Omarchy and use the scripts directly (watch this space).

```bash
omarchy-theme-list          # see all available themes
omarchy-theme-current       # what's active
omarchy-theme-set <name>    # switch themes
omarchy-theme-install <url> # install a theme from a git repo
omarchy-theme-remove        # remove a user-installed theme
omarchy-theme-refresh       # re-apply the current theme
omarchy-theme-update        # git pull all installed themes
```

---

## Standing on the shoulders of giants

None of this exists without the open source community — the decades of contributors
who turned bare terminals into powerful creative environments, who kept the DIY
hacker spirit alive long after personal computing went corporate, and who kept giving
their best work away for free.

Omarchy, Neovim, tmux, starship, fzf, ripgrep, bat, eza, zoxide, lazygit, gum —
every tool in this stack is the result of someone scratching their own itch and
sharing the solution. Thank you.

---

## License

MIT. Do whatever you want with it — that's the point. For specific legal details
check the [LICENSE](LICENSE) file.
