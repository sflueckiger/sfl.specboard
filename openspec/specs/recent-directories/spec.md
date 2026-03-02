## ADDED Requirements

### Requirement: Display recent directories in sidebar

The system SHALL display a "Recent" section in the left sidebar below the main navigation items.

#### Scenario: Recent section visible

- **WHEN** user loads the application
- **THEN** sidebar displays "Recent" section with clock icon below "Features" link
- **THEN** a horizontal separator appears above the "Recent" section header

#### Scenario: Recent section shows directory entries

- **WHEN** user has previously visited directories
- **THEN** recent section displays up to 5 directory entries
- **THEN** entries are ordered by most recently visited first

#### Scenario: Recent section empty state

- **WHEN** user has no previously visited directories
- **THEN** recent section displays no entries (empty list)

### Requirement: Persist recent directories in localStorage

The system SHALL persist the list of recently visited directories in browser localStorage.

#### Scenario: Save on path change

- **WHEN** user changes the root path via directory browser
- **THEN** system adds the new path to the recent directories list
- **THEN** system saves the updated list to localStorage key `specboard_recent_directories`

#### Scenario: Load on application start

- **WHEN** application initializes
- **THEN** system loads recent directories from localStorage
- **THEN** system renders the loaded directories in the Recent section

#### Scenario: Limit to 5 entries

- **WHEN** user visits a 6th unique directory
- **THEN** system removes the oldest entry from the list
- **THEN** list contains exactly 5 most recent directories

#### Scenario: Deduplicate on revisit

- **WHEN** user visits a directory that is already in the recent list
- **THEN** system moves that directory to the top of the list
- **THEN** no duplicate entries exist in the list

### Requirement: Quick-switch via recent entry click

The system SHALL allow users to switch root paths by clicking a recent directory entry.

#### Scenario: Click to switch path

- **WHEN** user clicks a recent directory entry
- **THEN** system changes the root path to the clicked directory
- **THEN** system refreshes repositories and features for the new path

#### Scenario: Display format

- **WHEN** rendering a recent directory entry
- **THEN** entry displays the directory basename (last path segment)
- **THEN** entry shows the full path as a tooltip on hover
