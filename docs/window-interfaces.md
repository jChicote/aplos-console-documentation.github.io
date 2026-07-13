# Interfaces

## IWindowResizeHandler

The contract for a window resize handler: reports the window's current and last-resized size,
and lets a caller resize, collapse, or restore it. Implemented by the built-in window resizing
component attached to each spawned window.

***Namespace***: `AplosConsole.Window.Components`

### Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `CanResize` | `bool` | Whether the window currently accepts resize operations. Get/set. |
| `LastResizeWindowSize` | `Vector2` | The window's size as of the last resize, used to restore it after a collapse. Read-only. |
| `CurrentWindowSize` | `Vector2` | The window's current size. Read-only. |

### Public methods

<h2 id="setwindowsize"><code>SetWindowSize</code></h2>

**Parameters:**

- `size` (`Vector2`) — Requested window size, clamped to the current min/max bounds.

**Example**

```csharp
resizeHandler.SetWindowSize(new Vector2(480f, 320f));
```

**Description:** Resizes the window to the given size, clamped between its current minimum and maximum bounds.

<br>

<h2 id="setsizeconstraints"><code>SetSizeConstraints</code></h2>

**Parameters:**

- `minSize` (`Vector2`) — Lower bound on the window's resizable dimensions.
- `maxSize` (`Vector2`) — Upper bound on the window's resizable dimensions.

**Example**

```csharp
resizeHandler.SetSizeConstraints(new Vector2(200f, 200f), new Vector2(800f, 600f));
```

**Description:** Overrides the window's min/max resize bounds and re-clamps its current size to fit within them.

<br>

<h2 id="collapsewindowsize"><code>CollapseWindowSize</code></h2>

**Example**

```csharp
resizeHandler.CollapseWindowSize();
```

**Description:** Remembers the window's current expanded size, then shrinks it down to the collapsed bar height.

<br>

<h2 id="restorewindowsize"><code>RestoreWindowSize</code></h2>

**Example**

```csharp
resizeHandler.RestoreWindowSize();
```

**Description:** Restores the window to the size it was at before it was last collapsed.

<br>

## IWindowStateStore

_Internal contract._ Persists and restores a single window's `WindowState` by key, abstracting
the backing store (file, prefs, ...) from the components that capture and apply window layout.

***Namespace***: `AplosConsole.Windows.Persistence`

### Public methods

<h2 id="tryload"><code>TryLoad</code></h2>

**Parameters:**

- `key` (`string`) — Identifier the state was previously saved under.
- `state` (`out WindowState`) — The stored state, if a valid save exists for the key.

**Example**

```csharp
if (windowStateStore.TryLoad("myWindow", out WindowState state))
{
    // apply state
}
```

**Description:** Returns `true` and outputs the stored state when a valid save exists for the key; otherwise returns `false` and leaves callers on their defaults.

<br>

<h2 id="save"><code>Save</code></h2>

**Parameters:**

- `key` (`string`) — Identifier to save the state under.
- `state` (`WindowState`) — The window state to persist.

**Example**

```csharp
windowStateStore.Save("myWindow", state);
```

**Description:** Persists the given state under the specified key.

<br>

<h2 id="clear"><code>Clear</code></h2>

**Parameters:**

- `key` (`string`) — Identifier of the saved state to discard.

**Example**

```csharp
windowStateStore.Clear("myWindow");
```

**Description:** Discards any saved state for the key so the next load falls back to the window's authored defaults (used by the console reset).

<br>
