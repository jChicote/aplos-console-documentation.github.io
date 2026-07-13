# Interfaces

## IConsoleInputProvider

Contract for forwarding console input actions from an input source to the console. Implemented by
[AplosConsole](aplos-console.md).

***Namespace***: `AplosConsole.Console`

### Public methods

<h2 id="autocompletepressed"><code>AutoCompletePressed</code></h2>

**Example**

```csharp
inputProvider.AutoCompletePressed();
```

**Description:** Signals that the auto-complete action was triggered for the current input.

<br>

<h2 id="submitpressed"><code>SubmitPressed</code></h2>

**Example**

```csharp
inputProvider.SubmitPressed();
```

**Description:** Signals that the submit action was triggered.

<br>

<h2 id="navigatepressed"><code>NavigatePressed</code></h2>

**Parameters:**

- `direction` (`int`) — The direction to move, where a positive value navigates up and a negative value navigates down.

**Example**

```csharp
inputProvider.NavigatePressed(1);
```

**Description:** Signals a navigation action through the console's command list.

<br>

<h2 id="toggledebug"><code>ToggleDebug</code></h2>

**Example**

```csharp
inputProvider.ToggleDebug();
```

**Description:** Signals a request to toggle the console's visibility open or closed.

<br>
