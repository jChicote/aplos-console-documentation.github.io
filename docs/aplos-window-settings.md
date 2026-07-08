# AplosWindowSettings

`AplosWindowSettings` is the single source of truth for the shared window settings — the bar
colours, the resize bounds, the logo presentation, and the window scale. It is a
`MonoBehaviour` singleton (namespace `AplosConsole.Windows.Components`) that implements
`IColorSettingsApplicable` and `ISettingsApplicable`.

## Properties

| Name | Description |
| --- | --- |
| `Instance` | Static singleton accessor. Returns the existing instance, otherwise finds one in the scene, otherwise creates a new `GameObject` carrying the component. Read-only. |
| `barBackgroundColor` | Colour applied to the window bar background. |
| `closeButtonColor` | Colour applied to the close button. |
| `collapseButtonColor` | Colour applied to the collapse button. |
| `settingsButtonColor` | Colour applied to the settings button. |
| `MinWidth` | Minimum window width (resize lower bound). Range 200–1080. |
| `MaxWidth` | Maximum window width (resize upper bound). Range 200–1080. |
| `MinHeight` | Minimum window height (resize lower bound). Range 200–1080. |
| `MaxHeight` | Maximum window height (resize upper bound). Range 200–1080. |
| `SmallLogoWidthThreshold` | Window width below which the compact logo is shown. Range 300–1080. |
| `ScaledCanvas` | The `Canvas` whose reference resolution is scaled by `WindowScale`. |
| `WindowScale` | Multiplier applied to the canvas reference resolution. Range 1–10. |

## Events

_This class exposes no events._

## Public methods

| Name | Description |
| --- | --- |
| `Register(AplosWindowHandler handler)` | Registers a window so it tracks the shared colours, and applies the current colours to it straight away. |
| `Unregister(AplosWindowHandler handler)` | Stops a window handler from tracking the shared colours. |
| `ApplyColorSettings()` | Re-applies the current bar colours to every registered window handler. Implements `IColorSettingsApplicable`. |
| `Register(WindowResizingHandler handler)` | Registers a resizer so it tracks the shared bounds, and seeds it with the current bounds straight away. |
| `Unregister(WindowResizingHandler handler)` | Stops a resizer from tracking the shared bounds. |
| `ApplySettings()` | Applies derived settings: re-seeds the resize bounds, refreshes logo views against the width threshold, and applies the window scale. Implements `ISettingsApplicable`. |
| `Register(WindowLogoView view)` | Registers a logo view so it tracks the shared width threshold, and seeds it with the current value straight away. |
| `Unregister(WindowLogoView view)` | Stops a logo view from tracking the shared width threshold. |

## Static methods

_This class currently exposes no public static methods. Global access is provided through the static `Instance` property listed under [Properties](#properties)._
