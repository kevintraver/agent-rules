# Global Agent Instructions

## Web Browsing

**Default: `agent-browser`** for web tasks including:

- Taking screenshots of rendered pages
- Filling forms, clicking elements, multi-step workflows
- Testing web applications
- Any task requiring browser state or login

For simple URL fetching and lookups, use `WebFetch`. For web searches, use `WebSearch`.

## Git Conflicts

If there's a conflict in a lockfile (`package-lock.json`, `pnpm-lock.yaml`, `yarn.lock`, `bun.lockb`), remove it and regenerate with the appropriate install command.

## Code Generation Guidelines

- Typescript: Avoid casting to `any` type
- Do not add extra defensive checks or try/catch blocks

## Development Servers

- Only start development servers when explicitly requested by the user.

## MCP Servers

When asked to install an MCP server, consult the documentation:

- OpenCode: https://opencode.ai/docs/mcp-servers/
- Claude: https://code.claude.com/docs/en/mcp#installing-mcp-servers
- Codex: https://developers.openai.com/codex/mcp

## TypeScript LSP Usage

Use the TypeScript Language Server Protocol (LSP) for accurate code navigation and understanding. Prefer LSP over text-based search when you need precise type information or symbol relationships.

### When to Use LSP

| Operation            | Use Case                                            |
| -------------------- | --------------------------------------------------- |
| `goToDefinition`     | Find where a function, type, or variable is defined |
| `findReferences`     | Find all usages of a symbol across the codebase     |
| `hover`              | Get type signatures and JSDoc documentation         |
| `documentSymbol`     | List all exports/functions/types in a file          |
| `workspaceSymbol`    | Search for a symbol by name across all files        |
| `goToImplementation` | Find concrete implementations of interfaces         |
| `incomingCalls`      | Find all callers of a function                      |
| `outgoingCalls`      | Find all functions called by a function             |

### Examples

```
# Find where a type is defined
LSP goToDefinition on `ReceptionistConfiguration` → packages/common/src/types/...

# Find all usages of a function
LSP findReferences on `createSupabaseServerClient` → all files using it

# Understand a function's signature
LSP hover on `generateKsuid()` → returns type info and description

# Trace call chains
LSP incomingCalls on `syncCallToAccount` → find all entry points
```

### Prefer LSP Over Text Search When

- You need the **exact definition** (not just string matches)
- You want **all references** including re-exports and type imports
- You need **type information** to understand function contracts
- You're **tracing call hierarchies** through the codebase
- You want to find **interface implementations**

Text search (Grep/Glob) is still useful for finding patterns, comments, or strings that LSP doesn't index.
