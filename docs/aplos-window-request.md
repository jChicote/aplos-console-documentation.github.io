# AplosWindowRequest

`AplosWindowRequest` describes how a window should be created and configured. It is passed to
[`AplosWindowManager.OpenWindow`](aplos-window-manager.md#openwindow), which uses it to spawn the
window's content, size it, and wire up its close behaviour. It is a plain class (namespace
`AplosConsole.Windows`) that implements no interfaces of its own.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ AplosWindowRequest
```

</details>
<br>

**Inherited Members:**

- `object.Equals(object)`
- `object.Equals(object, object)`
- `object.GetHashCode()`
- `object.GetType()`
- `object.ReferenceEquals(object, object)`
- `object.ToString()`

***Namespace***: `AplosConsole.Windows`

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `IsAutoClose` | `bool` | When true, the window destroys itself as soon as it is deactivated. Get/set. |
| `IsSettingsVisible` | `bool` | Whether the window's settings button is shown. Get/set. |
| `IsCollapseVisible` | `bool` | Whether the window's collapse button is shown. Get/set. |
| `IsLogoVisible` | `bool` | Whether the window's logo is shown. Get/set. |
| `IsShadowVisible` | `bool` | Whether the window's drop shadow is shown. Get/set. |
| `InitialSize` | `Vector2` | The window's size when it is first created. Get/set. |
| `MinSize` | `Vector2?` | Optional lower bound on the window's resizable dimensions. Get/set. |
| `MaxSize` | `Vector2?` | Optional upper bound on the window's resizable dimensions. Get/set. |
| `Content` | `GameObject` | Prefab or instance to spawn as the window's content. Get/set. |
| `Owner` | `GameObject` | Optional GameObject whose deactivation or destruction also closes this window. Get/set. |
| `CloseHandle` | `Action` | Optional callback intended to run when the window closes. Get/set. |
