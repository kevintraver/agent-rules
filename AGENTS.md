# Global Agent Instructions

- Use `agent-browser` for anything that needs a real browser (screenshots, forms, logins, testing web apps)
- If the project runs under `d3k`, that is the dev server: check errors, logs, and browser state with `d3k` (e.g. `d3k errors --context`) instead of asking me to paste output.
- Lockfile merge conflicts: delete the lockfile and regenerate it with the package manager's install command.
- TypeScript: don't cast to `any`.
- Don't add speculative defensive checks or try/catch blocks.
- My shell is zsh: never start an unquoted word with `=` (e.g. `echo ====`) — zsh expands `=word` to a command path and aborts the whole command line when it fails. Quote it or use `---` as a separator.
