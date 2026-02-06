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

## Supabase MCP for Database Operations

Use the Supabase MCP tools for all database queries and data manipulation in development. This provides direct access to the Postgres database without needing to write application code.

### Available Tools

| Tool              | Use Case                                    |
| ----------------- | ------------------------------------------- |
| `execute_sql`     | Run SELECT, INSERT, UPDATE, DELETE queries  |
| `list_tables`     | View all tables in the database             |
| `apply_migration` | DDL operations (CREATE, ALTER, DROP tables) |
| `get_logs`        | View database logs for debugging            |

### Examples

```sql
-- Query data
SELECT * FROM users WHERE email = 'test@example.com';

-- Delete all data from tables (with CASCADE for foreign keys)
TRUNCATE TABLE users, organizations CASCADE;

-- Check row counts
SELECT
  (SELECT COUNT(*) FROM users) as users_count,
  (SELECT COUNT(*) FROM organizations) as organizations_count;

-- Insert test data
INSERT INTO organizations (id, name) VALUES ('org_123', 'Test Org');
```

### When to Use Supabase MCP

- **Querying data** for debugging or verification
- **Seeding test data** in development
- **Cleaning up data** (TRUNCATE with CASCADE)
- **Checking database state** during development
- **Running ad-hoc queries** without writing application code

### Notes

- Use `execute_sql` for DML (SELECT, INSERT, UPDATE, DELETE)
- Use `apply_migration` for DDL (schema changes)
- Always use CASCADE when truncating tables with foreign key relationships
