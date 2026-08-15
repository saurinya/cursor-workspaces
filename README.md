# cursor-workspaces

Multi-root Cursor workspace files for [saurinya](https://github.com/saurinya) repos.

Open a `.code-workspace` file from this repo to work in several projects at once — including a shared guidelines/skills repo — without copying those artifacts into every project.

## Clone layout

Keep this repo **next to** the projects it references. Folder names must match GitHub repo names:

```text
software/
  cursor-workspaces/    this repo
  <repo-a>/
  <repo-b>/
  <shared-guidelines>/
```

Then open `cursor-workspaces/<name>.code-workspace`, not a single folder.

## Paths

Use relative folder paths only:

```json
{
  "folders": [
    { "path": "../shared-guidelines", "name": "guidelines" },
    { "path": "../repo-a" },
    { "path": "../repo-b" }
  ]
}
```

Edit paths by hand if the UI rewrites them to absolute locations (`C:\...` or `/Users/...`). Absolute paths will not work on other machines.

## What belongs where

| Thing | Location |
| --- | --- |
| Which repos to open together | `*.code-workspace` in this repo |
| Shared skills | sibling repo, `.cursor/skills/` |
| Shared always-on agent guidance | sibling repo, `.cursor/rules/` with `alwaysApply: true` and no globs |
| Per-project rules (stack, file globs) | that project's `.cursor/rules/` |

Do not copy the same `alwaysApply` rule into every project. Cursor loads each workspace root separately and will inject duplicates.
