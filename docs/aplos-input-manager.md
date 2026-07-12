# AplosInputManager

`AplosInputManager` wires the console's debug input bindings to Unity's Input System. On
start-up it resolves the active control scheme, selects the matching `DebugInputActionMapper`,
and binds that mapper's input against a `PlayerInput`. When no `PlayerInput` exists in the
scene it spawns a temporary debug-specific one from the configured prefab.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ AplosInputManager
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

***Namespace***: `AplosConsole.Input`

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `Instance` | `AplosInputManager` | Static singleton reference to the active input manager. Assigned on `Awake`, read-only from outside the class. |
| `PlayerInput` | `PlayerInput` | The `PlayerInput` currently driving the console's debug input bindings. Set when a `PlayerInput` is discovered or created during `StartPlayerInput()`. Get/set. |
| `ActiveConsoleInputAdapter` | [`IAplosConsoleInputAdapter`](input-interfaces.md#iaplosconsoleinputadapter) | The adapter resolved from this `GameObject` on `Awake`; bridges console open/close events to the active input action map. An error is logged if none is present. Read-only from outside the class. |
| `_debugInputBindings` | `List<DebugInputActionMapper>` | Required dependency. Serialized list of `DebugInputActionMapper`s, one per control scheme. The manager selects the mapper whose `SchemaName` matches the active control scheme and binds its input. |
| `_settings` | `AplosCommandConfiguration` | Required dependency. Serialized reference to the `AplosCommandConfiguration` asset, used to instantiate the fallback `PlayerInputPrefab` when no `PlayerInput` is found in the scene. |

## Public methods

<h2 id="startplayerinput"><code>StartPlayerInput</code></h2>

**Example**

```csharp
AplosInputManager.Instance.StartPlayerInput();
```

**Description:** Entry point that activates console input. Finds an existing `PlayerInput` in the scene and initialises the console bindings against it; if none exists, spawns a temporary debug-specific `PlayerInput` from the configured prefab and initialises against that. If no `DebugInputActionMapper` matches the active control scheme, a warning is logged and no binding is applied.

<br>
