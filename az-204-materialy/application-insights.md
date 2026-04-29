

# Azure Application Insights

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

## Wskazówka egzaminacyjna
- **Instrumentation Key** nie jest już zalecany, preferuj **connection string**.
- Sampling ogranicza koszty, ale może ukryć rzadkie błędy.
- Live Metrics nie wymaga restartu aplikacji.
- Najczęstszy błąd: brak telemetry w kodzie lub brak connection string w konfiguracji.
- Distributed tracing wymaga propagacji nagłówków między usługami.


---

[Prev: API Management](api-management.md) | [Next: App Service](app-service.md)
