# DebugGroupAttribute

`DebugGroupAttribute` marks a class for discovery by the debug settings scanner, grouping its
[`DebugSettingAttribute`](debug-setting-attribute.md) fields under one named group. It is a
sealed `Attribute` (namespace `AplosConsole.Settings.Attributes`) restricted via
`[AttributeUsage(AttributeTargets.Class, AllowMultiple = false, Inherited = false)]` to single,
non-inherited use on classes, and implements no interfaces of its own.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Attribute
    ↳ DebugGroupAttribute
```

</details>
<br>

**Inherited Members:**

- `Attribute.Equals(object)`
- `Attribute.GetHashCode()`
- `Attribute.IsDefaultAttribute()`
- `Attribute.Match(object)`
- `Attribute.TypeId`
- `object.GetType()`
- `object.ToString()`
- …

***Namespace***: `AplosConsole.Settings.Attributes`

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `GroupName` | `string` | The display name of this settings group in the JSON output. Read-only. |
| `Description` | `string` | Optional description shown in generated documentation. Get/set. |
| `Order` | `int` | Order of the group in the final JSON (lower = earlier). Get/set. |

## Constructors

<h2 id="debuggroupattribute-constructor"><code>DebugGroupAttribute</code></h2>

**Parameters:**

- `groupName` (`string`) — The display name of this settings group in the JSON output.

**Example**

```csharp
[DebugGroup("Graphics")]
public class GraphicsSettings
{
    [DebugSetting(Label = "Vsync")]
    public bool vsync;
}
```

**Description:** Creates the attribute with the group's display name. Throws `ArgumentException` if `groupName` is null, empty, or whitespace.
