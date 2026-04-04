### **CLI Commands & Flags**

For all available commands and flags, see the [official docs](https://code.claude.com/docs/en/cli-reference).

|  Command  |  Descrption  |
| -- | -- |
|`claude` / `claude "my prompt"` | Start a new Claude Code session, optionally with an initial prompt. |
| `claude -p "my prompt"` | Query Claude Code with "my prompt" and quit session once it's done (no ongoing session).|
`claude -c` | Continue most recent session.
`claude --agent DocsExplorer` | Start a new session with a custom agent (instead of the default one).
`claude --allowedTools "Read" "Write"` | Skip permission confirmation dialog for specified permissions.
`claude --disallowedTools "Write"` | Disallow certain tools (specified tools are removed from Claude Code's context => it doesn't know about them).
`claude --dangerously-skip-permissions` | Skip ALL permissions confirmation dialogs. Use with great caution!
`claude --append-system-prompt "Always check if redundant code can be deleted"` | Append an instruction to the default system prompt. Can be used as session-specific alternative to instructions placed in `CLAUDE.MD`.
`claude --system-prompt "You are a React.js expert"` | Replace the entire default system prompt with a custom one.
`claude --model opus` | Sets the default model for the current session. Can be changed in the session via `/model`, or generally via settings (see below). For valid options, see the [official list](https://code.claude.com/docs/en/model-config#model-aliases).
`claude --permission-mode plan` | Start in plan mode (default is *"default"* mode where Claude Code asks for permissions).
`claude --remote "Add dark mode"` | Start a remote (web) session.

### **Claude Code Interaction**

When inside a Claude Code session, you can use the following shortcuts for additional control. For all available shortcuts and commands, see the [official docs](https://code.claude.com/docs/en/interactive-mode).

| Interaction | Description |
| -- | -- |
`SHIFT + ENTER` / `OPTION + ENTER` / `CTRL + J` | Enter new line. Exact command depends on platform and terminal software used.
`SHIFT + TAB` | Switch through different modes ("default", "write permissions", "plan").
`CTRL + C` | Cancel current input or generation.
`ESC` | Cancel current generation (can be used to inject a new prompt into an ongoing task).
`ESC + ESC` | Restore the code prior to the last action performed by Claude Code.
`OPTION + P` / `ALT + P | Switch model. Alternative to `/model` which can be useful if you already entered a prompt.
`ARROW` keys (left / right / top / down) | Cycle through options or questions (left / right) or past message (up / down).
`CTRL + O` | Toggle verbose output (more / less details).
`CTRL + B` | Move task to background. Important: Claude Code also automatically moves tasks (e.g., exploration tasks) to the background and it's typically quite smart about that.
`CTRL + V` / `CMD + V` / `ALT + V | Insert text or image into prompt. The exact shortcut depends on your platform and terminal.

### Claude Commands
|  Command  |  Descrption  |
| -- | -- |
`/help` | List available commands and get usage help.
`/model` | Choose the active model for the current session.
`/clear` | Clear session context window (i.e., start a new session, effectively).
`/compact` | Compact (summarize) current session context history and clear it thereafter.
`/config` | Open interactive settings menu.
`/context` | View statistics about current context window & context usage.
`/usage` | View current usage for your active plan (i.e., how much usage remains until the next reset). For more details about plans and usage, see the official [help pages](https://support.claude.com/en/articles/11145838-using-claude-code-with-your-pro-or-max-plan).
`/init` | Analyze project and create initial `CLAUDE.MD` file (covered later).
`/mcp` | View and manage installed MCP servers.
`/permissions` | View and update / change permissions.
`/rewind` | Rewind (undo) to earlier point in conversation, same as `ESC + ESC`.
`/statusline` | Configure the Claude Code status line.

