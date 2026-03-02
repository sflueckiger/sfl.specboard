## Context

The server already loads archived features (from `openspec/changes/archive/` directories) and includes them in API responses with `isArchived: true`. Currently, both `renderFeatures()` (Live view) and `renderFeaturesList()` (Features tab) filter these out with `.filter(f => !f.isArchived)`.

The existing swimlane structure uses `.lane-meta` to display task/subtask stats on the right side of the lane header. The Features tab renders a simple card list without swimlanes.

## Goals / Non-Goals

**Goals:**
- Display archived features in Features tab below a separator, with full functionality
- Add a summary header to Live view showing active feature count with archive toggle
- Render archived swimlanes with visual distinction when toggle is enabled
- Persist toggle state to localStorage

**Non-Goals:**
- Filtering or searching archived features
- Different behavior for archived features (editing, actions)
- Archiving/unarchiving features from the UI

## Decisions

### 1. Features Tab: Separator approach

**Decision**: Insert a styled `<hr>` separator with "Archived" label between active and archived feature cards.

**Rationale**: Simple, clear visual hierarchy. Archived features remain fully interactive with all actions available.

**Implementation**: In `renderFeaturesList()`, after rendering active features, append separator div and archived feature cards if any exist.

### 2. Live View: Header bar placement

**Decision**: Add a header bar inside `#swimlanes` container, above all feature lanes. Contains left-aligned count text and right-aligned toggle.

**Rationale**: Placing inside swimlanes keeps it contextual to the content. The toggle only affects this view, so it belongs with the swimlanes rather than in the nav.

**Implementation**: In `renderFeatures()`, prepend header HTML before feature lanes.

### 3. Toggle control implementation

**Decision**: Use a CSS-styled checkbox with `<label>` for the toggle, styled as a pill/switch.

**Rationale**: Native checkbox provides accessibility (keyboard navigation, screen readers) without JavaScript toggle state management complexity. CSS handles visual styling.

### 4. Archive badge location

**Decision**: Add "Archived" badge in `.lane-meta` below the stats text ("n tasks | n/n subtasks").

**Rationale**: Per the proposal, badge appears below stats. Using `.lane-meta` keeps metadata grouped. Existing structure already supports multi-line content via flexbox.

**Implementation**: Modify `renderFeatureLane()` to accept optional `showArchiveBadge` parameter, render badge when true.

### 5. State persistence

**Decision**: New localStorage key `specboard_showArchive` (boolean as string).

**Rationale**: Follows existing pattern (`specboard_rootPath`, `specboard_repo`). Default false matches current behavior.

## Risks / Trade-offs

**[Large archive]** Many archived features could slow rendering or make the UI cluttered.
→ Acceptable for now since archived features are opt-in via toggle. Future: pagination if needed.

**[Toggle visibility]** Toggle is only visible when features exist.
→ Acceptable since toggle is meaningless with no features.

**[View synchronization]** Toggle state is Live view only; Features tab always shows archive.
→ Intentional per proposal: different UX for each view.
