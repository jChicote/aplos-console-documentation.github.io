# OverviewLoggerView

`OverviewLoggerView` is a `MonoBehaviour` (namespace `AplosConsole.Logger`) that renders an on-screen
overview log. It captures Unity log messages, spawns a coloured entry for each, trims the visible
list and retained history to their configured caps, and can export the history to a text file. It
is scanned as a [`DebugGroup`](debug-group-attribute.md) named `"Overview Logger"`.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ OverviewLoggerView
```

</details>
<br>

**Inherited Members:**

- `MonoBehaviour.IsInvoking()`
- `MonoBehaviour.CancelInvoke()`
- `MonoBehaviour.StartCoroutine(IEnumerator)`
- `MonoBehaviour.StopCoroutine(Coroutine)`
- `MonoBehaviour.StopAllCoroutines()`
- `Behaviour.enabled`
- `Component.gameObject`
- `Component.transform`
- `Object.name`
- …

***Namespace***: `AplosConsole.Logger` <br>
***Implements***: `IColorSettingsApplicable`, [`ISettingsApplicable`](settings-interfaces.md#isettingsapplicable), [`IExportableLogSettings`](overview-log-interfaces.md#iexportablelogsettings)

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `LogTextColor` | `Color` | Text colour for standard log entries. Defaults to white. |
| `LogErrorColor` | `Color` | Text colour for exception entries. Defaults to red. |
| `LogWarningColor` | `Color` | Text colour for warning entries. Defaults to yellow. |
| `LogBackgroundColor` | `Color` | Background colour applied to every log entry. Defaults to semi-transparent black. |
| `MaxLogDisplayCount` | `int` | Maximum number of entries shown on screen at once; older visible entries are trimmed. Range 10–500, defaults to `20`. |
| `MaxHistoryCount` | `int` | Maximum number of entries retained in the exportable history. Range 10–500, defaults to `20`. |
| `ShowOverviewLogger` | `bool` | Whether the overview log display is visible. Defaults to `false`. |
| `IsSuppressLoggingOnStartAndReset` | `bool` | When `true`, skips capturing the noisy messages emitted while the settings manager is booting or running a full reset. Defaults to `true`. |
| `ExportPath` | `string` | Filesystem path (file or directory) that exported logs are written to. Defaults to the desktop when left empty. |
| `ExportButton` | `DebugButton` | Runtime-only debug button that triggers `ExportLogs`. Created on `Awake` and not persisted. |

## Public methods

<h2 id="onshow"><code>OnShow</code></h2>

**Example**

```csharp
overviewLogger.OnShow();
```

**Description:** Activates the log display content so entries are visible.

<br>

<h2 id="onhide"><code>OnHide</code></h2>

**Example**

```csharp
overviewLogger.OnHide();
```

**Description:** Deactivates the log display content so it is hidden.

<br>

<h2 id="applycolorsettings"><code>ApplyColorSettings</code></h2>

**Example**

```csharp
overviewLogger.ApplyColorSettings();
```

**Description:** Reapplies the configured colours to every active log entry, matching each entry's colour to its log type. Implements `IColorSettingsApplicable`.

<br>

<h2 id="applysettings"><code>ApplySettings</code></h2>

**Example**

```csharp
overviewLogger.ApplySettings();
```

**Description:** Shows or hides the display according to `ShowOverviewLogger`, then trims the visible entries down to `MaxLogDisplayCount`. Implements [`ISettingsApplicable`](settings-interfaces.md#isettingsapplicable).

<br>

<h2 id="exportlogs"><code>ExportLogs</code></h2>

**Example**

```csharp
overviewLogger.ExportLogs();
```

**Description:** Writes the retained history to a UTF-8 text file at `ExportPath` (appending a timestamped filename when the path is a directory), logging an error if the path is empty or the write fails. Implements [`IExportableLogSettings`](overview-log-interfaces.md#iexportablelogsettings), and is also wired to `ExportButton`.

<br>
