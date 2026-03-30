# Standalone builds

Scene Notes works in standalone builds, not just in the Unity Editor. This means QA testers, playtesters, and team members can drop contextual notes while playing a built version of your game — no Unity installation required.

## How it works

1. You include the Scene Notes system in your build
2. A tester plays the build and presses the hotkey to create notes
3. Notes are saved to a JSON file on the tester's machine
4. The tester sends you the JSON file (or it syncs via a shared folder)
5. You import the file in the Unity Editor
6. Notes appear in the correct scene at the correct positions

This creates a complete QA feedback loop where bug reports include the exact world position of the issue, eliminating the guesswork of "it's somewhere near the bridge" or blurry screenshots.

## Setting up builds

### Including Scene Notes in your build

The Scene Notes system needs to be present in every scene where you want testers to create notes. The simplest approach:

1. Add the SceneNotesController prefab to your first scene
2. The controller uses DontDestroyOnLoad to persist across scene changes
3. Make sure the Settings and Database assets are referenced by the controller

Alternatively, add the SceneNotesController to each scene individually if you only want note-taking enabled in specific scenes.

### Build-specific behaviour

In standalone builds, Scene Notes automatically adapts its behaviour:

- Notes are saved to JSON at `Application.persistentDataPath` instead of modifying ScriptableObjects (which is editor-only)
- The file name format is `SceneNotes_[SceneName]_[Timestamp].json`
- Notes auto-save when the application quits or when the scene changes
- The note creation UI uses a runtime Canvas overlay

### Testing your build setup

1. Build your project normally
2. Run the build
3. Press the hotkey — the game should freeze and the note creation panel should appear
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
2. Click the Import from Build button
3. Select the JSON file from the file picker
4. Notes are added to the database for their respective scenes
5. Click Regenerate All to see the imported notes in the scene

### Duplicate handling

If you import the same JSON file twice, Scene Notes checks note IDs to avoid creating duplicates. Only new notes are added to the database.

### Multi-scene imports

A single JSON file may contain notes from multiple scenes (if the tester played through several scenes in one session). On import, notes are automatically sorted into the correct scene database. You will see notes from the current scene immediately. Switch to other scenes and regenerate to see their notes.

## QA team workflow

Here is a recommended workflow for teams with dedicated QA testers:

### Setup (one time)

1. Configure Scene Notes settings for your project
2. Set the hotkey to something that does not conflict with game controls
3. Build the project and distribute to your QA team
4. Tell testers the hotkey and ask them to set their author name in the in-game settings (if exposed) or pre-configure it in the build

### Each testing session

1. Tester plays the build normally
2. When they find an issue, they press the hotkey
3. They type a description and select a note type
4. They continue playing and repeat for each issue
5. When done, they quit the application
6. They send the JSON file to the development team (via email, Slack, shared drive, etc.)

### Processing feedback

1. Developer opens the project in Unity
2. Imports the JSON file via Scene Notes Manager
3. Opens each scene that has imported notes
4. Clicks through notes in the manager to review each issue at its exact location
5. Fixes issues and marks notes as resolved
6. Exports a CSV for the project tracker if needed

## JSON file format

The JSON export uses a simple array format:

```json
[
  {
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "description": "Player falls through floor here",
    "noteTypeName": "Critical",
    "worldPosition": { "x": -12.4, "y": 0.0, "z": 33.7 },
    "sceneName": "Level_01",
    "authorName": "QA_Tester_1",
    "dateTime": "2026-03-29T14:14:00",
    "isResolved": false
  }
]
```

This format is human-readable and can be parsed by external tools if needed.
