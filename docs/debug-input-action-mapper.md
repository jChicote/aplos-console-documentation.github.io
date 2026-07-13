# DebugInputActionMapper

`DebugInputActionMapper` is an abstract `MonoBehaviour` base for components that bind and unbind
a control scheme's input actions to the console. Derive from it to map a specific device/control
scheme (e.g. the built-in `DebugKeyboardAndMouseInputBinding`) to the console's input handlers.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ DebugInputActionMapper
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
| `SchemaName` | `string` | The name of the control scheme this mapper is responsible for. |
| `InputManager` | [`AplosInputManager`](aplos-input-manager.md) | The input manager that owns and coordinates this mapper. |
| `PlayerInput` | `PlayerInput` | The `PlayerInput` this mapper reads actions from; injected or derived from the GameObject at `Start`. |

## Public methods

<h2 id="bindinput"><code>BindInput</code></h2>

**Example**

```csharp
public override void BindInput()
{
    Subscribe(DebugInputActionName.Submit, OnSubmit);
}
```

**Description:** Abstract. Override to subscribe this mapper's input actions to their console handlers.

<br>

<h2 id="unbindinput"><code>UnbindInput</code></h2>

**Example**

```csharp
public override void UnbindInput()
{
    Unsubscribe(DebugInputActionName.Submit, OnSubmit);
}
```

**Description:** Abstract. Override to remove the subscriptions established by `BindInput`.

<br>
