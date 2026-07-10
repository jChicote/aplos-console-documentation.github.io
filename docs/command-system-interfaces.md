# Interfaces

The command system is expressed through two contracts in the `AplosConsole.Infrastrcutre`
namespace. `IConsoleCommandSystem` is the surface consumers use to add and remove commands,
and `IConsoleCommandRegistrator` is implemented by types that contribute their own commands to
that system. Depending on these interfaces rather than the concrete
[AplosConsole](aplos-console.md) keeps command registration decoupled from the console
implementation.

## IConsoleCommandSystem

The contract for a console command system: the surface through which commands are registered
and unregistered. Implemented by [AplosConsole](aplos-console.md).

### Methods

| Name | Description |
| --- | --- |
| `RegisterCommand` | Registers a command so that it is collected and presented in the console's command display list. See [AplosDebugCommand](aplos-debug-command.md) for the command types. |
| `UnregisterCommand` | Removes any previously registered command matching the supplied identifier (its `CommandId`) from the command display list. |

<details>
<summary>Declarations</summary>

```csharp
void RegisterCommand(AplosDebugCommandBase command);
void UnregisterCommand(string id);
```

</details>

## IConsoleCommandRegistrator

Contract for a type that supplies its own set of console commands and registers them with a
given `IConsoleCommandSystem` when invoked. Implement this on any object that wants to
contribute commands to the console.

### Methods

| Name | Description |
| --- | --- |
| `RegisterCommand` | Registers the implementer's commands through the supplied command system. |

<details>
<summary>Declarations</summary>

```csharp
void RegisterCommand(IConsoleCommandSystem consoleCommandSystem);
```

</details>
