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
```bash
git sparse-checkout add extensions/<extension-name>
```

## Initial Setup

```bash
git clone --filter=blob:none --sparse git@github.com:raycast/extensions.git
cd extensions
git sparse-checkout init --cone
git sparse-checkout set extensions/todoist extensions/fuzzy-clock
```
