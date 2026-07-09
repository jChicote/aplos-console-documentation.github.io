# Interfaces

The console is expressed through one contract in the `AplosConsole.Console` namespace.
`IConsoleInputProvider` is the surface used to drive the console from an input source,
implemented by [AplosConsole](aplos-console.md).

## IConsoleInputProvider

Contract for a type that can be driven by input to control the console.

### Methods

| Name | Description |
| --- | --- |
| `AutoCompletePressed()` | Input hook that requests auto-complete. |
| `SubmitPressed()` | Input hook that submits the current input. |
| `NavigatePressed(int direction)` | Input hook that requests navigation in the given direction. |
| `ToggleDebug()` | Input hook that toggles the console between its open and closed states. |
