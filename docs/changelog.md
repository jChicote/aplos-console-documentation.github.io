# Changelog

Release history and version notes for Aplos Console.

## 1.0.0 — 2026-07-14

First public release of Aplos Console, an in-game developer console for Unity.

### Console

- `AplosConsole` singleton that manages command registration and drives the console's open, close, and input actions.
- `AplosConsoleCommandConstructor` for assembling and registering commands at runtime.

### Command system

- `AplosDebugCommand` type for defining named, callable console commands.
- `AplosCommandConfiguration` `ScriptableObject` that bundles command actions and console prefabs, created from the `AplosConsole/Aplos Command Configuration` asset menu.

### Windows

- `AplosWindowManager` that opens, tracks, and tears down runtime windows spawned by the console through an `AplosWindowFactory`.
- `AplosWindowRequest` and `AplosWindowSettings` for describing and styling spawned windows, with a saved settings palette applied to each new window.

### Colour picker

- `AplosColorPickerView`, an HSV-based colour picker tying together the saturation/value field, hue and alpha rails, hex + RGBA inputs, and preview swatches.
- `AplosColorPalette` for defining and reusing named colours.

### Settings

- `AplosSettingsManager` that discovers `[DebugGroup]` components and their `[DebugSetting]` fields across the scene, then saves, loads, previews, and resets values through an `ISettingsStore`.
- `DebugSettingsScanner` that discovers debug groups and settings via reflection, returning them sorted by group order then name.
- `[DebugSetting]` and `[DebugGroup]` attributes for exposing fields and grouping them in the settings UI.

### Input

- `AplosInputManager` that wires the console's debug input bindings to Unity's Input System, resolving the active control scheme and binding the matching mapper against a `PlayerInput`.
- `DebugInputActionMapper` for mapping control schemes to console input, and `AplosConsoleInputAdapterBase` as the extension point for custom input backends.

### Overview log

- `OverviewLoggerView` that captures Unity log messages, renders an on-screen overview log with per-entry colouring, trims the visible list and history to configured caps, and can export the history to a text file.

### Known issues

- Tested on Mac and Windows, not suited for touch screen or VR implementations yet.
- The collapse button may be pointing in the wrong direction when toggled.
- Duplicate debug groups being scanned may not present the correct instance from the settings view
- Expanding the window when collapsed window is near button of screen will not reposition upwards.
- Overflow of elements not handled correctly when scaled extremely small
- Occasionally, input field text may not change when selecting on the commands visually
