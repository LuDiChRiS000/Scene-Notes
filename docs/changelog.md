# Changelog

## Version 1.0.0 (initial release)

### Setup

- Three-step setup wizard: Tools → Scene Notes → 1. Create Assets / 2. Create Prefabs / 3. Create Demo Scene
- Automatic creation of ScriptableObject assets, 3D and 2D note prefabs, materials, and the runtime Canvas prefab
- Demo scene with free-fly camera, pre-seeded notes of all types, and sample environment
- Settings Inspector with built-in validation panel and quick-action buttons

### Note creation

- Configurable hotkey (default F8) triggers note creation during play mode
- Game freezes via Time.timeScale = 0 while the creation panel is open
- Text input field with placeholder text
- Note type selection via colour-coded buttons matching configured types
- Auto-filled metadata: author name, date/time, world position, scene name
- Cursor state preservation — lock mode and visibility restored after creation
- Cancel via Escape key or Cancel button
- OnCreationCanvasToggled static event for external script integration

### Placement modes

- Player Position — offset from a player Transform with configurable Vector3 offset
- Cursor Raycast — Physics.Raycast from mouse position through camera
- Screen Centre Ray — Physics.Raycast from viewport centre
- 2D mode with ScreenToWorldPoint and configurable Z depth
- Tag-based player fallback ("Player" tag) when no direct reference is assigned
- Camera.main forward fallback when no player is found
- Configurable raycast layer mask, max distance, and fallback distance

### Note types

- Five default types: Critical (red), Bug (orange), Todo (yellow), Visual (green), Idea (blue)
- Fully customisable — add, remove, rename, and recolour types via the Settings asset
- Colour applied to 3D note header strip via MaterialPropertyBlock

### 3D and 2D note prefabs

- 3D prefab: billboard quad with colour header strip, description text, metadata text, and title
- 2D prefab: smaller layout optimised for orthographic cameras
- Custom NoteUnlit shader with per-material ZTest control for render-on-top
- Billboard behaviour in both play mode (faces Camera.main) and edit mode (faces Scene view camera)
- Render-on-top toggle — detected and applied at runtime without regeneration
- TextMeshPro for all text rendering
- Notes organised under a "Scene Notes" parent GameObject

### Scene Notes Manager editor window

- Open via Tools menu or Ctrl+Shift+N keyboard shortcut
- Toolbar: Regenerate All, Hide All, Delete All, Export CSV, Import from Build, Settings
- Type filter pills with note counts per type
- Resolved filter toggle
- Scrollable note list with colour strip, description, author, date, and position
- Click to fly Scene view camera to note position
- Ctrl+click for multi-select, Shift+click for range select
- Bulk Resolve/Unresolve Selected and Delete Selected buttons (appear when notes are selected)
- Right-click context menu: resolve/unresolve, fly to, copy position (as Vector3 code), delete
- Multi-select context menu for bulk operations
- Resolved notes display with strikethrough and dimmed opacity
- Select Note in Scene option — clicking a note also selects its GameObject in the Hierarchy
- Bottom bar showing total count, resolved count, and current hotkey
- Undo support for delete and resolve operations

### Persistence

- ScriptableObject-based database — notes survive play mode transitions
- Auto-regenerate on play mode exit — destroys runtime objects and rebuilds as edit-mode prefab instances
- DontDestroyOnLoad on the controller for cross-scene persistence in play mode

### Export and import

- CSV export with RFC-4180 compliant quoting and escaping
- CSV respects current type filters and date format setting
- JSON export to Application.persistentDataPath (timestamped files)
- Automatic JSON save on application quit in standalone builds
- JSON import with duplicate detection via note ID matching
- Auto-regeneration after import

### Settings

- Date format option: DayMonthYear or MonthDayYear
- Dates displayed in local timezone (converted from UTC storage)
- Settings Inspector validation: checks for missing database, empty types, missing prefabs, missing player reference, invalid values
- Community links in Inspector: Discord, Documentation, Leave a Rating

### Planned for future updates

- Screenshot capture attached to notes
- Trello and project management tool integration
- Scene view annotation drawing
- Priority levels and team member assignment
- Note search within the Manager window
