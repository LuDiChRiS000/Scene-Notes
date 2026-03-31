# Placement modes

Scene Notes supports three placement modes that determine where a note spawns when you press the hotkey. Choose the mode that matches your game type.

## Player Position

Notes spawn at your player character's location with a configurable offset.

This is the default mode and works best for games where you control a character directly: first-person shooters, third-person action games, platformers, side-scrollers, RPGs, and adventure games.

### How it works

When you press the hotkey, the note spawns at:

```
Player position + (right * offset.x) + (up * offset.y) + (forward * offset.z)
```

The default offset of (0, 0, 2) places the note 2 units in front of the player, which means it appears roughly where you are looking.

### Setup

1. Set Spawn Mode to Player Position in the settings
2. Drag your player GameObject into the Player Reference field
3. Adjust the Forward Offset if needed

### Tips

- For first-person games, an offset of (0, 0, 3) works well — the note appears a few metres ahead
- For third-person games with an overhead camera, try (0, 2, 0) to place notes above the player
- For side-scrolling 2D games, use (2, 0, 0) or (-2, 0, 0) depending on your character's facing direction

### Fallback behaviour

If the Player Reference is not set, Scene Notes looks for a GameObject tagged "Player" in the scene. If no player is found, a warning is logged and the note is not created.

## Cursor Raycast

Notes spawn wherever the mouse cursor is pointing in the world.

This mode is designed for games where the camera is detached from a player character: real-time strategy games, city builders, god games, tycoon games, top-down strategy, and any game with a free-floating camera.

### How it works

When you press the hotkey, a ray is cast from the mouse cursor position through the main camera into the scene. The note spawns at the first collider the ray hits.

In 3D mode, this uses `Physics.Raycast`. In 2D mode, this uses the camera's `ScreenToWorldPoint` with optional `Physics2D.Raycast`.

### Setup

1. Set Spawn Mode to Cursor Raycast in the settings
2. No player reference is needed
3. Adjust Max Raycast Distance and Fallback Ray Distance if needed

### Tips

- Make sure your terrain or ground plane has a collider — the raycast needs something to hit
- If the cursor is pointing at the sky or empty space, the note spawns at the fallback distance along the ray direction
- Use the Raycast Layer Mask to exclude layers you do not want notes placed on (UI, triggers, invisible volumes)

### Fallback behaviour

If the raycast does not hit any collider, the note spawns at the fallback distance from the camera along the ray direction. Default fallback is 20 units.

## Screen Centre Ray

Notes spawn at the point the centre of the screen is pointing at.

This mode is for games that hide the mouse cursor and use a crosshair or reticle: VR games, cursor-locked first-person shooters, and any game where the mouse is not used as a pointer.

### How it works

When you press the hotkey, a ray is cast from the exact centre of the screen (viewport position 0.5, 0.5) through the main camera. The note spawns at the first collider the ray hits.

This is identical to Cursor Raycast except the ray always originates from screen centre rather than the mouse position.

### Setup

1. Set Spawn Mode to Screen Centre Ray in the settings
2. No player reference is needed
3. Adjust Max Raycast Distance and Fallback Ray Distance if needed

### Tips

- This mode is ideal for VR because it places notes wherever the player is looking
- For cursor-locked FPS games, this places notes at whatever the crosshair is aimed at
- Same fallback behaviour as Cursor Raycast

## Choosing the right mode

| Game type | Recommended mode |
|-----------|-----------------|
| First-person shooter | Player Position or Screen Centre Ray |
| Third-person action/RPG | Player Position |
| Platformer (2D or 3D) | Player Position |
| Side-scroller | Player Position (2D mode) |
| RTS / strategy | Cursor Raycast |
| City builder / tycoon | Cursor Raycast |
| God game | Cursor Raycast |
| Top-down shooter | Cursor Raycast |
| VR game | Screen Centre Ray |
| Cursor-locked FPS | Screen Centre Ray |
| Editor/sandbox tool | Cursor Raycast |

## 2D vs 3D

All three placement modes work in both 2D and 3D projects. Enable 2D Mode in the settings to switch to 2D raycasting and sprite-based note objects.

In 2D mode, notes use XY coordinates for position and the Note Z Depth setting controls which sorting layer they appear on. Set a negative Z depth to place notes in front of your game art.
