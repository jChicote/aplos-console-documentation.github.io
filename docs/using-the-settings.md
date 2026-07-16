# Using the Settings / Options

How to expose a field so the settings system can track, persist, and restore it at runtime.

## Configuring a field for tracking

Aplos Console discovers settings by reflection: it scans the scene for components marked as a group, then collects the fields inside them that are marked as settings. Getting a field tracked is a matter of two attributes.

### Grouping the component

Put `[DebugGroup]` on the `MonoBehaviour` whose fields you want to expose. The group name becomes the heading its settings are filed under, both on the settings screen and in the saved JSON.

```csharp
[DebugGroup("Console UI", Description = "Console list item colors", Order = 20)]
public class AplosConsoleView : MonoBehaviour
{
    // ...
}
```

- **`GroupName`** (constructor argument) — the display name for the group. It cannot be null or empty.
- **`Description`** — optional text shown in generated documentation.
- **`Order`** — controls where the group appears; lower numbers sort earlier.

A component without any tracked fields is skipped (and logs a warning), so `[DebugGroup]` on its own does nothing until at least one field is marked.

### Marking the field

Tag each field you want tracked with `[DebugSetting]`. The scanner walks the whole inheritance chain, so fields declared on a base class are picked up too. Only **public instance fields** are collected — a private or static field is ignored even with the attribute.

```csharp
[DebugSetting(Label = "Suppress Scan/Load/Save Logs", Description = "Hide the routine scan, load and save log messages.")]
public bool SuppressProcessLogs = true;
```

Once marked, the field's value is serialized to disk on save and pushed back into the live component on load, keyed by group name and field name.

### Field options

`[DebugSetting]` takes several optional properties to refine how a field is presented and persisted:

- **`Label`** — the human-readable name for the field. Falls back to the field name if left unset.
- **`Description`** — tooltip / description text for tooling and generated docs.
- **`Min`** / **`Max`** — value hints for `int` and `float` fields. These are hints for tooling only; they are not enforced.
- **`ReadOnly`** — the field is still serialized, but flagged as non-editable in tooling.
- **`Ignore`** — excludes the field from tracking entirely, so it is neither scanned nor persisted.


### Remarks

The implementation does not restrict the user from adding multiple declarations of [DebugGroup] with the same parameters (i.e: name, etc). However the serializer will only persist one of these instances and will
