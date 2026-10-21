# Global Agent Instructions

- Use `agent-browser` for anything that needs a real browser (screenshots, forms, logins, testing web apps)
- Install agent skills with `npx skills add <package>` (e.g. `npx skills add vercel-labs/agent-skills`), not by cloning or copying skill folders by hand. Use `npx skills find`, `update`, and `remove` to search for, update, and uninstall them.
- Lockfile merge conflicts: delete the lockfile and regenerate it with the package manager's install command.
- TypeScript: don't cast to `any`.
- Don't add speculative defensive checks or try/catch blocks.
- My shell is zsh: never start an unquoted word with `=` (e.g. `echo ====`) — zsh expands `=word` to a command path and aborts the whole command line when it fails. Quote it or use `---` as a separator.
- `grilling` skill: ask questions with your native question tool (e.g. `AskUserQuestion`, `request_user_input`) instead of markdown.
