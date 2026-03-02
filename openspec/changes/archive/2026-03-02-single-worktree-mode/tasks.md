## 1. Add mode detection to server

- [x] 1.1 Add `detectMode(rootPath)` function that checks for openspec/changes at multiple levels
- [x] 1.2 Add `currentMode` state variable to track detected mode
- [x] 1.3 Call `detectMode()` in `startServer()` and when rootPath changes via API
- [x] 1.4 Update `/api/config` GET response to include `mode` field

## 2. Implement single-worktree scanning

- [x] 2.1 Add `getRepositoriesSingleMode()` function for single-worktree scanning
- [x] 2.2 Handle direct project case: `rootPath/openspec/changes/` → synthetic repo with basename
- [x] 2.3 Handle sibling projects case: `rootPath/*/openspec/changes/` → synthetic repo "projects"
- [x] 2.4 Update `getRepositories()` to delegate based on currentMode

## 3. Implement single-worktree features scanning

- [x] 3.1 Add `getFeaturesSingleMode()` function
- [x] 3.2 Handle direct project: return features with worktree = "main"
- [x] 3.3 Handle sibling projects: return features with worktree = project name
- [x] 3.4 Update `getFeatures()` to delegate based on currentMode

## 4. Update frontend for single mode

- [x] 4.1 Store mode from `/api/config` response in app state
- [x] 4.2 Hide repo selector dropdown when `repositories.length === 1`
- [x] 4.3 Auto-select single repository on load

## 5. Manual QA

- [x] 5.1 Manual QA: Test pointing at `/Users/sebastian/src/private/utils` shows sfl.specboard changes
- [x] 5.2 Manual QA: Test pointing at direct project with openspec/changes works
- [x] 5.3 Manual QA: Test existing workspace mode still works unchanged
- [x] 5.4 Manual QA: Test repo selector hides when only one repo exists
