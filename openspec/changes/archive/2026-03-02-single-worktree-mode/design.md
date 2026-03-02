## Context

Specboard scans `rootPath/{repo}/{worktree}/openspec/changes/` expecting Conductor's workspace structure. For single projects or flat layouts, this doesn't work. Need to auto-detect the structure and handle both cases.

## Goals / Non-Goals

**Goals:**
- Auto-detect workspace vs single-worktree mode based on directory structure
- Support pointing at `/Users/sebastian/src/private/utils` and seeing `sfl.specboard` changes
- Minimal UI changes - just hide unnecessary selectors in single mode

**Non-Goals:**
- Changing the existing workspace mode behavior
- Supporting deeply nested arbitrary structures
- Manual mode selection (auto-detect only)

## Decisions

### 1. Detection algorithm

**Choice**: Check for `openspec/` directory at multiple levels on startup.

Detection order:
1. `rootPath/openspec/changes/` → single-worktree mode (direct project)
2. `rootPath/*/openspec/changes/` → single-worktree mode (sibling projects)
3. `rootPath/*/*/openspec/changes/` → workspace mode (repo/worktree)

```typescript
async function detectMode(rootPath: string): Promise<"workspace" | "single"> {
  // Check if rootPath itself has openspec/changes
  if (await dirExists(join(rootPath, "openspec", "changes"))) {
    return "single";
  }

  // Check immediate children for openspec/changes
  const entries = await readdir(rootPath, { withFileTypes: true });
  for (const entry of entries) {
    if (entry.isDirectory() && !entry.name.startsWith(".")) {
      const childPath = join(rootPath, entry.name, "openspec", "changes");
      if (await dirExists(childPath)) {
        return "single";  // Found at first level = single mode
      }
    }
  }

  // Default to workspace mode (repo/worktree structure)
  return "workspace";
}
```

**Rationale**: Simple heuristic that covers common cases without configuration.

### 2. Data model in single-worktree mode

**Choice**: Use synthetic "repo" and "worktree" names for consistency.

In single mode, create a virtual structure:
- If `rootPath/openspec/changes/` exists: repo = basename(rootPath), worktree = "main"
- If `rootPath/project/openspec/changes/` exists: repo = "projects", worktree = project name

**Rationale**: Keeps the API response shape consistent. Frontend can hide selectors but data model stays the same.

### 3. Frontend changes

**Choice**: Hide repo selector dropdown when only one repo exists.

In `public/app.js`:
- Check if `repositories.length === 1`
- If so, auto-select it and hide the dropdown
- Show just the project/worktree name in the header

**Rationale**: Minimal change - just conditional visibility, no structural changes.

### 4. API response changes

**Choice**: Add `mode` field to `/api/config` response.

```json
{
  "rootPath": "/path/to/dir",
  "mode": "single" | "workspace"
}
```

**Rationale**: Frontend can use this to adjust UI behavior.

## Risks / Trade-offs

**[Detection heuristic may misfire]** → If someone has a workspace with only one repo that has `openspec/` at first level. Mitigation: Detection order prioritizes single mode only if pattern matches exactly.

**[Performance on large directories]** → Scanning for `openspec/changes` adds startup overhead. Mitigation: Stop scanning on first match; use early returns.
