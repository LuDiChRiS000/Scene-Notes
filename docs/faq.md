# FAQ and troubleshooting

## Frequently asked questions

### Does Scene Notes affect game performance?

No. During normal gameplay, the only runtime cost is a single `Input.GetKeyDown` check per frame to detect the hotkey. Note objects are standard GameObjects with a lightweight billboard script. The controller also checks for render-on-top setting changes once per frame, which is negligible.

### Can I use Scene Notes in a shipped game?

Scene Notes is designed as a development and QA tool. While it works in builds, you should remove or disable the SceneNotesCanvas GameObject before your final release build to prevent players from accessing the note creation UI.

### Do notes survive scene changes?

Yes. Notes are stored in a ScriptableObject database, not as scene objects. The database persists independently of scene loading. Notes are tagged with their scene name, so each scene's notes are tracked separately. The SceneNotesController uses `DontDestroyOnLoad` to persist across scene changes in play mode.

### How does the cursor work when creating notes?

When you press the hotkey, Scene Notes stores your current cursor lock state and visibility. The cursor is unlocked and made visible so you can interact with the creation UI. When you confirm or cancel, the cursor state is restored to exactly what it was before — so cursor-locked FPS games return to their locked state seamlessly.

### Can multiple team members use Scene Notes?

Yes. Each team member sets their own author name in settings. In standalone builds, each tester's notes are saved to a separate JSON file that can be imported into the editor. The import system uses note IDs to prevent duplicates when the same file is imported twice.

For editor-based workflows, the ScriptableObject database can be committed to version control. If merge conflicts occur, the recommended approach is to have each developer export to JSON and merge through the import system instead.

### What render pipelines are supported?

Scene Notes works with Built-in, URP, and HDRP. The note prefab uses a custom NoteUnlit shader that supports per-material ZTest control for the render-on-top feature. If the NoteUnlit shader is not found (for example, if shader files are missing), it falls back to Unity's built-in Unlit/Color shader.

### Can I customise the note appearance?

Yes. You can replace the default note prefab with your own by assigning a different prefab in the Note Prefab 3D or Note Prefab 2D fields in settings. Your custom prefab must have a SceneNoteObject component attached with its serialised references wired to your text and renderer components.

### What happens when I change the Render on Top setting?

The change is detected automatically at runtime and applied to all existing note objects without needing to regenerate. The SceneNotesController monitors the setting each frame and calls `RefreshRenderSettings()` on all notes when it changes.

### Can other scripts react to the note creation panel?

Yes. Subscribe to the static event `SceneNoteCreator.OnCreationCanvasToggled`. It fires with `true` when the panel opens and `false` when it closes. This is useful for pausing your own systems or disabling input while the note panel is active.

```csharp
SceneNoteCreator.OnCreationCanvasToggled += (bool isOpen) =>
{
    // Disable your input system or pause your game logic
};
```

## Troubleshooting

### The hotkey does not work during play mode

1. Verify the SceneNotesCanvas is in the scene and its components are enabled
2. Check that the hotkey is not being consumed by your game's input system before it reaches Scene Notes
3. If using the new Input System package, ensure both input backends are active: Project Settings → Player → Active Input Handling → Both
4. Check the Console for any error messages from Scene Notes

### Notes do not appear after exiting play mode

1. Check that Auto-regenerate on Play Mode Exit is enabled in settings
2. Verify the SceneNotesDatabase asset exists and is referenced in settings
3. Open the Settings Inspector and check the validation section for errors
4. Try clicking Regenerate All in the Scene Notes Manager or on the Settings Inspector
5. Check the Console — the regeneration logs how many notes were spawned

### Notes appear at the wrong position

1. Check your spawn mode matches your game type (see [Placement modes](spawn-modes.md))
2. In Player Position mode, verify the Player Reference is assigned or the player has the "Player" tag
3. In Cursor Raycast mode, ensure your ground or surfaces have colliders — the raycast needs something to hit
4. Check the Raycast Layer Mask — excluded layers will not receive notes
5. In 2D mode, check the Note Z Depth setting

### Note colours are wrong or missing

Note type colours are applied via MaterialPropertyBlock on the header renderer. If colours appear grey:

1. Check that the note type names in your database match the names in your settings exactly
2. Try running Regenerate All to rebuild the notes with fresh colour data
3. After entering and exiting play mode, the regeneration should restore colours automatically

### The note creation UI does not respond to input

1. Verify there is an EventSystem in the scene — Scene Notes creates one automatically if none exists, but custom setups may interfere
2. Check that the Canvas sort order (999) is higher than any other canvas in your scene
3. In builds, ensure the Canvas, its child objects, and the EventSystem are not stripped by build optimisation

### CSV export produces unexpected results

1. Check the filter bar — hidden types are excluded from the export
2. Verify the export path in settings is writable
3. Descriptions containing commas, quotes, or newlines are escaped automatically using RFC-4180 rules

### The demo scene is missing notes

Run the demo scene creation again: Tools → Scene Notes → 3. Create Demo Scene. This seeds fresh notes into the database and spawns them in the scene. Make sure you run steps 1 and 2 first if you have not already.

## Getting help

If your issue is not covered here:

- Join our Discord for community support: [https://discord.gg/DSUd2QcyHZ](https://discord.gg/DSUd2QcyHZ)
- Check the Settings Inspector validation panel for configuration issues
- Report bugs via the Discord support channel
- Request features — we actively develop Scene Notes and community feedback shapes our roadmap
