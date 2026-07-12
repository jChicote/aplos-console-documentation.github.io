# AplosWindowSettings

`AplosWindowSettings` is the single source of truth for the shared window settings — the bar
colours, the resize bounds, the logo presentation, and the window scale. It is a
`MonoBehaviour` singleton (namespace `AplosConsole.Windows.Components`) that implements
`IColorSettingsApplicable` and [`ISettingsApplicable`](settings-interfaces.md#isettingsapplicable).
It is scanned as a [`DebugGroup`](debug-group-attribute.md) named `"Window Bar"`.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ AplosWindowSettings
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

***Namespace***: `AplosConsole.Windows.Components` <br>
***Implements***: `IColorSettingsApplicable`, [`ISettingsApplicable`](settings-interfaces.md#isettingsapplicable)

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `Instance` | `AplosWindowSettings` | Static singleton accessor. Returns the existing instance, otherwise finds one in the scene, otherwise creates a new `GameObject` carrying the component. Read-only. |
| `barBackgroundColor` | `Color` | Colour applied to the window bar background. |
| `closeButtonColor` | `Color` | Colour applied to the close button. |
| `collapseButtonColor` | `Color` | Colour applied to the collapse button. |
| `settingsButtonColor` | `Color` | Colour applied to the settings button. |
| `MinWidth` | `int` | Minimum window width (resize lower bound). Range 200–1080. |
| `MaxWidth` | `int` | Maximum window width (resize upper bound). Range 200–1080. |
| `MinHeight` | `int` | Minimum window height (resize lower bound). Range 200–1080. |
| `MaxHeight` | `int` | Maximum window height (resize upper bound). Range 200–1080. |
| `SmallLogoWidthThreshold` | `float` | Window width below which the compact logo is shown. Range 300–1080. |
| `ScaledCanvas` | `Canvas` | The `Canvas` whose reference resolution is scaled by `WindowScale`. |
| `WindowScale` | `float` | Multiplier applied to the canvas reference resolution. Range 1–10. |

## Public methods

<h2 id="register"><code>Register</code></h2>

**Parameters:**

- `handler` (`AplosWindowHandler`) — The window handler to track.

**Example**

```csharp
AplosWindowSettings.Instance.Register(windowHandler);
```

**Description:** Registers a window so it tracks the shared colors, and applies the current colors to it straight away.

<br>

<h2 id="unregister"><code>Unregister</code></h2>

**Parameters:**

- `handler` (`AplosWindowHandler`) — The window handler to stop tracking.

**Example**

```csharp
AplosWindowSettings.Instance.Unregister(windowHandler);
```

**Description:** Stops tracking a previously registered window.

<br>

<h2 id="applycolorsettings"><code>ApplyColorSettings</code></h2>

**Example**

```csharp
AplosWindowSettings.Instance.ApplyColorSettings();
```

**Description:** Reapplies the current bar colors to every registered window. Implements `IColorSettingsApplicable`.

<br>

<h2 id="register-2"><code>Register</code></h2>

**Parameters:**

- `handler` (`WindowResizingHandler`) — The resizer to track.

**Example**

```csharp
AplosWindowSettings.Instance.Register(resizingHandler);
```

**Description:** Registers a resizer so it tracks the shared bounds, and seeds it with the current bounds straight away.

<br>

<h2 id="unregister-2"><code>Unregister</code></h2>

**Parameters:**

- `handler` (`WindowResizingHandler`) — The resizer to stop tracking.

**Example**

```csharp
AplosWindowSettings.Instance.Unregister(resizingHandler);
```

**Description:** Stops tracking a previously registered resizer.

<br>

<h2 id="applysettings"><code>ApplySettings</code></h2>

**Example**

```csharp
AplosWindowSettings.Instance.ApplySettings();
```

**Description:** Applies derived settings to resize the window: re-seeds the resize bounds, refreshes logo views against the width threshold, and applies the window scale. Implements `ISettingsApplicable`.

<br>

<h2 id="register-3"><code>Register</code></h2>

**Parameters:**

- `view` (`WindowLogoView`) — The logo view to track.

**Example**

```csharp
AplosWindowSettings.Instance.Register(logoView);
```

**Description:** Registers a logo view so it tracks the shared width threshold, and seeds it with the current value straight away.

<br>

<h2 id="unregister-3"><code>Unregister</code></h2>

**Parameters:**

- `view` (`WindowLogoView`) — The logo view to stop tracking.

**Example**

```csharp
AplosWindowSettings.Instance.Unregister(logoView);
```

**Description:** Stops tracking a previously registered logo view.

<br>
