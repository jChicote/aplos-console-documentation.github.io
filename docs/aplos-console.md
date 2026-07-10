# AplosConsole

`AplosConsole` is a singleton console that manages command registration and drives the
console's open, close, and input actions. It is a sealed `MonoBehaviour` singleton (namespace
`AplosConsole`) that implements `IConsoleCommandSystem` and `IConsoleInputProvider`.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ Component
       ↳ Behaviour
          ↳ MonoBehaviour
             ↳ AplosConsole
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

***Namespace***: `AplosConsole` <br>
***Implements***: [`IConsoleCommandSystem`](command-system-interfaces.md#iconsolecommandsystem), [`IConsoleInputProvider`](console-interfaces.md#iconsoleinputprovider)

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `Instance` | `AplosConsole` | Static singleton reference to the active console. Assigned on `Awake`, read-only from outside the class. |
| `CommandList` | `List<object>` | The list of registered command objects currently presented in the command display list. |
| `IsOpen` | `bool` | Whether the console is currently open (active). |
| `CommandConfiguration` | `AplosCommandConfiguration` | Required dependency. Serialized reference to the `AplosCommandConfiguration` asset that supplies the default command set. |
| `AplosWindow` | `GameObject` | Required dependency. Serialized reference to the console window `GameObject`; its active state determines the initial open/closed state. |
| `AddOnCommands` | `List<AplosConsoleCommandConstructor>` | List of additional `AplosConsoleCommandConstructor`s registered during initialisation. |

## Events

| Name | Data Type | Description |
| --- | --- | --- |
| `OnAutoComplete` | `UnityEvent` | Raised when auto-complete is requested (via `AutoCompletePressed`). |
| `OnInitialise` | `UnityEvent` | Raised once after commands are first initialised. |
| `OnRefresh` | `UnityEvent` | Raised after the command list is refreshed (via `RefreshCommands`). |
| `OnOpenConsole` | `UnityEvent` | Raised when the console opens. |
| `OnCloseConsole` | `UnityEvent` | Raised when the console closes. |
| `OnNavigate` | `UnityEvent<int>` | Raised when navigation is requested; passes the navigation direction as an `int`. |
| `OnShowAll` | `UnityEvent` | Raised when all commands should be shown (e.g. the built-in `help` command). |
| `OnSubmit` | `UnityEvent` | Raised when the current input is submitted (via `SubmitPressed`). |
| `OnCommandsChanged` | `UnityEvent` | Raised whenever the set of registered commands changes (runtime register/unregister). |

## Public methods

## `OpenConsole`

**Example**

```csharp
AplosConsole.Instance.OpenConsole();
```

**Description:** Opens the console and raises `OnOpenConsole`.

<br>

## `CloseConsole`

**Example**

```csharp
AplosConsole.Instance.CloseConsole();
```

**Description:** Closes the console and raises `OnCloseConsole`.

<br>

## `RegisterCommand`

**Parameters:**

- `command` — The command to add to the system.

**Example**

```csharp
var command = new AplosDebugCommand("hello", "Prints a greeting", "hello", () => Debug.Log("Hi!"));
AplosConsole.Instance.RegisterCommand(command);
```

**Description:** Registers a command so that it is collected and presented in the console's command display list.

<br>

## `RegisterCommand`

**Parameters:**

- `id` — Identifier used to invoke the command.
- `description` — Description shown in the command list.
- `format` — Usage/format string for the command.
- `command` — Action to run when the command is invoked.

**Example**

```csharp
AplosDebugCommand command = AplosConsole.Instance.RegisterCommand(
    "hello", "Prints a greeting", "hello", () => Debug.Log("Hi!"));
```

**Description:** Builds and registers a parameterless command in one call and returns it so the caller can keep a handle (e.g. to unregister it later).

<br>

## `UnregisterCommand`

**Parameters:**

- `id` — The `CommandId` of the command to remove.

**Example**

```csharp
AplosConsole.Instance.UnregisterCommand("hello");
```

**Description:** Removes any previously registered command matching the supplied identifier from the command display list.

<br>

## `RefreshCommands`

**Example**

```csharp
AplosConsole.Instance.RefreshCommands();
```

**Description:** Rebuilds the command list back to the default commands and raises `OnRefresh`.

<br>

## `AutoCompletePressed`

**Example**

```csharp
AplosConsole.Instance.AutoCompletePressed();
```

**Description:** Signals that the auto-complete action was triggered for the current input.

<br>

## `SubmitPressed`

**Example**

```csharp
AplosConsole.Instance.SubmitPressed();
```

**Description:** Signals that the submit action was triggered, confirming the current input.

<br>

## `NavigatePressed`

**Parameters:**

- `direction` — The direction to move, where a positive value navigates up and a negative value navigates down.

**Example**

```csharp
AplosConsole.Instance.NavigatePressed(1);
```

**Description:** Signals a navigation action through the console's command list.

<br>

## `ToggleDebug`

**Example**

```csharp
AplosConsole.Instance.ToggleDebug();
```

**Description:** Signals a request to toggle the console's visibility open or closed.

<br>
