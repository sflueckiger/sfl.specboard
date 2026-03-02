## Why

Specboard currently assumes a Conductor-style workspace structure (`root/repo/worktree/openspec/changes/`). Users with standalone projects or non-Conductor setups cannot easily monitor their OpenSpec changes without restructuring their directories.

## What Changes

- Add automatic path structure detection on startup
- Support two modes:
  - **Workspace mode** (existing): `rootPath/{repo}/{worktree}/openspec/changes/`
  - **Single-worktree mode** (new): `rootPath/openspec/changes/` or `rootPath/{project}/openspec/changes/`
- Auto-detect mode by checking if `openspec/changes/` exists at or near the root path
- Simplify UI in single-worktree mode (hide repo/worktree selectors when there's only one)
- Support scanning parent directory for sibling projects with `openspec/` folders

## Capabilities

### New Capabilities

- `path-detection`: Auto-detect whether the root path is a workspace (multi-repo/worktree) or a single project, and scan accordingly

### Modified Capabilities

None - existing workspace mode behavior unchanged.

## Impact

- **server.ts**: Add detection logic in `getRepositories()` and `getFeatures()` to handle both structures
- **public/app.js**: Conditionally hide repo selector when in single-worktree mode
- **API**: No changes to endpoints, just different data shapes returned
- **CLI**: No changes needed - already accepts arbitrary path
