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

## Debugging with d3k

When the user asks to **check for errors**, **read logs**, **see what's happening in the browser**, **check the dev server**, or anything similar about the running app, use `d3k` CLI tools first instead of grepping files or asking the user to paste output.

Common commands:

| Phrase | Command |
|--------|---------|
| "any errors?" / "check for errors" | `d3k errors --context` |
| "read the logs" / "show me the logs" | `d3k logs -n 200` |
| "browser console" / "client logs" | `d3k logs --type browser` |
| "server logs" / "backend logs" | `d3k logs --type server` |
| "take a screenshot" / "what does the page look like" | `d3k agent-browser screenshot /tmp/d3k-current.png` |
| "click X" / "fill the form" / drive the page | `d3k agent-browser snapshot -i` then `click @e<id>` / `fill` |

Rules:

- Don't start a separate `npm run dev` / `bun dev` — d3k is the dev server.
- Use `d3k agent-browser` to drive the same browser session d3k is already monitoring (CDP-connected).
- For Next.js–specific introspection (component tree, routes), use `d3k next-browser` instead.
- Artifacts live under `~/.d3k/{project}/` (`d3k.log`, `logs/`, `screenshots/`, `session.json`).

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

## MCP Tools: code-review-graph

**IMPORTANT: This project has a knowledge graph. ALWAYS use the
code-review-graph MCP tools BEFORE using Grep/Glob/Read to explore
the codebase.** The graph is faster, cheaper (fewer tokens), and gives
you structural context (callers, dependents, test coverage) that file
scanning cannot.

### When to use graph tools FIRST

- **Exploring code**: `semantic_search_nodes` or `query_graph` instead of Grep
- **Understanding impact**: `get_impact_radius` instead of manually tracing imports
- **Code review**: `detect_changes` + `get_review_context` instead of reading entire files
- **Finding relationships**: `query_graph` with callers_of/callees_of/imports_of/tests_for
- **Architecture questions**: `get_architecture_overview` + `list_communities`

Fall back to Grep/Glob/Read **only** when the graph doesn't cover what you need.

### Key Tools

| Tool                        | Use when                                               |
| --------------------------- | ------------------------------------------------------ |
| `detect_changes`            | Reviewing code changes — gives risk-scored analysis    |
| `get_review_context`        | Need source snippets for review — token-efficient      |
| `get_impact_radius`         | Understanding blast radius of a change                 |
| `get_affected_flows`        | Finding which execution paths are impacted             |
| `query_graph`               | Tracing callers, callees, imports, tests, dependencies |
| `semantic_search_nodes`     | Finding functions/classes by name or keyword           |
| `get_architecture_overview` | Understanding high-level codebase structure            |
| `refactor_tool`             | Planning renames, finding dead code                    |

### Workflow

1. The graph auto-updates on file changes (via hooks).
2. Use `detect_changes` for code review.
3. Use `get_affected_flows` to understand impact.
4. Use `query_graph` pattern="tests_for" to check coverage.
