# Global Agent Instructions

- Use `agent-browser` for anything that needs a real browser (screenshots, forms, logins, testing web apps)
- If a public site fails to load in agent-browser with a connection error, use the `adguard-dns` skill before trying anything else.
- Install agent skills with `npx skills add <package>` (e.g. `npx skills add vercel-labs/agent-skills`), not by cloning or copying skill folders by hand. Use `npx skills find`, `update`, and `remove` to search for, update, and uninstall them.
- Lockfile merge conflicts: delete the lockfile and regenerate it with the package manager's install command.
- zsh: don't start an unquoted word with `=` (e.g. `echo ====`). zsh treats `=word` as a command lookup and aborts the whole line if it finds none. Quote it or use `---` instead.
- zsh: quote any argument containing `*`, `?`, or `[` (e.g. `grep --include='*.ts'`, `find . -name '*.md'`). zsh expands globs in every word, including flags, and aborts the whole line with `no matches found` if nothing matches.
- fnox: shell secrets come from fnox's global config (`~/.config/fnox/config.toml`), which caches values from a 1Password Environment. After a value changes in 1Password, run `fnox sync -g -f -s op`, then open a new shell. Always pass `-g`: without it, fnox writes a `fnox.toml` into the current directory. To drop a key deleted from 1Password, run `fnox remove -g KEY`. Never print secret values.
- `grilling`, `grill-me`, and `interview-me` skills: ask questions with your native question tool (e.g. `AskUserQuestion`, `request_user_input`) instead of markdown. Put your recommended answer or guess first.
