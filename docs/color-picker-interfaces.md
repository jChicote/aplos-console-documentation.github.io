# Interfaces

## IColorPicker

Contract for a color picker that can be opened with an initial color and notified of the result
via callbacks. Implemented by [AplosColorPickerView](aplos-color-picker-view.md).

***Namespace***: `AplosConsole.Views.ColorPicker`

### Public methods

<h2 id="show"><code>Show</code></h2>

**Parameters:**

- `initial` (`Color`) — Initial color (R, G, B, A).
- `onApply` (`UnityAction<Color>`) — Action to call once the color is applied.
- `onCancel` (`UnityAction`) — Action to call if the color picker is cancelled. Defaults to `null`.

**Example**

```csharp
colorPicker.Show(Color.white, color => { /* apply the chosen color */ });
```

**Description:** Opens the color picker with the given initial color, invoking `onApply` once the color is applied or `onCancel` if the picker is cancelled.

<br>
