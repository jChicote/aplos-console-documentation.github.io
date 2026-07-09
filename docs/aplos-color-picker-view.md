# AplosColorPickerView

`AplosColorPickerView` is a `MonoBehaviour` (namespace `AplosConsole.Views.ColorPicker`) that
implements `IWindowIconProvider` and `IColorPicker`. It ties the saturation/value field, hue
rail, alpha rail, hex + RGBA inputs, and preview swatches into one HSV-based color picker; HSVA
is the single source of truth and everything else is derived from it on each refresh.

## Properties

| Name | Description |
| --- | --- |
| `CurrentColor` | The currently selected color, computed from the internal HSVA state. |
| `WindowIcon` | The icon shown in the host window's title bar. |

## Events

| Name | Description |
| --- | --- |
| `onColorChanged` | Raised whenever the HSVA state changes and the UI is refreshed, passing the resulting color. |
| `onApplied` | Raised when the apply button is clicked (or the `Show` callback fires), passing the committed color. |
| `onCancelled` | Raised when the cancel button is clicked (or the `Show` callback fires). |

## Public methods

| Name | Description |
| --- | --- |
| `Show(Color initial, UnityAction<Color> onApply, UnityAction onCancel = null)` | Opens the picker with the given initial color, temporarily wiring the supplied callbacks to `onApplied`/`onCancelled` for this session only. |
| `Provide()` | Returns the `WindowIcon` sprite; implements `IWindowIconProvider`. |
| `Commit()` | Accepts the current color as the new baseline, updating the "old" preview swatch. |
| `Cancel()` | Reverts the picker back to the initial color. |

## Static methods

_This class currently exposes no static methods._
