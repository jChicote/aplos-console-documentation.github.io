# DebugSettingAttribute

`DebugSettingAttribute` marks a field for discovery by the debug settings scanner, exposing it
as a configurable setting. It is a sealed `Attribute` (namespace `AplosConsole.Settings.Attributes`)
restricted via `[AttributeUsage(AttributeTargets.Field, AllowMultiple = false, Inherited = false)]`
to single, non-inherited use on fields, and implements no interfaces of its own.

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Attribute
    ↳ DebugSettingAttribute
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
| `Label` | `string` | Human-readable label. Falls back to the field name if not set. Get/set. |
| `Description` | `string` | Tooltip / description for tooling or generated docs. Get/set. |
| `Min` | `float` | Minimum value hint for int/float fields (tooling use only). Get/set. |
| `Max` | `float` | Maximum value hint for int/float fields (tooling use only). Get/set. |
| `ReadOnly` | `bool` | When true the field is serialized but flagged as non-editable in tooling. Get/set. |
| `Ignore` | `bool` | Exclude this field entirely from serialization. Get/set. |
