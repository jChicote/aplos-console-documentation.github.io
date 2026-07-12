# AplosDebugCommand

The Aplos command family models a runnable console command. Commands are registered with and invoked
through [AplosConsole](aplos-console.md).

## AplosDebugCommandBase

The base shared by every command variant. It stores the command's identity and usage
text and exposes them read-only; it carries no executable delegate of its own.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ AplosDebugCommandBase
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

***Namespace***: `AplosConsole.Commands`

### Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `CommandId` | `string` | The identifier used to invoke the command from the console. Read-only. |
| `CommandDescription` | `string` | Human-readable description shown in the command list and help output. Read-only. |
| `CommandFormat` | `string` | Usage/format string describing the command's expected arguments. Read-only. |

### Constructors

<h2 id="aplosdebugcommandbase-constructor"><code>AplosDebugCommandBase</code></h2>

**Parameters:**

- `commandId` (`string`) — Identifier used to invoke the command.
- `commandDescription` (`string`) — Description shown in the command list.
- `commandFormat` (`string`) — Usage/format string for the command.

**Example**

```csharp
public class MyCommand : AplosDebugCommandBase
{
    public MyCommand(string id, string description, string format)
        : base(id, description, format) { }
}
```

**Description:** Initialises the shared metadata. Normally called via `base(...)` from a derived `AplosDebugCommand` variant rather than directly.

<br>

## AplosDebugCommand

A parameterless command. Wraps an `Action` that runs when the command is invoked with no
arguments.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ AplosDebugCommandBase
    ↳ AplosDebugCommand
```

</details>
<br>

**Inherited Members:**

- `AplosDebugCommandBase.CommandId`
- `AplosDebugCommandBase.CommandDescription`
- `AplosDebugCommandBase.CommandFormat`

***Namespace***: `AplosConsole.Commands`

### Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `IsBuiltIn` | `bool` | Marks the command as one that ships with the console (as opposed to a user-registered command). Defaults to `false`. Get/set. |

### Constructors

<h2 id="aplosdebugcommand-constructor"><code>AplosDebugCommand</code></h2>

**Parameters:**

- `commandId` (`string`) — Identifier used to invoke the command.
- `commandDescription` (`string`) — Description shown in the command list.
- `commandFormat` (`string`) — Usage/format string for the command.
- `command` (`Action`) — Action to run when the command is invoked.
- `isBuiltIn` (`bool`) — Whether to flag the command as a built-in command. Defaults to `false`.

**Example**

```csharp
var command = new AplosDebugCommand("hello", "Prints a greeting", "hello", () => Debug.Log("Hi!"));
```

**Description:** Builds a parameterless command from the given metadata and action. Pass `isBuiltIn: true` to flag it as a built-in command.

<br>

### Public methods

<h2 id="invoke"><code>Invoke</code></h2>

**Example**

```csharp
command.Invoke();
```

**Description:** Executes the wrapped action. No-op if the action is `null`.

<br>

## AplosDebugCommand&lt;T&gt;

A single-argument command. Wraps an `Action<T>` invoked with one typed argument parsed from the
console input.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ AplosDebugCommandBase
    ↳ AplosDebugCommand<T>
```

</details>
<br>

**Inherited Members:**

- `AplosDebugCommandBase.CommandId`
- `AplosDebugCommandBase.CommandDescription`
- `AplosDebugCommandBase.CommandFormat`

***Namespace***: `AplosConsole.Commands`

### Constructors

<h2 id="aplosdebugcommand-constructor-2"><code>AplosDebugCommand</code></h2>

**Parameters:**

- `commandId` (`string`) — Identifier used to invoke the command.
- `commandDescription` (`string`) — Description shown in the command list.
- `commandFormat` (`string`) — Usage/format string for the command.
- `command` (`Action<T>`) — Action to run when the command is invoked, receiving the parsed argument.

**Example**

```csharp
var command = new AplosDebugCommand<int>("setlevel", "Sets the level", "setlevel <int>", level => Debug.Log(level));
```

**Description:** Builds a command from the given metadata that forwards a single typed argument to `command`.

<br>

### Public methods

<h2 id="invoke-2"><code>Invoke</code></h2>

**Parameters:**

- `value` (`T`) — The argument to forward to the wrapped action.

**Example**

```csharp
command.Invoke(5);
```

**Description:** Executes the wrapped action with the supplied argument. No-op if the action is `null`.

<br>

## AplosDebugCommand&lt;T1, T2&gt;

A two-argument command. Wraps an `Action<T1, T2>` invoked with two typed arguments parsed from
the console input.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ AplosDebugCommandBase
    ↳ AplosDebugCommand<T1, T2>
```

</details>
<br>

**Inherited Members:**

- `AplosDebugCommandBase.CommandId`
- `AplosDebugCommandBase.CommandDescription`
- `AplosDebugCommandBase.CommandFormat`

***Namespace***: `AplosConsole.Commands`

### Constructors

<h2 id="aplosdebugcommand-constructor-3"><code>AplosDebugCommand</code></h2>

**Parameters:**

- `commandId` (`string`) — Identifier used to invoke the command.
- `commandDescription` (`string`) — Description shown in the command list.
- `commandFormat` (`string`) — Usage/format string for the command.
- `command` (`Action<T1, T2>`) — Action to run when the command is invoked, receiving the two parsed arguments.

**Example**

```csharp
var command = new AplosDebugCommand<int, string>("setitem", "Sets an item", "setitem <int> <string>", (id, name) => Debug.Log($"{id}: {name}"));
```

**Description:** Builds a command from the given metadata that forwards two typed arguments to `command`.

<br>

### Public methods

<h2 id="invoke-3"><code>Invoke</code></h2>

**Parameters:**

- `value` (`T1`) — The first argument to forward to the wrapped action.
- `value2` (`T2`) — The second argument to forward to the wrapped action.

**Example**

```csharp
command.Invoke(5, "sword");
```

**Description:** Executes the wrapped action with the two supplied arguments. No-op if the action is `null`.
