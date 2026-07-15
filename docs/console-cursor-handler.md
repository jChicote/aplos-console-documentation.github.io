# ConsoleCursorHandler

`ConsoleCursorHandler` is an optional, game-agnostic cursor handler for the console. When present,
it caches the game's cursor lock state and visibility as the console opens, frees the cursor for
interaction, then restores the previous state when the console closes — so the console never
dictates the game's resting cursor policy. Attach it to a GameObject in the scene to enable it;
omit it to leave the cursor entirely under game control.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ ConsoleCursorHandler
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

## Behaviour

On `Start` the handler subscribes to [`AplosConsole`](aplos-console.md)'s `OnOpenConsole` and
`OnCloseConsole` events, and unsubscribes from them on `OnDestroy`.

When the console opens, it caches the current `Cursor.lockState` and `Cursor.visible`, then sets
`Cursor.lockState` to `CursorLockMode.None` and `Cursor.visible` to `true` so the cursor is free
to interact with the console. When the console closes, it writes the cached lock state and
visibility back, leaving the cursor exactly as the game had it before the console was opened.

Because it only reacts to these events, the handler is entirely opt-in: attach it to enable the
save/restore behaviour, or leave it off to keep the cursor under full game control.
