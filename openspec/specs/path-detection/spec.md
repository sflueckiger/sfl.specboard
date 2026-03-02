## ADDED Requirements

### Requirement: Auto-detect path structure mode

The system SHALL automatically detect whether the root path is a workspace (multi-repo/worktree) or single-worktree structure on startup.

#### Scenario: Direct project path

- **WHEN** root path contains `openspec/changes/` directory directly
- **THEN** system operates in single-worktree mode
- **THEN** system treats the root path as a single project

#### Scenario: Sibling projects path

- **WHEN** root path contains child directories with `openspec/changes/`
- **THEN** system operates in single-worktree mode
- **THEN** system scans all child directories for `openspec/changes/`

#### Scenario: Workspace path

- **WHEN** root path contains `{repo}/{worktree}/openspec/changes/` structure
- **THEN** system operates in workspace mode
- **THEN** system scans using existing repo/worktree hierarchy

### Requirement: Report mode in config API

The system SHALL include the detected mode in the `/api/config` response.

#### Scenario: Config includes mode

- **WHEN** client requests GET `/api/config`
- **THEN** response includes `mode` field with value "single" or "workspace"

### Requirement: Single-worktree mode scanning

The system SHALL scan for changes in single-worktree mode without requiring repo/worktree structure.

#### Scenario: Scan direct project

- **WHEN** mode is "single" and `rootPath/openspec/changes/` exists
- **THEN** system returns changes from that directory
- **THEN** changes are grouped under a synthetic repository name

#### Scenario: Scan sibling projects

- **WHEN** mode is "single" and `rootPath/{project}/openspec/changes/` exists
- **THEN** system returns changes from all matching projects
- **THEN** each project appears as a separate "worktree" under a synthetic repository

### Requirement: UI adapts to mode

The system SHALL simplify the UI when operating in single-worktree mode with only one repository.

#### Scenario: Hide repo selector for single repo

- **WHEN** only one repository exists
- **THEN** repo selector dropdown is hidden
- **THEN** repository is auto-selected
