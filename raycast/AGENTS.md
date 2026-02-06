# Raycast Extensions

This repo uses sparse checkout to only check out specific extensions instead of the entire monorepo.

## Sparse Checkout

List currently checked out extensions:

```bash
git sparse-checkout list
```

Find an extension by name (case-insensitive search):

```bash
git ls-tree --name-only origin/main extensions/ | grep -i <search-term>
```

Add an extension:

**IMPORTANT:** Always run sparse-checkout commands from the repo root (`/Users/kevin/Code/raycast/extensions`), not from inside the `extensions/` subdirectory. Running from the wrong directory causes doubled paths like `extensions/extensions/<name>`.

```bash
git sparse-checkout add extensions/<extension-name>
```

If the extension doesn't appear after adding it, make sure upstream is up to date first:

```bash
git fetch upstream main && git merge upstream/main
```

## Initial Setup

```bash
git clone --filter=blob:none --sparse git@github.com:raycast/extensions.git
cd extensions
git sparse-checkout init --cone
git sparse-checkout set extensions/todoist extensions/fuzzy-clock
```
