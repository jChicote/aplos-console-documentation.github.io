# Interfaces

The input system is expressed through two contracts in the `AplosConsole.Input` namespace.
`IAplosConsoleInputActionMapHandler` is the surface for reacting to the console's open/close
state, and `IAplosConsoleInputAdapter` extends it to describe a full input adapter that can be
initialised with and disposed from a console input provider.

## IAplosConsoleInputActionMapHandler

Contract for a type that reacts to the console opening and closing, typically by enabling or
disabling an input action map.

### Methods

| Name | Description |
| --- | --- |
| `HandleConsoleOpen` | Invoked when the console opens. |
| `HandleConsoleClose` | Invoked when the console closes. |

<details>
<summary>Declarations</summary>

```csharp
void HandleConsoleOpen();
void HandleConsoleClose();
```

</details>

## IAplosConsoleInputAdapter

Contract for an input adapter that binds to the console's input handling. Extends
[IAplosConsoleInputActionMapHandler](#iaplosconsoleinputactionmaphandler) with lifecycle methods
for wiring up and tearing down against an `IConsoleInputProvider`.

### Methods

| Name | Description |
| --- | --- |
| `Initialise` | Wires the adapter up to the given console input provider. |
| `Dispose` | Tears down the adapter, releasing any resources or bindings it holds. |

<details>
<summary>Declarations</summary>

```csharp
void Initialise(IConsoleInputProvider inputProvider);
void Dispose();
```

</details>
