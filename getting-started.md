# Getting started

This guide walks you through importing Scene Notes into your project and creating your first note.

## Installation

1. Import the Scene Notes package from the Unity Asset Store
2. The package installs to `Assets/SceneNotes/`
3. No additional setup is required — the default settings work out of the box

## First-time setup

After importing, you will find a settings asset at `Assets/SceneNotes/Settings/DefaultSceneNotesSettings.asset`. Select it in the Project window to view the configuration in the Inspector.

<!-- ![Settings asset in Inspector](images/settings-inspector.png) -->

The default settings are:

| Setting | Default |
|---------|---------|
| Hotkey | F8 |
| Spawn mode | Player Position |
| Author name | Your system username |
| 2D mode | Off |
| Auto-regenerate on play mode exit | On |

For most projects, the only thing you may need to change is the spawn mode. See [Placement modes](spawn-modes.md) for details on which mode suits your game type.

## Setting up the player reference

If you are using Player Position spawn mode (the default), you need to tell Scene Notes which GameObject is your player:

1. Select the Scene Notes Settings asset
2. In the Placement section, find the Player Reference field
3. Drag your player GameObject from the scene hierarchy into this field
4. Optionally adjust the Forward Offset to control where notes spawn relative to the player

If the player reference is not set, Scene Notes will attempt to find a GameObject tagged "Player" as a fallback.

!!! tip
    For games where the player object changes between scenes, use the tag-based fallback. Tag your player GameObject as "Player" in each scene and leave the Player Reference field empty.

## Creating your first note

1. Enter play mode in the Unity Editor
2. Play your game normally
3. When you spot something worth noting, press the hotkey (default F8)
4. The game freezes and the note creation panel appears
5. Type a description of the issue or task
6. Select a note type from the dropdown (Critical, Bug, Todo, Visual, or Idea)
7. Click Confirm

The note spawns as a colour-coded sticky note at your position. The game resumes automatically.

<!-- ![Note creation panel](images/note-creation-panel.png) -->

## Viewing notes after playtesting

When you exit play mode, Scene Notes automatically regenerates all your notes as scene objects. You can see them floating in the scene at the positions where you created them.

To manage your notes, open the Scene Notes Manager window:

- Go to Window > Scene Notes > Scene Notes Manager
- Or use the keyboard shortcut (configurable in settings)

The manager window lists all notes in the current scene. Click any note to fly the Scene view camera to its location. See [Scene Notes Manager](editor-window.md) for full details.

## Adding Scene Notes to a build

Scene Notes also works in standalone builds, allowing QA testers to drop notes without opening Unity. See [Standalone builds](build-workflow.md) for setup instructions.

## Next steps

- [Configuration](configuration.md) — customise hotkeys, spawn modes, and visuals
- [Placement modes](spawn-modes.md) — choose the right mode for your game type
- [Note types](note-types.md) — create custom note categories
- [Exporting notes](exporting.md) — export to CSV or import from builds
