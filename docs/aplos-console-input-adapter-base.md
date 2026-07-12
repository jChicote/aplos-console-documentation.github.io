# AplosConsoleInputAdapterBase

`AplosConsoleInputAdapterBase` is an abstract `MonoBehaviour` base for implementing a custom
input adapter. It implements [`IAplosConsoleInputAdapter`](input-interfaces.md#iaplosconsoleinputadapter),
wiring `Initialise` up automatically and hooking `HandleConsoleOpen`/`HandleConsoleClose` into
[`AplosConsole`](aplos-console.md)'s open/close events on `Start`, then calling `Dispose` and
unsubscribing on `OnDestroy`. Derive from it and implement the abstract members to bind your own
input system to the console; the console's built-in `UnityInputSystemAdapter` is implemented the
same way.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ AplosConsoleInputAdapterBase
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

***Namespace***: `AplosConsole.Input` <br>
***Implements***: [`IAplosConsoleInputAdapter`](input-interfaces.md#iaplosconsoleinputadapter)

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `InputProvider` | `IConsoleInputProvider` | The input provider passed to `Initialise`, set automatically on `Start`. Protected; get-only from derived classes. |
| `PlayerInput` | `PlayerInput` | The Unity Input System `PlayerInput` this adapter drives. Protected; get/set from derived classes. |

## Protected methods

<h2 id="start"><code>Start</code></h2>

**Example**

```csharp
protected override void Start()
{
    SetupPlayerInput();
    base.Start();
}
```

**Description:** Calls `Initialise(AplosConsole.Instance)` and subscribes `HandleConsoleOpen`/`HandleConsoleClose` to `AplosConsole.OnOpenConsole`/`OnCloseConsole`. Override to set up adapter-specific state first, then call `base.Start()` to preserve this wiring.

<br>

<h2 id="ondestroy"><code>OnDestroy</code></h2>

**Example**

```csharp
protected override void OnDestroy()
{
    base.OnDestroy();
}
```

**Description:** Calls `Dispose()` and unsubscribes `HandleConsoleOpen`/`HandleConsoleClose` from `AplosConsole`'s open/close events. Override only for extra teardown, and call `base.OnDestroy()` to preserve this unsubscription.

<br>

## Public methods

<h2 id="initialise"><code>Initialise</code></h2>

**Parameters:**

- `inputProvider` ([`IConsoleInputProvider`](console-interfaces.md#iconsoleinputprovider)) — Console input provider the adapter wires itself up to.

**Example**

```csharp
adapter.Initialise(AplosConsole.Instance);
```

**Description:** Stores `inputProvider` in `InputProvider`. Called automatically from `Start`; implements [`IAplosConsoleInputAdapter.Initialise`](input-interfaces.md#initialise).

<br>

<h2 id="handleconsoleopen"><code>HandleConsoleOpen</code></h2>

**Example**

```csharp
public override void HandleConsoleOpen()
{
    if (PlayerInput == null) return;
    PlayerInput.SwitchCurrentActionMap("UI");
}
```

**Description:** Abstract. Override to react to the console opening, typically by switching or disabling gameplay input action maps.

<br>

<h2 id="handleconsoleclose"><code>HandleConsoleClose</code></h2>

**Example**

```csharp
public override void HandleConsoleClose()
{
    if (PlayerInput == null) return;
    PlayerInput.SwitchCurrentActionMap(_previousActionMap);
}
```

**Description:** Abstract. Override to react to the console closing, typically by restoring the gameplay input action map.

<br>

<h2 id="dispose"><code>Dispose</code></h2>

**Example**

```csharp
public override void Dispose()
    => _currentInputBinding?.UnbindInput();
```

**Description:** Abstract. Override to release any resources or bindings the adapter holds. Called automatically from `OnDestroy`.

<br>
