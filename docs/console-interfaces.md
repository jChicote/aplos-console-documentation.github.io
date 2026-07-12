# Interfaces

## IConsoleInputProvider

Contract for a type that can be driven by input to control the console.

### Methods

| Name | Description |
| --- | --- |
| `AutoCompletePressed` | Input hook that requests auto-complete. |
| `SubmitPressed` | Input hook that submits the current input. |
| `NavigatePressed` | Input hook that requests navigation in the given direction. |
| `ToggleDebug` | Input hook that toggles the console between its open and closed states. |

<details>
<summary>Declarations</summary>

```csharp
void AutoCompletePressed();
void SubmitPressed();
void NavigatePressed(int direction);
void ToggleDebug();
```

</details>
