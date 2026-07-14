# Adding Commands

_A guide to creating console commands and getting them into Aplos Console._

## How it works

_An overview of the command system and how commands are registered and invoked._

1. Authoring Commands - Developed commands live as objects and can be used interchangeably.
2. Registration - Command objects are then registered against the console so that they show up as entries within the console command list.
3. Execution - When selected, the underlying configured action is invoked against the selected command.

## Developing commands

1. Creating the command object

**Example**

```csharp
AplosConsole.Instance.UnregisterCommand("hello");
```

2.Adding command objects to oonsole

## Adding commands during runtime

_How to register commands dynamically while the game is running._

## Configuring pre-loaded commands

_How to set up commands that are available from startup._
