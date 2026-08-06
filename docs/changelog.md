# Changelog

Release history and version notes for Aplos Console.

## 1.1.0 — Unreleased

A maintenance release covering package structure, editor tooling, and reliability fixes.

### Package

- Reorganised the package under `Assets/Lumencore-Studios/AplosConsole`, with runtime scripts, prefabs, and art gathered under `Runtime`. The old `Assets/Release` folder is gone.
- Editor code moved into its own `AplosConsoleEditor` assembly, separate from the `AplosConsoleScripts` runtime assembly, so editor-only types no longer reach player builds.
- The `Debug_InputSystem_Asset` Input Actions asset now ships with the package rather than living in the host project.
- Added the `Example_AplosConsole` sample scene under `Sample`, with the console, input, and example commands already wired up.

### Editor

- Added the **Window → Aplos Console → Utility** window, showing the installed version alongside shortcuts to the documentation, getting started guide, and changelog. It opens automatically the first time the package is imported.
- **Window → Aplos Console → Documentation** now falls back to serving the documentation bundled with the package on `localhost:8080` when the online site cannot be reached.

### Console

- Commands are no longer registered twice. A command whose id is already taken is rejected with a warning, and a constructor class referenced from both `AddOnCommands` and the command configuration now contributes its commands once, with `AddOnCommands` taking priority.
- `RefreshCommands` rebuilds from a cleared list, so repeated refreshes no longer accumulate duplicate entries. Runtime registrations are carried back over unless a rebuilt command has claimed the same id.
- Empty or destroyed entries in `AddOnCommands` and the command configuration are skipped instead of aborting initialisation.
- Command searching and auto-complete are now case-sensitive, matching the console's own validation.

### Settings

- Settings are written to a temporary file and swapped into place, so an interrupted save can no longer leave a half-written configuration on disk.
- A truncated settings file is now treated as missing values, leaving the current settings untouched rather than failing to load.

### Windows

- Fixed the window resize handles.

### Overview log

- The overview log no longer recurses when handling a log raised by its own display, and missing display dependencies are reported once instead of on every message.

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
