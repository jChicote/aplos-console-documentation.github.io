# Interfaces

The settings system is expressed through four contracts in the `AplosConsole.Settings` namespace
(with `ISettingsStore` in the nested `AplosConsole.Settings.Persistence` namespace).
`IResettable` and `ISettingsApplicable` are implemented by individual settings-bearing
components to be collected and driven by the [AplosSettingsManager](aplos-settings-manager.md).
`ISettingsService` is the surface consumers use to apply persisted settings to spawned objects,
and `ISettingsStore` abstracts the underlying persistence mechanism from the manager that
serializes and applies it.

## IResettable

Contract representing components that implement resettable field options to be collected and
managed by the [AplosSettingsManager](aplos-settings-manager.md).

### Methods

| Name | Description |
| --- | --- |
| `ResetToDefaults()` | Discards persisted state and restores authored defaults, on disk and live. |

## ISettingsApplicable

Generalised apply-hook contract for pushing loaded field values into live runtime state.

### Methods

| Name | Description |
| --- | --- |
| `ApplySettings()` | Pushes loaded field values into live runtime state. Excludes the color state of the given UI element. |

## ISettingsService

Lets components react to settings being (re)loaded and apply the saved palette to a spawned
object.

### Properties

| Name | Description |
| --- | --- |
| `HasLoadedSettings` | True once a saved configuration has been loaded and pushed to visuals. |
| `SettingsLoaded` | `UnityEvent` raised after each load so consumers can (re)apply without ordering assumptions. |

### Methods

| Name | Description |
| --- | --- |
| `ApplySettingsTo(GameObject root, bool includeChildren = true)` | Applies the persisted settings to a freshly spawned object (e.g. a runtime window). |

## ISettingsStore

_Internal contract._ Persists and restores the raw settings-configuration JSON, abstracting the
backing store (file, prefs, ...) from the settings manager that serializes and applies it.

### Methods

| Name | Description |
| --- | --- |
| `TryLoad(out string json)` | Returns the stored JSON when a saved configuration exists and could be read; returns `false` (with the defaults left in place) otherwise. |
| `Save(string json)` | Persists the given JSON to the backing store. |
