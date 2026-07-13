# AplosColorPalette

`AplosColorPalette` is a `[Serializable]` struct that gathers the colours (and button styling)
applied across the console's UI. It is authored on the settings views and carried down to the
individual widgets, keeping their appearance in sync (namespace `AplosConsole.General`).

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ ValueType
    ↳ AplosColorPalette
```

</details>
<br>

**Inherited Members:**

- `ValueType.Equals(object)`
- `ValueType.GetHashCode()`
- `ValueType.ToString()`
- `object.GetType()`
- …

***Namespace***: `AplosConsole.General`

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `PrimaryText` | `Color` | Colour for primary text. |
| `PrimaryIcon` | `Color` | Colour for primary icons. |
| `PrimaryBackground` | `Color` | Colour for the primary background surface. |
| `ContentBackground` | `Color` | Colour for content-area backgrounds. |
| `OverlayBackground` | `Color` | Colour for overlay backgrounds drawn above content. |
| `GroupLabel` | `Color` | Colour for group heading labels. |
| `GroupBackground` | `Color` | Colour for group backgrounds. |
| `ListItemLabel` | `Color` | Colour for list-item labels. |
| `ListItemText` | `Color` | Colour for list-item body text. |
| `ListItemBackground` | `Color` | Colour for list-item backgrounds. |
| `ButtonStyle` | `AplosButtonStyle` | Styling applied to the buttons embedded in settings field options, carried down alongside the colour fields. |
