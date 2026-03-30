# Configuration

All Scene Notes settings are stored in a single ScriptableObject asset. Select it in the Project window to edit the configuration in the Inspector.

Default location: `Assets/SceneNotes/Settings/DefaultSceneNotesSettings.asset`

## General settings

### Hotkey

The key that triggers note creation during play mode. Default is F8. You can set this to any KeyCode value.

Choose a key that does not conflict with your game's controls. If your game uses F8 for something, change this before playtesting.

### Author name

The name attached to each note you create. Defaults to your system username. Override this in the settings if you prefer a different name, or if multiple team members share a machine.

For team workflows, each team member should set their own author name so notes can be attributed correctly.

### Database

A reference to the SceneNotesDatabase ScriptableObject that stores all note data. The default database is created automatically. You can create additional databases if you need to maintain separate note sets.

### Auto-regenerate on play mode exit

When enabled (default), Scene Notes automatically rebuilds all note objects in the scene when you exit play mode. Disable this if you prefer to regenerate manually via the Scene Notes Manager window.

## Placement settings

### Spawn mode

Controls where notes appear when created. See [Placement modes](spawn-modes.md) for detailed guidance.

| Mode | Best for |
|------|----------|
| Player Position | FPS, third-person, platformers, RPGs |
| Cursor Raycast | RTS, city builders, god games, top-down strategy |
| Screen Centre Ray | VR, cursor-locked FPS, reticle-based games |

### Player reference

The Transform of your player character. Only used in Player Position mode. If left empty, Scene Notes looks for a GameObject tagged "Player" as a fallback.

### Forward offset

A Vector3 offset applied in Player Position mode. Controls where the note spawns relative to the player. Default is (0, 0, 2) which places the note 2 units in front of the player.

- X: left/right offset
- Y: up/down offset
- Z: forward/backward offset

Adjust this based on your camera setup. For a first-person game, (0, 0, 3) places notes a comfortable distance ahead. For a third-person game with an overhead camera, (0, 2, 0) places notes above the player.

### 2D mode

Enable this for 2D projects. Changes the note prefab to a sprite-based version and uses 2D raycasting instead of 3D.

### Note Z depth (2D only)

The Z position for notes in 2D mode. Negative values place notes in front of your game art. Adjust this so notes are visible but do not obscure important gameplay elements. Default is -1.

### Max raycast distance

The maximum distance for cursor and screen centre raycasts. If the ray does not hit any collider within this distance, the fallback distance is used instead. Default is 100 units.

### Fallback ray distance

When a raycast does not hit anything (for example, the cursor is pointing at the sky), the note spawns at this distance from the camera along the ray direction. Default is 20 units.

### Raycast layer mask

Controls which layers the raycast can hit. Default is Everything. If your game has layers that should not receive notes (UI layers, trigger volumes, etc.), exclude them here.

## Visual settings

### Note prefab (3D)

The prefab used for 3D note objects. The default prefab is a billboard sticky note with a colour header and text display. You can replace this with your own prefab — it must have a SceneNoteObject component attached.

### Note prefab (2D)

The prefab used for 2D note objects. Same requirements as the 3D prefab but using SpriteRenderer instead of MeshRenderer.

### Note scale

Global scale multiplier for note objects. Increase this if notes are too small to read in your scene. Default is 1.0.

### Billboard notes

When enabled (default), note objects always face the camera. Disable this if you want notes to remain at a fixed rotation.

### Render on top

When enabled (default), notes render on top of all scene geometry so they are never hidden behind walls or objects. Uses a high sorting order or ZTest Always depending on render pipeline. Disable this if you prefer notes to be occluded by geometry.

### Gizmo max distance

The maximum distance at which note gizmos are visible in the Scene view. Notes beyond this distance fade out. Default is 100 units. Increase for large open-world scenes, decrease to reduce visual clutter.

## Export settings

### CSV export path

The file path for CSV exports, relative to the project root. Default is `SceneNotes_Export.csv`. See [Exporting notes](exporting.md).

### Build import path

The path to look for JSON files from standalone builds. Default is auto-detected from `Application.persistentDataPath`. See [Standalone builds](build-workflow.md).
