## Context

The sidebar currently has two navigation items: "Live" and "Features". Users switch between root directories via a modal directory browser triggered from the header. Frequent directory switching requires multiple clicks through the modal each time.

The sidebar has available space below the current navigation items that can accommodate a "Recent" section for quick directory access.

## Goals / Non-Goals

**Goals:**
- Provide one-click access to recently visited directories
- Persist recent directories across browser sessions
- Integrate seamlessly with existing sidebar styling
- Update recent list automatically when root path changes

**Non-Goals:**
- Favorites/pinned directories (separate feature)
- Directory search functionality
- Syncing recent directories across devices/browsers
- Removing individual items from recent list

## Decisions

### 1. Storage Format

**Decision:** Store as JSON array in localStorage under `specboard_recent_directories`

```javascript
["path/one", "path/two", "path/three"]
```

**Rationale:** Simple array is sufficient. No need for timestamps or metadata since we only care about recency order. Paths are stored as strings, matching the existing `specboard_root_path` format.

**Alternatives considered:**
- Object with timestamps: Unnecessary complexity for a simple MRU list
- IndexedDB: Overkill for storing a few strings

### 2. Maximum Entries

**Decision:** Limit to 5 entries

**Rationale:** Keeps the list scannable at a glance. The sidebar has limited vertical space, and 5 entries provides enough history without scrolling. Old entries automatically fall off when limit is reached.

**Alternatives considered:**
- 10 entries: Too long, requires scrolling in smaller viewports
- Configurable limit: Over-engineering for initial implementation

### 3. Icon Choice

**Decision:** Use Lucide `clock` icon for the "Recent" section header

**Rationale:** Standard icon for recent/history across UIs. Already using Lucide icons throughout the app.

### 4. Visual Separator

**Decision:** Add CSS border-top with spacing above the "Recent" header

**Rationale:** Follows existing visual patterns in the app. A simple 1px border with appropriate margin creates clear visual hierarchy without heavy styling.

### 5. Display Format

**Decision:** Show only the directory basename (last path segment) with full path as title tooltip

**Rationale:** Basenames are typically unique and recognizable. Full paths would be too long for the narrow sidebar. Hover reveals full path when needed.

### 6. Click Behavior

**Decision:** Clicking a recent item calls the existing `updateRootPath()` function with the stored path

**Rationale:** Reuses existing path-switching logic. The updateRootPath flow already handles API calls, localStorage updates, and UI refresh. Adding to recent list happens in this same function.

## Risks / Trade-offs

**[Invalid paths in storage]** User may have directories that no longer exist
- Mitigation: The app already handles invalid paths gracefully. Failed API calls show errors. Stale entries will naturally fall off as user visits new directories.

**[Full paths in localStorage]** Absolute paths contain username/system info
- Mitigation: localStorage is already used for root path. This is consistent with existing behavior. Not a new exposure.

**[Sidebar height]** Adding 5+ items may cause sidebar overflow on small screens
- Mitigation: Sidebar already scrolls if needed. Keep limit at 5 to minimize impact.
