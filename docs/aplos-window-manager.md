# AplosWindowManager

`AplosWindowManager` opens, tracks, and tears down the runtime windows spawned by the console.
It creates windows through an `AplosWindowFactory`, keeps a list of the ones currently open,
applies the saved settings palette and configuration to each freshly spawned window, and can
close them all at once. It is a `MonoBehaviour` singleton (namespace `AplosConsole.Windows`)
that implements no interfaces of its own.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ AplosWindowManager
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

***Namespace***: `AplosConsole.Windows`

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `Instance` | `AplosWindowManager` | Static singleton reference to the active window manager. Assigned on `Awake`, read-only from outside the class. |
| `OpenWindows` | `IReadOnlyList<AplosWindowHandler>` | Read-only list of the `AplosWindowHandler`s currently open and tracked by the manager. |
| `_windowFactory` | `AplosWindowFactory` | Required dependency. Serialized reference to the `AplosWindowFactory` used to instantiate and initialise new window instances. |
| `_windowParent` | `Transform` | Optional. Serialized `Transform` that spawned windows are parented under. Falls back to this manager's own transform when unset. |

## Public methods

<h2 id="openwindow"><code>OpenWindow</code></h2>

**Parameters:**

- `request` (`AplosWindowRequest`) — Describes the window's content and configuration.

**Example**

```csharp
var handler = AplosWindowManager.Instance.OpenWindow(request);
```

**Description:** Spawns a window from the given request, applies the current settings palette to it, and adds it to `OpenWindows`. Returns the spawned window's handler, or `null` if creation failed.

<br>

<h2 id="closeall"><code>CloseAll</code></h2>

**Example**

```csharp
AplosWindowManager.Instance.CloseAll();
```

**Description:** Destroys every currently open window and clears `OpenWindows`.

<br>
