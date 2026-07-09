# Interfaces

The color picker is expressed through one contract in the `AplosConsole.Views.ColorPicker`
namespace. `IColorPicker` is the surface consumers use to open a color picker, implemented by
[AplosColorPickerView](aplos-color-picker-view.md).

## IColorPicker

Contract for a color picker that can be opened with an initial color and notified of the result
via callbacks.

### Methods

| Name | Description |
| --- | --- |
| `Show(Color initial, UnityAction<Color> onApply, UnityAction onCancel = null)` | Opens the color picker with the given initial color (R, G, B, A), invoking `onApply` once the color is applied or `onCancel` if the picker is cancelled. |
