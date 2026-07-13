# AplosColorPickerView

`AplosColorPickerView` is a `MonoBehaviour` (namespace `AplosConsole.Views.ColorPicker`) that ties
the saturation/value field, hue rail, alpha rail, hex + RGBA inputs, and preview swatches into one
HSV-based color picker. HSVA is the single source of truth and everything else is derived from it
on each refresh.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ AplosColorPickerView
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

***Namespace***: `AplosConsole.Views.ColorPicker` <br>
***Implements***: `IWindowIconProvider`, [`IColorPicker`](color-picker-interfaces.md#icolorpicker)

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `CurrentColor` | `Color` | The currently selected color, computed from the internal HSVA state. Read-only. |
| `WindowIcon` | `Sprite` | The icon shown in the host window's title bar. Read-only. |

## Events

| Name | Data Type | Description |
| --- | --- | --- |
| `onColorChanged` | `ColorChangedEvent` | Raised whenever the HSVA state changes and the UI is refreshed, passing the resulting color. |
| `onApplied` | `ColorChangedEvent` | Raised when the apply button is clicked (or the `Show` callback fires), passing the committed color. |
| `onCancelled` | `UnityEvent` | Raised when the cancel button is clicked (or the `Show` callback fires). |

## Public methods

<h2 id="show"><code>Show</code></h2>

**Parameters:**

- `initial` (`Color`) — Initial color to open the picker with.
- `onApply` (`UnityAction<Color>`) — Callback invoked once the color is applied.
- `onCancel` (`UnityAction`) — Callback invoked if the picker is cancelled. Defaults to `null`.

**Example**

```csharp
colorPickerView.Show(Color.white, color => { /* apply the chosen color */ });
```

**Description:** Opens the picker with the given initial color, temporarily wiring the supplied callbacks to `onApplied`/`onCancelled` for this session only. Implements [`IColorPicker.Show`](color-picker-interfaces.md#show).

<br>

<h2 id="provide"><code>Provide</code></h2>

**Example**

```csharp
Sprite icon = colorPickerView.Provide();
```

**Description:** Returns the `WindowIcon` sprite. Implements `IWindowIconProvider`.

<br>

<h2 id="commit"><code>Commit</code></h2>

**Example**

```csharp
colorPickerView.Commit();
```

**Description:** Accepts the current color as the new baseline, updating the "old" preview swatch.

<br>

<h2 id="cancel"><code>Cancel</code></h2>

**Example**

```csharp
colorPickerView.Cancel();
```

**Description:** Reverts the picker back to the initial color.

<br>
