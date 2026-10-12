# Global Agent Instructions

- Use `agent-browser` for anything that needs a real browser (screenshots, forms, logins, testing web apps)
- If the project runs under `d3k`, that is the dev server: check errors, logs, and browser state with `d3k` (e.g. `d3k errors --context`) instead of asking me to paste output.
- Lockfile merge conflicts: delete the lockfile and regenerate it with the package manager's install command.
- TypeScript: don't cast to `any`.
- Don't add speculative defensive checks or try/catch blocks.
- To install an MCP server, check the current docs for the tool you're running in: [Claude Code](https://code.claude.com/docs/en/mcp#installing-mcp-servers), [Codex](https://developers.openai.com/codex/mcp), [OpenCode](https://opencode.ai/docs/mcp-servers/).
