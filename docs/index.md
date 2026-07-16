# Aplos Console

Welcome to the official documentation for **Aplos Console** — an in-game developer console for Unity.

## Contents

### Guides

- **[Getting Started](getting-started.md)** — installation, setup, and your first command.
    - [Installation](getting-started.md#installation)
    - [Adding the console to your scene](getting-started.md#adding-the-console-to-your-scene)
    - [Your first command](getting-started.md#your-first-command)
- **[Adding Commands](adding-commands.md)** — authoring, registering, and pre-loading console commands.
    - [How it works](adding-commands.md#how-it-works)
    - [Developing commands](adding-commands.md#developing-commands)
    - [Adding commands during runtime](adding-commands.md#adding-commands-during-runtime)
    - [Configuring pre-loaded commands](adding-commands.md#configuring-pre-loaded-commands)
- **[Setting up Input](setting-up-input.md)** — wiring device input into the console and configuring the components that drive it.
    - [How it works](setting-up-input.md#how-it-works)
    - [Configuring Input](setting-up-input.md#configuring-input)
- **[Using the Console](using-the-console.md)** — a tour of the runtime console and how you interact with each part.
    - [Parts of the console](using-the-console.md#parts-of-the-console)
- **[Using the Settings](using-the-settings.md)** — exposing fields so the settings system can track, persist, and restore them.
    - [Configuring a field for tracking](using-the-settings.md#configuring-a-field-for-tracking)
    - [Manual operation](using-the-settings.md#manual-operation)
- **[Changelog](changelog.md)** — release history and version notes.
- **[About](about.md)** — overview, credits, and licensing.
    - [Overview](about.md#overview)
    - [Credits](about.md#credits)
    - [License](about.md#license)

### API reference

- **Console** — [AplosConsole](aplos-console.md), [AplosConsoleCommandConstructor](aplos-console-command-constructor.md), [Interfaces](console-interfaces.md)
- **Window** — [AplosWindowManager](aplos-window-manager.md), [AplosWindowRequest](aplos-window-request.md), [AplosWindowSettings](aplos-window-settings.md), [Interfaces](window-interfaces.md)
- **Command System** — [AplosCommandConfiguration](aplos-command-configuration.md), [AplosDebugCommand](aplos-debug-command.md), [Interfaces](command-system-interfaces.md)
- **Color Picker** — [AplosColorPalette](aplos-color-palette.md), [AplosColorPickerView](aplos-color-picker-view.md), [Interfaces](color-picker-interfaces.md)
- **Settings** — [AplosSettingsManager](aplos-settings-manager.md), [DebugSettingsScanner](debug-settings-scanner.md), [Interfaces](settings-interfaces.md)
- **Attributes** — [DebugSettingAttribute](debug-setting-attribute.md), [DebugGroupAttribute](debug-group-attribute.md)
- **Input** — [AplosInputManager](aplos-input-manager.md), [AplosConsoleInputAdapterBase](aplos-console-input-adapter-base.md), [DebugInputActionMapper](debug-input-action-mapper.md), [Interfaces](input-interfaces.md)
- **Overview Log** — [OverviewLoggerView](overview-logger-view.md), [Interfaces](overview-log-interfaces.md)
