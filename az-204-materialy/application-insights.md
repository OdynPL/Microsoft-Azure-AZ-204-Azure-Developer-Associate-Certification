

# Azure Application Insights
---

[Prev: API Management](api-management.md) | [Next: App Service](app-service.md)

## Definicja
- Usługa do monitorowania aplikacji w czasie rzeczywistym (**APM**).
- Zbiera logi, metryki, śledzi błędy, wydajność, zależności i żądania.
- Umożliwia analizę działania aplikacji i szybkie wykrywanie problemów.

## Znaczenie na AZ-204
- Pozwala szybko diagnozować problemy w aplikacji.
- Integracja z .NET, Functions, App Service, AKS, Logic Apps.
- Umożliwia automatyczne alerty, wykrywanie anomalii, analizę ścieżek użytkownika.

## Kluczowe pojęcia
- **Telemetry**: dane o zdarzeniach, błędach, wydajności, żądaniach, zależnościach.
- **Instrumentation Key**: identyfikator instancji Application Insights (zastępowany przez connection string).
- **Connection String**: nowy sposób konfiguracji połączenia.
- **Live Metrics**: podgląd na żywo, bez restartu aplikacji.
- **Distributed Tracing**: śledzenie żądań między usługami (np. microservices).
- **Sampling**: ograniczanie liczby wysyłanych danych telemetrycznych.
- **Log Analytics**: zaawansowane zapytania i analiza danych (KQL).
- **Smart Detection**: automatyczne wykrywanie anomalii.
- **Availability Test**: testowanie dostępności endpointów.
- **Dependency Tracking**: monitorowanie połączeń z bazą, API, usługami zewnętrznymi.
- **Custom Events**: własne zdarzenia i metryki.

**Kluczowe pojęcia dodatkowe:**
- **Cloud Role Name** – identyfikacja komponentu w rozproszonej architekturze.
- **Operation Id** – śledzenie powiązanych żądań w distributed tracing.

## Scenariusze egzaminacyjne
- Rejestrowanie zdarzeń, błędów, metryk w .NET 8 (Web API, Functions).
- Analiza wydajności, alerty, wykrywanie anomalii.
- Integracja z App Service, Functions, AKS.
- Konfiguracja sampling, distributed tracing.
- Wysyłanie custom events i metryk.
- Analiza logów przez KQL w Log Analytics.
- Testowanie dostępności endpointów (Availability Test).

## Przykład użycia
- TrackEvent, TrackException, TrackDependency w kodzie .NET.
- Analiza logów i metryk w portalu Azure.
- Konfiguracja alertów na błędy lub spadek wydajności.
- Testowanie dostępności API.

## Komendy
- Tworzenie Application Insights:
  `az monitor app-insights component create --app myapp --location westeurope --resource-group rg --application-type web`
- Pobranie connection string:
  `az monitor app-insights component show --app myapp --resource-group rg --query connectionString`
- Włączenie monitoringu w App Service:
  `az webapp config appsettings set --resource-group rg --name myapp --settings "APPLICATIONINSIGHTS_CONNECTION_STRING=..."`

- Pobranie logów przez PowerShell:
  `Search-AzMonitorLog -ResourceGroupName rg -WorkspaceName myapp -Query "exceptions | take 10"`

## Przykład kodu C# (.NET 8)
```csharp
using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.Extensibility;

var builder = WebApplication.CreateBuilder(args);
builder.Services.AddApplicationInsightsTelemetry();

var app = builder.Build();

app.MapGet("/error", (TelemetryClient telemetry) =>
{
  try
  {
    throw new Exception("Test error");
  }
  catch (Exception ex)
  {
    telemetry.TrackException(ex);
    return Results.Problem("Błąd zgłoszony do Application Insights");
  }
});

app.Run();
```

```csharp
// Przykład 2: Wysyłanie custom event i dependency
using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

var builder = WebApplication.CreateBuilder(args);
builder.Services.AddApplicationInsightsTelemetry();
var app = builder.Build();
app.MapGet("/custom", (TelemetryClient telemetry) =>
{
    telemetry.TrackEvent("CustomEvent", new Dictionary<string, string> { { "User", "test" } });
    telemetry.TrackDependency("HTTP", "ExternalAPI", "GET /data", DateTimeOffset.Now, TimeSpan.FromMilliseconds(120), true);
    return Results.Ok("Custom event i dependency wysłane");
});
// Przykład 3: Wysyłanie custom metrics
app.MapGet("/metric", (TelemetryClient telemetry) =>
{
  telemetry.GetMetric("CustomMetric").TrackValue(42);
  return Results.Ok("Custom metric wysłana");
});

// Przykład 4: Logowanie do Application Insights przez ILogger
var logger = app.Services.GetRequiredService<ILoggerFactory>().CreateLogger("AppLogger");
app.MapGet("/log", () =>
{
  logger.LogWarning("To jest log ostrzeżenia do Application Insights");
  return Results.Ok("Log wysłany");
});

// Przykład 5: Alert na błąd (konfiguracja w portalu Azure)
// 1. Przejdź do Application Insights > Alerts > New alert rule
// 2. Ustaw Condition: Custom log search (np. exceptions > 0 w ciągu 5 min)
// 3. Ustaw Action Group (np. email, SMS)
// 4. Zapisz i przetestuj wywołując endpoint /error
app.Run();
```

## Wskazówka egzaminacyjna
- **Instrumentation Key** nie jest już zalecany, preferuj **connection string**.
- Sampling ogranicza koszty, ale może ukryć rzadkie błędy.
- Live Metrics nie wymaga restartu aplikacji.
- Najczęstszy błąd: brak telemetry w kodzie lub brak connection string w konfiguracji.
- Distributed tracing wymaga propagacji nagłówków między usługami.
  - Częsty błąd: brak Cloud Role Name lub Operation Id w rozproszonych systemach.


---

