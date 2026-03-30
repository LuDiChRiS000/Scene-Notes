# Scene Notes Manager

The Scene Notes Manager is an editor window that gives you full control over all notes in your scene. Open it from the Unity menu: Window > Scene Notes > Scene Notes Manager.

<!-- ![Scene Notes Manager window](images/manager-window.png) -->

## Quick action buttons

The top of the window contains action buttons for managing notes in bulk:

### Regenerate all

Destroys all existing note objects in the scene and rebuilds them from the database. Use this if note objects have been accidentally deleted or moved, or after importing notes from a build.

This does not create or delete any data — it only rebuilds the visual objects from the stored note data.

### Hide all

Removes all note objects from the scene without affecting the database. The notes still exist in the ScriptableObject and can be brought back at any time with Regenerate All.

Useful when notes are cluttering the Scene view during level design work and you want a clean view temporarily.

### Delete all

Permanently removes all notes for the current scene from the database and destroys their scene objects. This action cannot be undone — a confirmation dialog appears before proceeding.

### Export CSV

Exports all notes in the current scene to a CSV file. See [Exporting notes](exporting.md) for details on the export format and configuration.

### Import from build

Opens a file picker to select a JSON file from a standalone build. See [Standalone builds](build-workflow.md) for the full QA workflow.

## Filter bar

Below the action buttons, a row of filter pills lets you show or hide notes by type. Each pill displays the type name, colour, and the number of notes of that type in the current scene.

Click a pill to toggle that type's visibility. Active types are shown with full opacity, hidden types are dimmed.

A separate Resolved filter lets you choose between showing all notes, only unresolved notes, or only resolved notes.

Filters affect both the note list in the manager window and the visibility of note objects in the scene.

## Note list

The main area of the window is a scrollable list of all notes in the current scene (after filtering). Each row shows:

- A colour dot indicating the note type
- The description text (truncated if long)
- The author name
- The creation date and time
- The world position coordinates

### Click to navigate

Click any note in the list to fly the Scene view camera to that note's world position. The selected note is highlighted in the list and its scene object is also highlighted with a selection outline.

This is the fastest way to find a specific issue — scan the list, click the note, and you are looking at exactly where the problem is.

### Right-click context menu

Right-click any note to access:

- Resolve / Unresolve — toggle the resolved status
- Delete — remove this single note (with confirmation)
- Copy position — copy the world position coordinates to clipboard
- Select in scene — select the note's GameObject in the hierarchy

### Resolved notes

Resolved notes appear with a strikethrough on the description and reduced opacity. They remain in the list and database until explicitly deleted, giving you a record of issues that have been addressed.

## Sorting

Click the column headers in the note list to sort by different fields:

- Sort by type — groups notes by category
- Sort by date — newest or oldest first
- Sort by author — groups notes by team member
- Sort by resolved — unresolved notes first

## Keyboard shortcuts

The manager window supports these keyboard shortcuts when focused:

- Delete key — delete the selected note (with confirmation)
- R — toggle resolved status on the selected note
- F — fly to the selected note in the Scene view

## Scene view integration

When the Scene Notes Manager is open, note gizmos appear in the Scene view as small coloured icons at each note position. These are visible even when zoomed out or when note GameObjects are hidden.

Hovering over a gizmo in the Scene view shows a tooltip with the note description. Gizmos fade with distance based on the Gizmo Max Distance setting.
