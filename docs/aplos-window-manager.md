# AplosWindowManager

`AplosWindowManager` opens, tracks, and tears down the runtime windows spawned by the console.
It creates windows through an `AplosWindowFactory`, keeps a list of the ones currently open,
applies the saved settings palette and configuration to each freshly spawned window, and can
close them all at once. It is a `MonoBehaviour` singleton (namespace `AplosConsole.Windows`).

## Properties

| Name | Description |
| --- | --- |
| `Instance` | Static singleton reference to the active window manager. Assigned on `Awake`, read-only from outside the class. |
| `OpenWindows` | Read-only list of the `AplosWindowHandler`s currently open and tracked by the manager. |
| `_windowFactory` | Required dependency. Serialized reference to the `AplosWindowFactory` used to instantiate and initialise new window instances. |
| `_windowParent` | Optional. Serialized `Transform` that spawned windows are parented under. Falls back to this manager's own transform when unset. |

<details>
<summary>Declarations</summary>

```csharp
public static AplosWindowManager Instance { get; private set; }
public IReadOnlyList<AplosWindowHandler> OpenWindows { get; }
[SerializeField] private AplosWindowFactory _windowFactory;
[SerializeField] private Transform _windowParent;
```

</details>

## Events

_This class exposes no events._

## Public methods

| Name | Description |
| --- | --- |
| `OpenWindow` | Creates a window through the factory from the given request and starts tracking it. Applies the saved settings (bar palette and any `DebugGroup` content) via `AplosSettingsManager` so the new window matches the persisted configuration, then re-asserts its per-window resize constraints last so the shared window sizing settings don't clobber them. Returns the created `AplosWindowHandler`, or `null` if creation failed. |
| `CloseAll` | Destroys every tracked open window and clears the tracking list. |

<details>
<summary>Declarations</summary>

```csharp
public AplosWindowHandler OpenWindow(AplosWindowRequest request);
public void CloseAll();
```

</details>

## Static methods

_This class currently exposes no public static methods. Global access is provided through the static `Instance` property listed under [Properties](#properties)._
