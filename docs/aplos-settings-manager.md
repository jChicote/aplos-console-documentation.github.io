# AplosSettingsManager

`AplosSettingsManager` discovers `[DebugGroup]` components and their `[DebugSetting]` fields
across the scene, then saves, loads, previews, and resets those values through an
`ISettingsStore`. It is a `MonoBehaviour` singleton (namespace `AplosConsole.Settings`) that
implements `ISettingsService`.

## Properties

| Name | Description |
| --- | --- |
| `Instance` | Static singleton reference to the active settings manager. Assigned on `Awake`, read-only from outside the class. |
| `EnableColorSettingsScan` | Static, read-only hard toggle. When `false`, colour-based settings are excluded everywhere — neither persisted to the JSON file nor surfaced as editable options on the settings screen. |
| `IsProcessing` | `true` while a scan/load/save phase is running. Opt-in loggers watch this flag to suppress the routine scan/load/save messages. Read-only from outside the class. |
| `HasLoadedSettings` | `true` once settings have been successfully loaded from disk. Read-only from outside the class. |
| `SettingsStore` | The backing store used to read and write the settings JSON. Defaults to a `FileSettingsStore` for the configured file name; settable to inject an alternative store. |
| `ResetConsoleButton` | Runtime-built `DebugButton` surfaced on the settings screen that triggers the reset-to-defaults flow behind a confirmation modal. Not serialized. |
| `SuppressProcessLogs` | When `true`, hides the routine scan, load, and save log messages. Surfaced as a `[DebugSetting]` toggle. |

<details>
<summary>Declarations</summary>

```csharp
public static AplosSettingsManager Instance { get; private set; }
public static readonly bool EnableColorSettingsScan;
public bool IsProcessing { get; private set; }
public bool HasLoadedSettings { get; private set; }
public ISettingsStore SettingsStore { get; set; }
public DebugButton ResetConsoleButton;
public bool SuppressProcessLogs;
```

</details>

## Events

| Name | Description |
| --- | --- |
| `SettingsLoaded` | Raised after `Load()` successfully applies the saved settings. |

<details>
<summary>Declarations</summary>

```csharp
public UnityEvent SettingsLoaded;
```

</details>

## Public methods

| Name | Description |
| --- | --- |
| `GetAllScannedGroups` | Returns the collection of groups discovered by the most recent scan. |
| `ApplySettingsTo` | Applies the persisted settings to a freshly spawned object (e.g. a runtime window) so it matches the saved configuration immediately, without waiting for the next full scene rescan. |
| `RefreshGroups` | Re-scans the scene for `[DebugGroup]` objects and re-applies the saved values on top. Call this whenever the settings view is opened so newly-active groups are captured. |
| `Save` | Serializes all discovered `[DebugSetting]` field values and writes them to disk. |
| `Load` | Reads the JSON file and pushes matching values back into every live field. Groups or fields absent from the file keep their current values. |
| `PreviewJson` | Returns the serialized JSON for the current field values without saving. |
| `ResetAll` | Resets every discovered `[DebugSetting]` field to the value it had when first scanned (the authored default). |
| `ResetAllToDefaultsAndSave` | Full console reset: re-scans the scene, restores every field to its authored default, pushes those defaults into the live visuals, then persists them as the new saved configuration. |

<details>
<summary>Declarations</summary>

```csharp
public ICollection<ScannedGroup> GetAllScannedGroups();
public void ApplySettingsTo(GameObject root, bool includeChildren = true);
public void RefreshGroups();
public void Save();
public void Load();
public string PreviewJson();
public void ResetAll();
public void ResetAllToDefaultsAndSave();
```

</details>

## Static methods

_This class currently exposes no public static methods. Global access is provided through the static `Instance` property listed under [Properties](#properties)._
