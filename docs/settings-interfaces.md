# Interfaces

## IResettable

Contract representing components that implement resettable field options to be collected and
managed by the [AplosSettingsManager](aplos-settings-manager.md).

***Namespace***: `AplosConsole.Settings`

### Public methods

<h2 id="resettodefaults"><code>ResetToDefaults</code></h2>

**Example**

```csharp
public class MyResettableComponent : MonoBehaviour, IResettable
{
    public void ResetToDefaults()
    {
        // restore authored defaults
    }
}
```

**Description:** Discards persisted state and restores authored defaults, on disk and live.

<br>

## ISettingsApplicable

Generalised apply-hook contract for pushing loaded field values into live runtime state.

***Namespace***: `AplosConsole.Settings`

### Public methods

<h2 id="applysettings"><code>ApplySettings</code></h2>

**Example**

```csharp
public void ApplySettings()
{
    // push loaded field values into live runtime state
}
```

**Description:** Pushes the currently-loaded field values into live runtime state. Colour state is handled separately via `IColorSettingsApplicable`.

<br>

## ISettingsService

Lets components react to settings being (re)loaded and apply the saved palette to a spawned
object. Implemented by [AplosSettingsManager](aplos-settings-manager.md).

***Namespace***: `AplosConsole.Settings`

### Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `HasLoadedSettings` | `bool` | True once a saved configuration has been loaded and pushed to visuals. Read-only. |
| `SettingsLoaded` | `UnityEvent` | Raised after each load so consumers can (re)apply without ordering assumptions. Read-only. |

### Public methods

<h2 id="applysettingsto"><code>ApplySettingsTo</code></h2>

**Parameters:**

- `root` (`GameObject`) — The freshly spawned object to apply the saved settings to.
- `includeChildren` (`bool`) — Whether to include inactive children when applying settings. Defaults to `true`.

**Example**

```csharp
settingsService.ApplySettingsTo(newWindow.gameObject);
```

**Description:** Applies the persisted settings to a freshly spawned object (e.g. a runtime window).

<br>

## ISettingsStore

_Internal contract._ Persists and restores the raw settings-configuration JSON, abstracting the
backing store (file, prefs, ...) from the settings manager that serializes and applies it.

***Namespace***: `AplosConsole.Settings.Persistence`

### Public methods

<h2 id="tryload"><code>TryLoad</code></h2>

**Parameters:**

- `json` (`out string`) — The stored JSON, if a saved configuration exists and could be read.

**Example**

```csharp
if (settingsStore.TryLoad(out string json))
{
    // apply json
}
```

**Description:** Returns the stored JSON when a saved configuration exists and could be read; returns `false` (with the defaults left in place) otherwise.

<br>

<h2 id="save"><code>Save</code></h2>

**Parameters:**

- `json` (`string`) — The settings JSON to persist.

**Example**

```csharp
settingsStore.Save(json);
```

**Description:** Persists the given JSON to the backing store.

<br>