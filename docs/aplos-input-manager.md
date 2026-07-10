# AplosInputManager

`AplosInputManager` wires the console's debug input bindings to Unity's Input System. On
start-up it resolves the active control scheme, selects the matching `DebugInputActionMapper`,
and binds that mapper's input against a `PlayerInput`. When no `PlayerInput` exists in the
scene it spawns a temporary debug-specific one from the configured prefab. It is a
`MonoBehaviour` singleton (namespace `AplosConsole.Input`) that survives scene loads via
`DontDestroyOnLoad`.

## Properties

| Name | Description |
| --- | --- |
| `Instance` | Static singleton reference to the active input manager. Assigned on `Awake`, read-only from outside the class. |
| `PlayerInput` | The `PlayerInput` currently driving the console's debug input bindings. Set when a `PlayerInput` is discovered or created during `StartPlayerInput()`. |
| `ActiveConsoleInputAdapter` | The `IAplosConsoleInputAdapter` resolved from this `GameObject` on `Awake`; bridges console open/close events to the active input action map. An error is logged if none is present. Read-only from outside the class. |
| `_debugInputBindings` | Required dependency. Serialized list of `DebugInputActionMapper`s, one per control scheme. The manager selects the mapper whose `SchemaName` matches the active control scheme and binds its input. |
| `_settings` | Required dependency. Serialized reference to the `AplosCommandConfiguration` asset, used to instantiate the fallback `PlayerInputPrefab` when no `PlayerInput` is found in the scene. |

<details>
<summary>Declarations</summary>

```csharp
public static AplosInputManager Instance { get; private set; }
public PlayerInput PlayerInput { get; set; }
public IAplosConsoleInputAdapter ActiveConsoleInputAdapter { get; private set; }
[SerializeField] private List<DebugInputActionMapper> _debugInputBindings;
[SerializeField] private AplosCommandConfiguration _settings;
```

</details>

## Events

_This class exposes no events._

## Public methods

| Name | Description |
| --- | --- |
| `StartPlayerInput` | Entry point that activates console input. Finds an existing `PlayerInput` in the scene and initialises the console bindings against it; if none exists, spawns a temporary debug-specific `PlayerInput` from the configured prefab and initialises against that. If no `DebugInputActionMapper` matches the active control scheme, a warning is logged and no binding is applied. |

<details>
<summary>Declarations</summary>

```csharp
public void StartPlayerInput();
```

</details>

## Static methods

_This class currently exposes no public static methods. Global access is provided through the static `Instance` property listed under [Properties](#properties)._
