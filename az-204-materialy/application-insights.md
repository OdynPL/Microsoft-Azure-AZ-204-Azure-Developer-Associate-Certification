# Azure Application Insights

- Monitorowanie aplikacji w czasie rzeczywistym.
- Zbieranie logów, metryk, śledzenie błędów.
- Integracja z .NET przez SDK.

## Przykład C# (.NET 8, rejestrowanie telemetryki)

```csharp
public class MyService
{
    private readonly TelemetryClient _telemetry;
    public MyService(TelemetryClient telemetry)
    {
        _telemetry = telemetry;
    }
    public void TrackEvent(string name)
    {
        _telemetry.TrackEvent(name);
    }
}
```

- Użycie Microsoft.ApplicationInsights.
- Wstrzykiwanie TelemetryClient przez DI.

---

[Prev: API Management](api-management.md) | [Next: App Service](app-service.md)
