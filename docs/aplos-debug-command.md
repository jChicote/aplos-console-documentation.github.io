# AplosDebugCommand

The Aplos command family models a runnable console command: the metadata that describes it
(its id, description, and usage format) paired with a delegate to execute. All variants live in
the `AplosConsole.Commands` namespace and derive from `AplosDebugCommandBase`, which holds the
shared metadata. The concrete `AplosDebugCommand` types differ only in how many typed arguments
they forward to their wrapped delegate. Commands are registered with and invoked through
[AplosConsole](aplos-console.md).

## AplosDebugCommandBase

The metadata base shared by every command variant. It stores the command's identity and usage
text and exposes them read-only; it carries no executable delegate of its own.

### Properties

| Name | Description |
| --- | --- |
| `CommandId` | The identifier used to invoke the command from the console. Read-only. |
| `CommandDescription` | Human-readable description shown in the command list and help output. Read-only. |
| `CommandFormat` | Usage/format string describing the command's expected arguments. Read-only. |

### Constructors

| Signature | Description |
| --- | --- |
| `AplosDebugCommandBase(string commandId, string commandDescription, string commandFormat)` | Initialises the shared metadata. Normally called via `base(...)` from a derived `AplosDebugCommand` variant rather than directly. |

## AplosDebugCommand

A parameterless command. Wraps an `Action` that runs when the command is invoked with no
arguments.

### Properties

| Name | Description |
| --- | --- |
| `IsBuiltIn` | Marks the command as one that ships with the console (as opposed to a user-registered command). Defaults to `false`. Get/set. |
| _Inherited_ | `CommandId`, `CommandDescription`, and `CommandFormat` from `AplosDebugCommandBase`. |

### Constructors

| Signature | Description |
| --- | --- |
| `AplosDebugCommand(string commandId, string commandDescription, string commandFormat, Action command, bool isBuiltIn = false)` | Builds a parameterless command from the given metadata and action. Pass `isBuiltIn: true` to flag it as a built-in command. |

### Public methods

| Name | Description |
| --- | --- |
| `Invoke()` | Executes the wrapped action. No-op if the action is `null`. |

## AplosDebugCommand&lt;T&gt;

A single-argument command. Wraps an `Action<T>` invoked with one typed argument parsed from the
console input.

### Properties

| Name | Description |
| --- | --- |
| _Inherited_ | `CommandId`, `CommandDescription`, and `CommandFormat` from `AplosDebugCommandBase`. Adds no properties of its own. |

### Constructors

| Signature | Description |
| --- | --- |
| `AplosDebugCommand(string commandId, string commandDescription, string commandFormat, Action<T> command)` | Builds a command from the given metadata that forwards a single typed argument to `command`. |

### Public methods

| Name | Description |
| --- | --- |
| `Invoke(T value)` | Executes the wrapped action with the supplied argument. No-op if the action is `null`. |

## AplosDebugCommand&lt;T1, T2&gt;

A two-argument command. Wraps an `Action<T1, T2>` invoked with two typed arguments parsed from
the console input.

### Properties

| Name | Description |
| --- | --- |
| _Inherited_ | `CommandId`, `CommandDescription`, and `CommandFormat` from `AplosDebugCommandBase`. Adds no properties of its own. |

### Constructors

| Signature | Description |
| --- | --- |
| `AplosDebugCommand(string commandId, string commandDescription, string commandFormat, Action<T1, T2> command)` | Builds a command from the given metadata that forwards two typed arguments to `command`. |

### Public methods

| Name | Description |
| --- | --- |
| `Invoke(T1 value, T2 value2)` | Executes the wrapped action with the two supplied arguments. No-op if the action is `null`. |
