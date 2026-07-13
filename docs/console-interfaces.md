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

## IConsolePinStateStore

_Internal contract._ Persists and restores the set of pinned console commands by key, abstracting
the backing store (file, prefs, ...) from the console view that captures and applies pin state.

***Namespace***: `AplosConsole.Console.Persistence`

### Public methods

<h2 id="tryload"><code>TryLoad</code></h2>

**Parameters:**

- `key` (`string`) — Identifier the state was previously saved under.
- `state` (`out ConsolePinState`) — The stored state, if a valid save exists for the key.

**Example**

```csharp
if (pinStateStore.TryLoad("myConsole", out ConsolePinState state))
{
    // apply state
}
```

**Description:** Returns `true` and outputs the stored state when a valid save exists for the key; otherwise returns `false` and leaves callers on their defaults.

<br>

<h2 id="save"><code>Save</code></h2>

**Parameters:**

- `key` (`string`) — Identifier to save the state under.
- `state` (`ConsolePinState`) — The pin state to persist.

**Example**

```csharp
pinStateStore.Save("myConsole", state);
```

**Description:** Persists the given state under the specified key.

<br>

<h2 id="clear"><code>Clear</code></h2>

**Parameters:**

- `key` (`string`) — Identifier of the saved state to discard.

**Example**

```csharp
pinStateStore.Clear("myConsole");
```

**Description:** Discards any saved state for the key so the next load falls back to no pins (used by a console / settings reset).

<br>
