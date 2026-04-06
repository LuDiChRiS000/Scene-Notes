# Standalone builds

Scene Notes works in standalone builds, not just the Unity Editor. QA testers, playtesters, and team members can drop contextual notes while playing a built version of your game — no Unity installation required.

## How it works

1. You include the SceneNotesCanvas prefab in your build
2. A tester plays the build and presses the hotkey to create notes
3. Notes are stored in memory during the session
4. When the application quits, notes are saved to a JSON file automatically
5. The tester sends the JSON file to the development team
6. You import it in the Unity Editor — notes appear at the correct positions

## Setting up builds

### Including Scene Notes in your build

The SceneNotesCanvas prefab must be present in your scene. It contains both the SceneNotesController (which manages note data and persistence) and the SceneNoteCreator (which handles the hotkey and creation UI).

The controller uses `DontDestroyOnLoad` so it persists across scene changes — you only need to place it in your first loaded scene.

Make sure the SceneNotesSettings asset is assigned on the SceneNotesController component. The settings and database references are serialised on the prefab, so they are included in the build automatically.

### Build-specific behaviour

In standalone builds, Scene Notes adapts automatically:

- Notes are saved to JSON at `Application.persistentDataPath` instead of modifying ScriptableObjects (which is editor-only)
- The file name format is `SceneNotes_[SceneName]_[Timestamp].json`
- Notes auto-save when the application quits via `OnApplicationQuit`
- The note creation UI uses the same runtime Canvas overlay as in the editor

### Testing your build

1. Build your project normally
2. Run the build
3. Press the hotkey (default F8) — the game should freeze and the creation panel should appear
4. Create a test note and confirm
5. Quit the application
6. Check `Application.persistentDataPath` for the JSON file

!!! tip
    The persistent data path varies by platform:
    
    - Windows: `C:/Users/[username]/AppData/LocalLow/[CompanyName]/[ProductName]/`
    - macOS: `~/Library/Application Support/[CompanyName]/[ProductName]/`
    - Linux: `~/.config/unity3d/[CompanyName]/[ProductName]/`

## Importing notes from builds

1. Open the Scene Notes Manager window in the Unity Editor
2. Click Import from Build in the toolbar
3. A file picker opens — navigate to the JSON file and select it
4. Notes are merged into the database with duplicate detection (importing the same file twice is safe — existing IDs are skipped)
5. The manager regenerates note objects automatically

If the JSON file contains notes from multiple scenes, they are all added to the database. Switch to each scene and regenerate to see its notes.

The import path defaults to `Application.persistentDataPath`. You can set a custom path in the Build Import Path field in settings if your testers save files to a shared network folder.

## JSON file format

The export uses Unity's `JsonUtility` with a wrapper object:

```json
{
  "notes": [
    {
      "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
      "description": "Player falls through floor here",
      "noteTypeName": "Critical",
      "worldPosition": { "x": -12.4, "y": 0.0, "z": 33.7 },
      "sceneName": "Level_01",
      "authorName": "QA_Tester_1",
      "dateTime": "2026-03-29T14:14:00.0000000Z",
      "isResolved": false
    }
  ]
}
```

## QA team workflow

### Setup (one time)

1. Run the setup wizard (Tools → Scene Notes → 1. Create Assets, then 2. Create Prefabs)
2. Place the SceneNotesCanvas prefab in your first scene
3. Configure the hotkey and spawn mode
4. Build and distribute to your QA team
5. Tell testers the hotkey and ask them to set author names if the settings allow it

### Each testing session

1. Tester plays the build normally
2. Presses the hotkey when they find an issue
3. Types a description, selects a type, confirms
4. Continues playing — repeats for each issue
5. Quits the application — JSON file saves automatically

### Processing feedback

1. Developer opens Unity and the Scene Notes Manager
2. Clicks Import from Build, selects the JSON file
3. Notes appear in the correct scenes at the correct positions
4. Clicks through notes to review each issue at its exact location
5. Fixes issues and marks notes as resolved
6. Exports CSV for the project tracker if needed
