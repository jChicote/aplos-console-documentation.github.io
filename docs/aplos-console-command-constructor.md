# AplosConsoleCommandConstructor

`AplosConsoleCommandConstructor` is a `MonoBehaviour` wrapper for a debug command: an abstract
base you derive from to configure the command's action before it is packaged and registered
with the console. Concrete subclasses override `RegisterCommand` to build and register their command(s) with
the supplied [`IConsoleCommandSystem`](command-system-interfaces.md#iconsolecommandsystem).

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ AplosConsoleCommandConstructor
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

***Namespace***: `AplosConsole.Console`

## Public methods

<h2 id="registercommand"><code>RegisterCommand</code></h2>

**Parameters:**

- `commandSystem` ([`IConsoleCommandSystem`](command-system-interfaces.md#iconsolecommandsystem)) — The command system to register the built command(s) with.

**Example**

```csharp
public class MyCommandConstructor : AplosConsoleCommandConstructor
{
    public override void RegisterCommand(IConsoleCommandSystem commandSystem)
    {
        commandSystem.RegisterCommand(
            new AplosDebugCommand("hello", "Prints a greeting", "hello", () => Debug.Log("Hi!")));
    }
}
```

**Description:** Builds this constructor's command(s) and registers each with `commandSystem`. Abstract — override this in a derived `MonoBehaviour` to contribute one or more commands to the console.
