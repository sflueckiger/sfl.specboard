## 1. Add recent directories state and persistence

- [x] 1.1 Add `recentDirectories` array variable to app state in `public/app.js`
- [x] 1.2 Add `loadRecentDirectories()` function to read from localStorage key `specboard_recent_directories`
- [x] 1.3 Add `saveRecentDirectories()` function to write to localStorage
- [x] 1.4 Add `addToRecentDirectories(path)` function with deduplication and 5-entry limit
- [x] 1.5 Call `loadRecentDirectories()` in `init()` function

## 2. Integrate with path change flow

- [x] 2.1 Call `addToRecentDirectories()` in `updateRootPath()` when path successfully changes
- [x] 2.2 Verify deduplication moves existing entries to top of list

## 3. Add sidebar UI elements

- [x] 3.1 Add Recent section container to sidebar in `public/index.html`
- [x] 3.2 Add `renderRecentDirectories()` function in `public/app.js`
- [x] 3.3 Render clock icon header with "Recent" label
- [x] 3.4 Render directory entries showing basename with full path as title tooltip
- [x] 3.5 Add click handlers to call `updateRootPath()` with stored path
- [x] 3.6 Call `renderRecentDirectories()` in `init()` and after path changes

## 4. Add CSS styles

- [x] 4.1 Add separator style (border-top) above Recent section in `public/styles.css`
- [x] 4.2 Add Recent section header styles (icon + label alignment)
- [x] 4.3 Add Recent entry styles (clickable, hover state, truncation)

## 5. Manual QA

- [x] 5.1 Manual QA: Verify Recent section appears below Features with separator
- [x] 5.2 Manual QA: Verify changing directory adds entry to Recent list
- [x] 5.3 Manual QA: Verify clicking Recent entry switches root path
- [x] 5.4 Manual QA: Verify recent list persists after page reload
- [x] 5.5 Manual QA: Verify 6th entry pushes oldest entry out of list
