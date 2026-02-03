# Global Agent Instructions

## Web Browsing

**Default: `agent-browser`** for web tasks including:

- Taking screenshots of rendered pages
- Filling forms, clicking elements, multi-step workflows
- Testing web applications
- Any task requiring browser state or login

**Use `firecrawl` only when:**

- Explicitly requested by the user
- Crawling multiple pages or entire sites
- Site mapping or link discovery

## Git Conflicts

If there's a conflict in a lockfile (`package-lock.json`, `pnpm-lock.yaml`, `yarn.lock`, `bun.lockb`), remove it and regenerate with the appropriate install command.

## Screenshots & Terminal Output

- When creating CLI/terminal screenshots, use `freeze`
- Command pattern: `freeze --execute "ls -la"`

## Code Generation Guidelines

- Typescript: Avoid casting to `any` type
- Do not add extra defensive checks or try/catch blocks

## Development Servers

- Only start development servers when explicitly requested by the user.

## Debugging & Diagnostics

- When asked to "look at logs", "check logs", "debug errors", or diagnose app issues, use the `mcp__dev3000__fix_my_app` tool if available
- This tool provides browser console logs and network errors from the running app

## MCP Servers

When asked to install an MCP server, consult the documentation:

- OpenCode: https://opencode.ai/docs/mcp-servers/
- Claude: https://code.claude.com/docs/en/mcp#installing-mcp-servers
- Codex: https://developers.openai.com/codex/mcp
