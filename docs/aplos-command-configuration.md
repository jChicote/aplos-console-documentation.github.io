# AplosCommandConfiguration

`AplosCommandConfiguration` is a `ScriptableObject` that bundles the command actions and the
prefabs the console needs to build itself. It is created from the Unity asset menu via
`AplosConsole/Aplos Command Configuration` (namespace `AplosConsole.Scriptable.Definitions`).

<details>
<summary><strong>Inheritance</strong></summary>

```
object
 ↳ Object
    ↳ ScriptableObject
       ↳ AplosCommandConfiguration
```

</details>
<br>

**Inherited Members:**

- `ScriptableObject.CreateInstance(Type)`
- `Object.name`
- `Object.GetInstanceID()`
- `Object.Destroy(Object)`
- `Object.Instantiate(Object)`
- …

***Namespace***: `AplosConsole.Scriptable.Definitions`

## Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `CommandActions` | `List<AplosCommandActionAssest>` | The named command actions the console registers, each pairing a display name with its command constructor. |
| `PlayerInputPrefab` | `GameObject` | Prefab spawned to drive player input for the console. |
| `ConsoleListItemPrefab` | `GameObject` | Prefab used to instantiate each entry in the console's list. |

## AplosCommandActionAssest

A `[Serializable]` nested type that names a single command action and the constructor that
builds it. Appears as an editable entry in the `CommandActions` list.

***Namespace***: `AplosConsole.Scriptable.Definitions`

### Properties

| Name | Data Type | Description |
| --- | --- | --- |
| `Name` | `string` | Display name for the command action. |
| `CommandConstructor` | `AplosConsoleCommandConstructor` | The [constructor](aplos-console-command-constructor.md) that builds the command this entry registers. |
