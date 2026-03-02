## 1. State Management

- [x] 1.1 Add `showArchive` to STORAGE_KEYS object in app.js
- [x] 1.2 Add `showArchive` global variable initialized from localStorage (default false)

## 2. Features Tab - Archived Display

- [x] 2.1 Modify `renderFeaturesList()` to separate active and archived features
- [x] 2.2 Add archive separator HTML with "Archived" label after active features
- [x] 2.3 Render archived feature cards after the separator
- [x] 2.4 Fix click handler indexing to work with combined active/archived array
- [x] 2.5 Add CSS styles for `.archive-separator` element

## 3. Live View - Header Bar

- [x] 3.1 Create `renderSwimlanesHeader()` function returning header HTML with feature count
- [x] 3.2 Add toggle checkbox with label for "Show Archive" in header
- [x] 3.3 Prepend header to swimlanes container in `renderFeatures()`
- [x] 3.4 Add CSS styles for `.swimlanes-header`, count text, and toggle control

## 4. Live View - Toggle Behavior

- [x] 4.1 Add change event listener to toggle checkbox
- [x] 4.2 Save toggle state to localStorage on change
- [x] 4.3 Re-render swimlanes when toggle changes
- [x] 4.4 Initialize toggle checked state from `showArchive` variable

## 5. Live View - Archived Swimlanes

- [x] 5.1 Modify `renderFeatureLane()` to accept `isArchived` parameter
- [x] 5.2 Add "Archived" badge below stats in `.lane-meta` when `isArchived` is true
- [x] 5.3 Conditionally render archived swimlanes in `renderFeatures()` based on toggle
- [x] 5.4 Add CSS styles for `.archived-badge` element

## 6. Manual QA

- [ ] 6.1 Manual QA: Verify Features tab shows active features, separator, then archived features
- [ ] 6.2 Manual QA: Verify clicking archived feature in Features tab opens detail view with all tabs
- [ ] 6.3 Manual QA: Verify Live view header shows correct count and toggle
- [ ] 6.4 Manual QA: Verify toggle shows/hides archived swimlanes
- [ ] 6.5 Manual QA: Verify toggle state persists across page refresh
- [ ] 6.6 Manual QA: Verify archived swimlanes show "Archived" badge below stats
