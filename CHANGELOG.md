# Changelog

All notable changes to Specboard are documented in this file.

## [1.1.0] - 2026-03-02

### Added

#### CLI Support
- Run Specboard from anywhere with `bunx @sflueckiger/specboard` or `npx @sflueckiger/specboard`
- Global install support: `bun install -g @sflueckiger/specboard` then run `specboard`
- CLI flags: `--port <number>`, `--open` (auto-open browser), `--help`, `--version`
- Positional argument for root path: `specboard /path/to/workspace`

#### Single-Worktree Mode
- Auto-detect directory structure on startup (workspace vs single-project)
- Support standalone projects with `openspec/changes/` directly in root
- Support sibling projects: `root/{project}/openspec/changes/`
- Simplified UI when only one repository exists (auto-select, hide dropdown)

#### Recent Directories
- New "Recent" section in sidebar below Features navigation
- Quick-switch to previously visited directories with one click
- Persists up to 5 recent directories in localStorage
- Shows directory basename with full path tooltip on hover

#### Archive Display
- View archived features in the Features tab (below a separator)
- "Show Archive" toggle in Live view header
- Archived swimlanes display with "Archived" badge
- Full artifact access for archived features

### Changed

- Refactored server to export `startServer(options)` for programmatic use
- Path changes now update the view directly without manual refresh

## [1.0.0] - 2026-03-01

### Added

- Initial release
- Real-time OpenSpec progress monitoring via SSE
- Kanban-style task visualization (Todo, In Progress, Done)
- Feature detail view with artifact tabs (Proposal, Specs, Design, Plan)
- Interactive Manual QA subtask toggling
- Directory browser for path selection
- Multi-repository and multi-worktree support
- Action buttons to open in Finder, VS Code, or Terminal
