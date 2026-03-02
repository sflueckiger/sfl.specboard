## Why

Users frequently switch between different root directories when using Specboard. Currently, changing the root path requires navigating through the directory browser each time. A "Recent" section in the sidebar would provide quick access to previously visited directories, improving workflow efficiency.

## What Changes

- Add "Recent" section to the left sidebar below "Features"
- Add horizontal separator above the Recent section
- Display recently visited directories with Clock icon (Lucide)
- Store recent directories in localStorage (max 5-10 entries)
- Allow clicking a recent entry to switch root path
- Auto-update recent list when root path changes

## Capabilities

### New Capabilities
- `recent-directories`: Sidebar section displaying recently visited root directories with localStorage persistence and quick-switch functionality

### Modified Capabilities
<!-- No existing capabilities are being modified at the spec level -->

## Impact

- **Frontend**: `public/app.js` - Add recent directories state, localStorage read/write, sidebar rendering
- **Frontend**: `public/styles.css` - Add styles for separator and recent items
- **Frontend**: `public/index.html` - Add container for recent section in sidebar
- **LocalStorage**: New key `specboard_recent_directories` for persistence
