# AplosSettingsManager

`AplosSettingsManager` discovers `[DebugGroup]` components and their `[DebugSetting]` fields
across the scene, then saves, loads, previews, and resets those values through an
`ISettingsStore`. The manager itself is scanned as a
[`DebugGroup`](debug-group-attribute.md) named `"Console"` (order 100).

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ AplosSettingsManager
```

</details>
<br>

**Inherited Members:**

- `MonoBehaviour.IsInvoking()`
- `MonoBehaviour.CancelInvoke()`
- `MonoBehaviour.Invoke(string, float)`
- `MonoBehaviour.InvokeRepeating(string, float, float)`
- `MonoBehaviour.CancelInvoke(string)`
- `MonoBehaviour.StartCoroutine(IEnumerator)`
- `MonoBehaviour.StopCoroutine(Coroutine)`
- `MonoBehaviour.StopAllCoroutines()`
- `Behaviour.enabled`
- `Component.gameObject`
- `Component.transform`
- `Object.name`
- …

***Namespace***: `AplosConsole.Settings` <br>
***Implements***: [`ISettingsService`](settings-interfaces.md#isettingsservice)

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `Instance` | `AplosSettingsManager` | Static singleton reference to the active settings manager. Assigned on `Awake`, read-only from outside the class. |
| `EnableColorSettingsScan` | `bool` | Static, read-only hard toggle. When `false`, colour-based settings are excluded everywhere — neither persisted to the JSON file nor surfaced as editable options on the settings screen. |
| `IsProcessing` | `bool` | `true` while a scan/load/save phase is running. Opt-in loggers watch this flag to suppress the routine scan/load/save messages. Read-only from outside the class. |
| `HasLoadedSettings` | `bool` | `true` once settings have been successfully loaded from disk. Read-only from outside the class. Implements `ISettingsService.HasLoadedSettings`. |
| `SettingsStore` | [`ISettingsStore`](settings-interfaces.md#isettingsstore) | The backing store used to read and write the settings JSON. Defaults to a `FileSettingsStore` for the configured file name; settable to inject an alternative store. |
| `SuppressProcessLogs` | `bool` | When `true`, hides the routine scan, load, and save log messages. Surfaced as a `[DebugSetting]` toggle. |

## Events

| Name | Data Type | Description |
| --- | --- | --- |
| `SettingsLoaded` | `UnityEvent` | Raised after `Load()` successfully applies the saved settings. Also surfaced explicitly as `ISettingsService.SettingsLoaded`. |

## Public methods

<h2 id="getallscannedgroups"><code>GetAllScannedGroups</code></h2>

**Example**

```csharp
var groups = AplosSettingsManager.Instance.GetAllScannedGroups();
```

**Description:** Returns the collection of groups discovered by the most recent scan.

<br>

<h2 id="applysettingsto"><code>ApplySettingsTo</code></h2>

**Parameters:**

- `root` (`GameObject`) — The freshly spawned object to apply the saved settings to.
- `includeChildren` (`bool`) — Whether to include inactive children when scanning `root` for `[DebugGroup]` components. Defaults to `true`.

**Example**

```csharp
AplosSettingsManager.Instance.ApplySettingsTo(newWindow.gameObject);
```

**Description:** Applies the persisted settings to a freshly spawned object (e.g. a runtime window) so it matches the saved palette immediately, without waiting for the next full scene rescan. Settings are keyed by group name, so every window that shares a `[DebugGroup]` ends up with identical styling. Implements `ISettingsService.ApplySettingsTo`.

<br>

<h2 id="refreshgroups"><code>RefreshGroups</code></h2>

**Example**

```csharp
AplosSettingsManager.Instance.RefreshGroups();
```

**Description:** Re-scans the scene for `[DebugGroup]` objects and re-applies the saved values on top. Call this whenever the settings view is opened so newly-active groups are captured rather than relying on the one-off boot-time scan.

<br>

<h2 id="save"><code>Save</code></h2>

**Example**

```csharp
AplosSettingsManager.Instance.Save();
```

**Description:** Serializes all discovered `[DebugSetting]` field values and writes them to disk.

<br>

<h2 id="load"><code>Load</code></h2>

**Example**

```csharp
AplosSettingsManager.Instance.Load();
```

**Description:** Reads the JSON file and pushes matching values back into every live field. Groups or fields absent from the file keep their current values. Raises `SettingsLoaded` on success.

<br>

<h2 id="previewjson"><code>PreviewJson</code></h2>

**Example**

```csharp
string json = AplosSettingsManager.Instance.PreviewJson();
```

**Description:** Returns the serialized JSON for the current field values without saving.

<br>

<h2 id="resetall"><code>ResetAll</code></h2>

**Example**

```csharp
AplosSettingsManager.Instance.ResetAll();
```

**Description:** Resets every discovered `[DebugSetting]` field to the value it had when first scanned (the authored default), restored from the snapshot captured before any saved values were loaded.

<br>

<h2 id="resetalltodefaultsandsave"><code>ResetAllToDefaultsAndSave</code></h2>

**Example**

```csharp
AplosSettingsManager.Instance.ResetAllToDefaultsAndSave();
```

**Description:** Full console reset: re-scans the scene, restores every field to its authored default, pushes those defaults into the live visuals, then persists them as the new saved configuration.

<br>