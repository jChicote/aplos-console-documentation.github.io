# Adding Commands

A guide to creating console commands and getting them into Aplos Console.

## How it works

_An overview of the command system and how commands are registered and invoked._

1. **Authoring** — commands live as objects and can be used interchangeably.
2. **Registration** — command objects are registered against the console so that they show up as entries within the console command list.
3. **Execution** — when selected, the underlying configured action is invoked against the selected command.

## Developing commands

_How to author a command object and attach it in Unity._

1. Create the command object.
    1. Create a new class component inheriting from [`AplosConsoleCommandConstructor`](aplos-console-command-constructor.md).
    2. Add the methods that contain the behaviour required for each command, and register them as part of the [`RegisterCommand`](aplos-console-command-constructor.md#registercommand) override.
2. In Unity, create a new GameObject and attach the recently created component.

**Example**

```csharp
public class UnityLogCommand : AplosConsoleCommandConstructor
{

    public override void RegisterCommand(IConsoleCommandSystem commandSystem)
    {
        AplosDebugCommand printLog = new AplosDebugCommand(
            "printLog",
            "Command for printing some random text to Unity's Console.",
            "printLog",
            this.LogToUnityConsoleCommand);

        commandSystem.RegisterCommand(printLog);
    }

    private void LogToUnityConsoleCommand()
    {
        // Arrange

        // Act
        Debug.Log("Log this to Unity Console.");
    }

}
```

## Adding commands during runtime

_How to register a command while the console is already running._

1. Open the [`AplosConsole`](aplos-console.md) component from the inspector.
2. Add a new entry to [`AddOnCommands`](aplos-console.md#properties) and pass in a command GameObject.
3. Press the **Refresh Command List** button.
4. Show all commands from the Console view.

## Configuring pre-loaded commands

_How to bundle commands into a configuration so they load with the console._

1. Create the command GameObject.
2. Create a prefab of the command GameObject.
3. Locate your instance of the [`AplosCommandConfiguration`](aplos-command-configuration.md) ScriptableObject. If one does not exist, create a new command configuration by right-clicking in the Project area and navigating to **Create → AplosConsole → Aplos Command Configuration**.
    1. If a new command configuration is created, set this ScriptableObject on the [`AplosConsole`](aplos-console.md) component's `CommandConfiguration` field and the [`AplosInputManager`](aplos-input-manager.md) component's `Settings` field.
4. Play the scene.
5. Open the console by pressing `` ` `` key.
6. Show all commands (command: `help`).
