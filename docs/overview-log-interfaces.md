# Interfaces

## IExportableLogSettings

Contract for a log view whose retained history can be exported to an external file. Implemented by
[OverviewLoggerView](overview-logger-view.md).

***Namespace***: `AplosConsole.Logger`

### Public methods

<h2 id="exportlogs"><code>ExportLogs</code></h2>

**Example**

```csharp
exportableLogSettings.ExportLogs();
```

**Description:** Exports the retained log history to the configured destination.

<br>
