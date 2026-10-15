# 🖥️ tmux Cheat Sheet

A quick reference for **tmux** (terminal multiplexer) — manage multiple terminal sessions, windows, and panes from a single screen.

> **Prefix key:** By default this is `CTRL + B`. In the tables below, `PREFIX` means *press `CTRL + B`, release, then press the next key*. Many users remap it to `CTRL + A` (see [Configuration](#configuration)).

For the full manual, see `man tmux` or the [official wiki](https://github.com/tmux/tmux/wiki).

---

## Installation

| Platform | Command |
| -- | -- |
| macOS (Homebrew) | `brew install tmux` |
| Debian / Ubuntu | `sudo apt install tmux` |
| Fedora / RHEL | `sudo dnf install tmux` |
| Arch | `sudo pacman -S tmux` |
| Check version | `tmux -V` |

---

## Sessions

A **session** is a collection of windows. You can detach from a session and it keeps running in the background.

| Command | Description |
| -- | -- |
| `tmux` | Start a new unnamed session. |
| `tmux new -s mysession` | Start a new named session (`mysession`). |
| `tmux ls` | List all running sessions. |
| `tmux attach` / `tmux a` | Attach to the most recent session. |
| `tmux attach -t mysession` | Attach to a specific named session. |
| `tmux kill-session -t mysession` | Kill a specific session. |
| `tmux kill-server` | Kill the tmux server and ALL sessions. |
| `PREFIX d` | Detach from the current session (it keeps running). |
| `PREFIX s` | Interactively list & switch between sessions. |
| `PREFIX $` | Rename the current session. |
| `PREFIX (` / `PREFIX )` | Switch to previous / next session. |

---

## Windows

A **window** is like a tab inside a session. Each window fills the screen and can be split into panes.

| Command | Description |
| -- | -- |
| `PREFIX c` | Create a new window. |
| `PREFIX ,` | Rename the current window. |
| `PREFIX w` | List & select windows interactively. |
| `PREFIX n` | Move to the next window. |
| `PREFIX p` | Move to the previous window. |
| `PREFIX 0`...`9` | Jump to window by number. |
| `PREFIX l` | Toggle to the last-active window. |
| `PREFIX &` | Kill the current window (asks to confirm). |
| `PREFIX f` | Find a window by name. |

---

## Panes

A **pane** is a split within a window — multiple shells visible side by side.

| Command | Description |
| -- | -- |
| `PREFIX %` | Split the current pane vertically (left / right). |
| `PREFIX "` | Split the current pane horizontally (top / bottom). |
| `PREFIX ←↑↓→` | Move to the pane in that direction (arrow keys). |
| `PREFIX o` | Cycle to the next pane. |
| `PREFIX ;` | Toggle to the last-active pane. |
| `PREFIX q` | Show pane numbers (then press a number to jump). |
| `PREFIX z` | Toggle zoom (fullscreen) for the current pane. |
| `PREFIX x` | Kill the current pane (asks to confirm). |
| `PREFIX {` / `PREFIX }` | Swap pane with the previous / next one. |
| `PREFIX SPACE` | Cycle through preset pane layouts. |
| `PREFIX !` | Break the current pane out into its own window. |
| `PREFIX CTRL + ←↑↓→` | Resize the current pane (hold `CTRL` + arrows). |

---

## Copy Mode (Scroll & Select)

Copy mode lets you scroll back through output and copy text.

| Command | Description |
| -- | -- |
| `PREFIX [` | Enter copy mode (then scroll with arrows / PageUp / PageDown). |
| `q` | Quit copy mode. |
| `SPACE` | Start selection (in copy mode). |
| `ENTER` | Copy the selection and exit copy mode. |
| `PREFIX ]` | Paste the most recent copy buffer. |
| `/` / `?` | Search forward / backward (in copy mode). |

> Tip: `vi` or `emacs` key bindings in copy mode are set via `setw -g mode-keys vi`.

---

## Miscellaneous

| Command | Description |
| -- | -- |
| `PREFIX ?` | List all key bindings (built-in help). |
| `PREFIX t` | Show a large clock. |
| `PREFIX :` | Open the tmux command prompt. |
| `tmux source-file ~/.tmux.conf` | Reload the config file without restarting. |

---

## Configuration

Place settings in `~/.tmux.conf`. Reload with `PREFIX :` then `source-file ~/.tmux.conf`.

```bash
# Remap prefix from CTRL+B to CTRL+A
unbind C-b                  # stop CTRL+B from being the prefix
set -g prefix C-a           # make CTRL+A the new prefix
bind C-a send-prefix        # press CTRL+A twice to pass it through to the shell

# Start windows and panes at 1, not 0
set -g base-index 1         # number windows starting at 1 (easier to reach keys)
setw -g pane-base-index 1   # number panes starting at 1 to match windows

# Enable mouse support (scroll, select, resize)
set -g mouse on             # let the mouse scroll, pick panes/windows, and drag to resize

# Use vi keys in copy mode
setw -g mode-keys vi        # navigate and select in copy mode with vi-style keys

# Increase scrollback buffer size
set -g history-limit 10000  # keep 10,000 lines of scrollback per pane (default is 2000)

# Intuitive split bindings (| and -)
bind | split-window -h      # PREFIX | splits left/right (vertical divider)
bind - split-window -v      # PREFIX - splits top/bottom (horizontal divider)

# Quick config reload with PREFIX r
bind r source-file ~/.tmux.conf \; display "Config reloaded!"  # reload config and show a confirmation message
```

---

## Common Workflow

```bash
# Start a named session for a project
tmux new -s webapp

# Split into editor + server + logs, then detach
#   PREFIX %   -> split vertically
#   PREFIX "   -> split horizontally
#   PREFIX d   -> detach (work keeps running)

# Later, reattach from anywhere
tmux attach -t webapp
```
