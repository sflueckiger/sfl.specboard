## ADDED Requirements

### Requirement: Features tab displays archived features

The Features tab SHALL display archived features below active features, separated by a visual divider with "Archived" label.

#### Scenario: Repository has both active and archived features
- **WHEN** user views the Features tab for a repository with active and archived features
- **THEN** active features are displayed first, followed by a separator line with "Archived" label, followed by archived feature cards

#### Scenario: Repository has only archived features
- **WHEN** user views the Features tab for a repository with only archived features
- **THEN** the separator line with "Archived" label is displayed, followed by archived feature cards

#### Scenario: Archived feature interaction
- **WHEN** user clicks on an archived feature card in the Features tab
- **THEN** the feature detail view opens with full access to all artifacts (proposal, design, specs, plan)

### Requirement: Live view displays active feature count header

The Live view SHALL display a header bar above all feature swimlanes showing the count of features in active development.

#### Scenario: Header displays active feature count
- **WHEN** user views the Live view with N active (non-archived) features
- **THEN** a header bar is displayed with text "N Features in active development"

#### Scenario: Header with zero active features
- **WHEN** user views the Live view with no active features (only archived or none)
- **THEN** the header bar displays "0 Features in active development"

### Requirement: Live view archive toggle

The Live view header SHALL include a "Show Archive" toggle on the right side, defaulting to off.

#### Scenario: Toggle default state
- **WHEN** user views the Live view for the first time (no stored preference)
- **THEN** the "Show Archive" toggle is off and archived features are hidden

#### Scenario: Toggle enables archive display
- **WHEN** user enables the "Show Archive" toggle
- **THEN** archived feature swimlanes are displayed below active feature swimlanes

#### Scenario: Toggle disables archive display
- **WHEN** user disables the "Show Archive" toggle while archived features are visible
- **THEN** archived feature swimlanes are hidden

### Requirement: Archive toggle state persistence

The Live view "Show Archive" toggle state SHALL be persisted to localStorage.

#### Scenario: Toggle state is saved
- **WHEN** user changes the "Show Archive" toggle state
- **THEN** the state is saved to localStorage key `specboard_showArchive`

#### Scenario: Toggle state is restored
- **WHEN** user returns to the Live view after previously setting the toggle
- **THEN** the toggle reflects the previously saved state

### Requirement: Archived swimlanes display badge

Archived feature swimlanes in the Live view SHALL display an "Archived" badge below the task/subtask statistics.

#### Scenario: Badge placement
- **WHEN** archived feature swimlanes are displayed (toggle is on)
- **THEN** each archived swimlane shows "Archived" badge in the lane-meta area, below the "N tasks | N/N subtasks" text

#### Scenario: Active features have no badge
- **WHEN** active feature swimlanes are displayed
- **THEN** no "Archived" badge is shown in the lane-meta area
