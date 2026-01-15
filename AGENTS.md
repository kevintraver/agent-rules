# Global Agent Instructions

## System Tools

- Use `rg` (ripgrep) instead of `grep` for searching files and content
- Use `fd` instead of `find` for finding files and directories
- Use `eza` instead of `ls` for listing files and directories
- Use `bat` instead of `cat` for displaying file contents
- Use `sd` instead of `sed` for find and replace

## Markdown Rendering

- When rendering markdown files on the CLI, use `glow` (Charm CLI tool)
- Command pattern: `glow <file>.md`
- Options: `-s dark` for dark theme, `-w <width>` for width control

## Screenshots & Terminal Output

- When creating CLI/terminal screenshots, use `freeze` (Charm CLI tool)
- Command pattern: `<command> | freeze -o <output>.png`
- Example: `glow file.md | freeze -o screenshot.png`

## Code Generation Guidelines

- Never use dynamic imports (e.g., `await import(...)`) unless explicitly requested
- Never cast to `any` type
- Do not add extra defensive checks or try/catch blocks

## Development Servers

- Only start development servers when explicitly requested by the user.
