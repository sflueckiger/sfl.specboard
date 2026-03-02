## Why

Archived features are currently hidden from the UI entirely. Users cannot review completed work, reference past implementations, or get an overview of project history. This limits visibility into what has been accomplished and makes it harder to learn from past changes.

## What Changes

- **Features tab**: Display archived features below a visual separator line, providing full access to view their artifacts and details
- **Live view**: Add a summary header showing "n Features in active development" with a "Show Archive" toggle on the right
- **Live view archive display**: When toggle is enabled, render archived feature swimlanes with an "Archived" badge displayed below the task/subtask stats

## Capabilities

### New Capabilities

- `archive-display`: Controls for viewing and toggling archived feature visibility across both Features and Live views

### Modified Capabilities

None - this change adds new display options without modifying existing behavior.

## Impact

- **public/app.js**: Modify `renderFeaturesView()` to include archived features with separator; modify `renderSwimlanes()` to add header with toggle and optional archived swimlanes with badge
- **public/styles.css**: Add styles for archive separator, header bar, toggle control, and "Archived" badge
- **State management**: Add `showArchive` state variable (persisted to localStorage) for the Live view toggle
