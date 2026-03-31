# Changelog

## Version 1.0.0 (initial release)

### Features

- Create notes during play mode with configurable hotkey (default F8)
- Three placement modes: Player Position, Cursor Raycast, Screen Centre Ray
- 2D and 3D project support
- Works in Unity Editor and standalone builds
- Five default note types: Critical, Bug, Todo, Visual, Idea
- Customisable note types with user-defined names and colours
- ScriptableObject-based persistence — notes survive play mode transitions
- Scene Notes Manager editor window with full note management
- Click-to-navigate — fly the Scene view camera to any note
- Filter notes by type and resolved status
- Mark notes as resolved without deleting
- Regenerate, hide, and delete all notes from the manager
- CSV export for project management tools
- JSON export from standalone builds
- JSON import into editor with duplicate detection
- Auto-filled metadata: date, time, author, position, scene name
- Billboard 3D sticky note prefab with colour-coded type headers
- 2D sprite-based note prefab for 2D projects
- Scene view gizmos with distance-based fade
- Render-on-top option for note visibility through geometry
- Tag-based player fallback when player reference is not set
- Compatible with Built-in, URP, and HDRP
- Full source code included
- Documentation and demo scene included

### Planned for future updates

- Screenshot capture attached to notes
- Trello and project management tool integration
- Scene view annotation drawing
- Priority levels and team member assignment
- Note search within the manager window
