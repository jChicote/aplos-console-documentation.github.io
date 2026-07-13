# DebugSettingsScanner

`DebugSettingsScanner` discovers `[DebugGroup]` components and their `[DebugSetting]`-tagged
fields via reflection, returning them as `ScannedGroup` results sorted by group `Order` then
name.

***Namespace***: `AplosConsole.Settings.Scanner`

## Public methods

<h2 id="scanscene"><code>ScanScene</code></h2>

**Parameters:**

- `includeInactive` (`bool`) — When true, inactive GameObjects are also scanned. Defaults to `false`.

**Example**

```csharp
var groups = DebugSettingsScanner.ScanScene();
```

**Description:** Scans every MonoBehaviour in the active scene(s) for `[DebugGroup]` components.

<br>

<h2 id="scanobjects"><code>ScanObjects</code></h2>

**Parameters:**

- `roots` (`IEnumerable<GameObject>`) — The GameObjects to scan.
- `includeChildren` (`bool`) — Whether to also scan each root's children. Defaults to `true`.
- `includeInactive` (`bool`) — When true, inactive GameObjects are also scanned. Defaults to `false`.

**Example**

```csharp
var groups = DebugSettingsScanner.ScanObjects(new[] { myGameObject });
```

**Description:** Scans only the MonoBehaviours on the supplied GameObjects (and optionally their children).

<br>

<h2 id="scanobject"><code>ScanObject</code></h2>

**Parameters:**

- `root` (`GameObject`) — The GameObject to scan.
- `includeChildren` (`bool`) — Whether to also scan the root's children. Defaults to `true`.
- `includeInactive` (`bool`) — When true, inactive GameObjects are also scanned. Defaults to `false`.

**Example**

```csharp
var groups = DebugSettingsScanner.ScanObject(myGameObject);
```

**Description:** Scans a single GameObject and its children.

<br>

<h2 id="filterbygroup"><code>FilterByGroup</code></h2>

**Parameters:**

- `scan` (`IReadOnlyList<ScannedGroup>`) — A previous scan result to filter.
- `groupName` (`string`) — The group name to match.

**Example**

```csharp
var windowGroups = DebugSettingsScanner.FilterByGroup(groups, "Window Bar");
```

**Description:** Filters a previous scan result to groups whose name matches `groupName`.

<br>
