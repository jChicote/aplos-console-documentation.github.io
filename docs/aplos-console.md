# AplosConsole

`AplosConsole` is responsible for console actions and command handling. It is a sealed
`MonoBehaviour` singleton (namespace `AplosConsole`) that implements `IConsoleCommandSystem`
and `IConsoleInputProvider`.

## Properties

| Name | Description |
| --- | --- |
| `Instance` | Static singleton reference to the active console. Assigned on `Awake`, read-only from outside the class. |
| `CommandList` | The list of registered command objects currently presented in the command display list. |
| `IsOpen` | Whether the console is currently open (active). |
| `CommandConfiguration` | Required dependency. Serialized reference to the `AplosCommandConfiguration` asset that supplies the default command set. |
| `AplosWindow` | Required dependency. Serialized reference to the console window `GameObject`; its active state determines the initial open/closed state. |
| `AddOnCommands` | List of additional `AplosConsoleCommandConstructor`s registered during initialisation. |

## Events

| Name | Description |
| --- | --- |
| `OnAutoComplete` | Raised when auto-complete is requested (via `AutoCompletePressed`). |
| `OnInitialise` | Raised once after commands are first initialised. |
| `OnRefresh` | Raised after the command list is refreshed (via `RefreshCommands`). |
| `OnOpenConsole` | Raised when the console opens. |
| `OnCloseConsole` | Raised when the console closes. |
| `OnNavigate` | Raised when navigation is requested; passes the navigation direction as an `int`. |
| `OnShowAll` | Raised when all commands should be shown (e.g. the built-in `help` command). |
| `OnSubmit` | Raised when the current input is submitted (via `SubmitPressed`). |
| `OnCommandsChanged` | Raised whenever the set of registered commands changes (runtime register/unregister). |

## Public methods

| Name | Description |
| --- | --- |
| `OpenConsole()` | Marks the console active and raises `OnOpenConsole`. |
| `CloseConsole()` | Marks the console inactive and raises `OnCloseConsole`. |
| `RegisterCommand(AplosDebugCommandBase command)` | Registers a command to be collected and presented in the command display list. |
| `RegisterCommand(string id, string description, string format, Action command)` | Convenience overload that builds and registers a parameterless command in one call and returns the created `AplosDebugCommand`. |
| `UnregisterCommand(string id)` | Removes all registered commands matching the given id and raises `OnCommandsChanged`. |
| `RefreshCommands()` | Clears and rebuilds the command list back to the default initial commands, then raises `OnRefresh`. |
| `AutoCompletePressed()` | Input hook that raises `OnAutoComplete`. |
| `SubmitPressed()` | Input hook that raises `OnSubmit`. |
| `NavigatePressed(int direction)` | Input hook that raises `OnNavigate` with the given direction. |
| `ToggleDebug()` | Toggles the console between its open and closed states. |

## Static methods

_This class currently exposes no static methods. Global access is provided through the static `Instance` property listed under [Properties](#properties)._
