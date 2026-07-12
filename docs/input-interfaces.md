# Interfaces

## IAplosConsoleInputActionMapHandler

Contract for a type that reacts to the console opening and closing, typically by enabling or
disabling an input action map.

***Namespace***: `AplosConsole.Input`

### Public methods

<h2 id="handleconsoleopen"><code>HandleConsoleOpen</code></h2>

**Example**

```csharp
public void HandleConsoleOpen()
{
    _playerActions.Disable();
}
```

**Description:** Invoked when the console opens. Implementers typically use this to disable a gameplay input action map.

<br>

<h2 id="handleconsoleclose"><code>HandleConsoleClose</code></h2>

**Example**

```csharp
public void HandleConsoleClose()
{
    _playerActions.Enable();
}
```

**Description:** Invoked when the console closes. Implementers typically use this to re-enable a gameplay input action map.

<br>

## IAplosConsoleInputAdapter

Contract for an input adapter that binds to the console's input handling. Extends
[`IAplosConsoleInputActionMapHandler`](#iaplosconsoleinputactionmaphandler) with lifecycle methods
for wiring up and tearing down against an `IConsoleInputProvider`.

***Namespace***: `AplosConsole.Input` <br>
***Extends***: [`IAplosConsoleInputActionMapHandler`](#iaplosconsoleinputactionmaphandler)

### Public methods

<h2 id="initialise"><code>Initialise</code></h2>

**Parameters:**

- `inputProvider` ([`IConsoleInputProvider`](console-interfaces.md#iconsoleinputprovider)) — Console input provider the adapter wires itself up to.

**Example**

```csharp
adapter.Initialise(AplosConsole.Instance);
```

**Description:** Wires the adapter up to the given console input provider, ready to forward input to it.

<br>

<h2 id="dispose"><code>Dispose</code></h2>

**Example**

```csharp
adapter.Dispose();
```

**Description:** Tears down the adapter, releasing any resources or bindings it holds.

<br>
