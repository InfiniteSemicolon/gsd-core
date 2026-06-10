---
type: Fixed
pr: 998
---
Claude Code plugin installs now create the canonical `~/.claude/gsd-core` path that bundled agents, commands, and prompt templates `@`-include. A marketplace plugin install never runs `bin/install.js` (the step that populates that directory), so every `@~/.claude/gsd-core/...` include resolved to nothing and gsd agents failed (e.g. the executor reporting empty plugin paths). A new SessionStart hook (`gsd-ensure-canonical-path.js`) makes `~/.claude/gsd-core` a real directory whose immutable bundled subdirs are symlinked to the plugin's `gsd-core/` tree; it is a no-op in classic installs, preserves user files, and self-heals after `claude plugin update`. (#997)
