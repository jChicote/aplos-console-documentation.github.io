# Interfaces

The command system is expressed through two contracts, `IConsoleCommandSystem` is the surface consumers use to add and remove commands,
and `IConsoleCommandRegistrator` is implemented by types that contribute their own commands to
that system. Neither interface extends another. Depending on these interfaces rather than the
concrete [AplosConsole](aplos-console.md) keeps command registration decoupled from the console
implementation.

## IConsoleCommandSystem

The contract for a console command system: the surface through which commands are registered
and unregistered. Implemented by [AplosConsole](aplos-console.md).

***Namespace***: `AplosConsole.Infrastrcutre`

### Public methods

<h2 id="registercommand"><code>RegisterCommand</code></h2>

**Parameters:**

- `command` ([`AplosDebugCommandBase`](aplos-debug-command.md#aplosdebugcommandbase)) — The command to add to the system.

**Example**

```csharp
consoleCommandSystem.RegisterCommand(command);
```

**Description:** Registers a command so that it is collected and presented in the console's command display list. See [AplosDebugCommand](aplos-debug-command.md) for the command types.

<br>

<h2 id="unregistercommand"><code>UnregisterCommand</code></h2>

**Parameters:**

- `id` (`string`) — The `CommandId` of the command to remove.

**Example**

```csharp
consoleCommandSystem.UnregisterCommand("hello");
```

**Description:** Removes any previously registered command matching the supplied identifier from the command display list.

<br>

## IConsoleCommandRegistrator

Contract for a type that supplies its own set of console commands and registers them with a
given `IConsoleCommandSystem` when invoked. Implement this on any object that wants to
contribute commands to the console.

***Namespace***: `AplosConsole.Infrastrcutre`

### Public methods

<h2 id="registercommand-2"><code>RegisterCommand</code></h2>

**Parameters:**

- `consoleCommandSystem` ([`IConsoleCommandSystem`](command-system-interfaces.md#iconsolecommandsystem)) — Command system responsible for handling these commands.

**Example**

```csharp
public void RegisterCommand(IConsoleCommandSystem consoleCommandSystem)
{
    consoleCommandSystem.RegisterCommand(myCommand);
}
```

**Description:** Registers commands from the implemented object through the command system.

<br>
