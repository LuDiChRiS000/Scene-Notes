# FAQ and troubleshooting

## Frequently asked questions

### Does Scene Notes affect game performance?

No. Scene Notes has no runtime cost during normal gameplay. The only performance impact is a single `Input.GetKeyDown` check per frame to detect the hotkey, which is negligible. Note objects in the scene are standard GameObjects with minimal components.

### Can I use Scene Notes in a shipped game?

Scene Notes is designed as a development and QA tool. While it technically works in builds, you should remove or disable the SceneNotesController before your final release build to prevent players from accessing the note creation UI.

### Do notes survive scene changes?

Notes are stored in a ScriptableObject database, not as scene objects. The database persists independently of scene loading. When you switch scenes and come back, your notes are still in the database. Click Regenerate All in the Scene Notes Manager to rebuild the note objects.

### Can multiple team members use Scene Notes simultaneously?

Each team member can create notes in their own editor or build session. Notes from builds are exported as JSON files that can be imported and merged in the editor. In the editor, notes are stored in the ScriptableObject, which can be committed to version control. Set different author names in settings so notes can be attributed correctly.

### Does Scene Notes work with version control?

Yes. The ScriptableObject database is a standard Unity asset file that works with Git, Perforce, SVN, and other version control systems. If two team members create notes in the same scene simultaneously (in separate editor sessions), you may need to handle merge conflicts on the database asset.

For team workflows, the recommended approach is to have each developer export to CSV or JSON and merge notes through the import system rather than committing the database directly.

### What render pipelines are supported?

Scene Notes works with Built-in, URP, and HDRP. The note prefab uses an unlit material that is compatible with all pipelines. If you use a custom render pipeline, you may need to adjust the note material.

### Can I change the look of the sticky notes?

Yes. You can replace the default note prefab with your own custom prefab. Your prefab must have a SceneNoteObject component attached. The component handles data binding — your prefab can use any mesh, material, or visual style you prefer.

## Troubleshooting

### The hotkey does not work during play mode

Check these common causes:

1. Make sure the hotkey is not being consumed by your game's input system. Some input managers intercept all key presses before they reach other systems.
2. Verify the SceneNotesController is present in the scene and enabled.
3. Check the Console for any error messages from Scene Notes.
4. If using the new Input System, ensure Scene Notes is set up to use the legacy Input Manager or that both input backends are active (Project Settings > Player > Active Input Handling > Both).

### Notes do not appear after exiting play mode

Check these common causes:

1. Make sure Auto-regenerate on Play Mode Exit is enabled in settings.
2. Verify the SceneNotesDatabase asset exists and is referenced in settings.
3. Check the Console for any error messages during the regeneration step.
4. Try clicking Regenerate All in the Scene Notes Manager window manually.

### Notes appear at the wrong position

This can happen if:

1. The player reference Transform is wrong or has moved since the note was created.
2. In Cursor Raycast mode, the raycast is hitting an unexpected collider (check your layer mask).
3. The scene's coordinate system has changed (objects reparented or moved).
4. In 2D mode, the Z depth setting may place notes behind other objects.

### The note creation UI does not appear

1. Check that the SceneNotesCanvas prefab is present and referenced by the controller.
2. In standalone builds, ensure the Canvas is included in the build (not stripped).
3. Verify there is an EventSystem in the scene — UI input requires one.

### CSV export produces an empty file

1. Make sure there are notes in the current scene's database.
2. Check the filter settings — if all types are hidden, the export will be empty.
3. Verify the export path in settings is writable.

### Cannot import JSON from a build

1. Verify the JSON file is valid — open it in a text editor and check for malformed data.
2. Make sure the scene names in the JSON match your current scene names exactly. If you renamed a scene after the build was created, the import will not match those notes to any scene.
3. Check the Console for any parsing errors during import.

### Notes are too small or too large in the scene

Adjust the Note Scale setting in the Scene Notes Settings asset. The default scale of 1.0 works for most projects, but large open-world scenes may need a larger scale (2.0 or 3.0) while small indoor scenes may need a smaller scale (0.5).

## Getting help

If your issue is not covered here:

- Join our Discord for community support: [https://discord.gg/DSUd2QcyHZ](https://discord.gg/DSUd2QcyHZ)
- Report bugs via the Discord support channel
- Request features — we actively develop Scene Notes and community feedback shapes our roadmap
