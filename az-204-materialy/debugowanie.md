
# Debugowanie aplikacji w Azure
---

[Prev: Sposoby deployowania aplikacji](deployment-methods.md) | [Next: Azure Monitor](monitor.md)

**Definicja:**
- **Debugowanie** to proces wykrywania i usuwania błędów w aplikacjach wdrożonych na platformie Azure.
- Obejmuje monitorowanie, analizę logów, śledzenie żądań, zdalne debugowanie i diagnostykę.

**Znaczenie na egzaminie AZ-204:**
- Wymagana znajomość narzędzi do debugowania aplikacji w chmurze.
- Często pytania o Application Insights, logi, zdalny debug, troubleshooting.

## Kluczowe pojęcia i komponenty

- **Application Insights** – monitorowanie, telemetry, śledzenie żądań, wykrywanie wyjątków.
- **Log Analytics** – zaawansowane zapytania do logów (KQL).
- **Azure Monitor** – zbiera metryki, logi, alerty z różnych usług.
- **Live Metrics Stream** – podgląd na żywo metryk i błędów.
- **Snapshot Debugger** – zdalne debugowanie kodu produkcyjnego (App Service, Functions).
- **Remote Debugging** – podłączanie się do procesu aplikacji przez Visual Studio.
- **Diagnostyka App Service** – narzędzia do analizy problemów z wydajnością, błędami HTTP, restartami.
- **Log Stream** – podgląd logów na żywo z App Service.
- **Kudu (Advanced Tools)** – narzędzia diagnostyczne dla App Service (dostęp przez /scm).
- **Azure Storage Logs** – logi operacji na Storage Account.
- **Event Grid/Event Hub** – przesyłanie logów i zdarzeń do dalszej analizy.

- **Diagnostyka Functions** – Monitor w portalu Functions, podgląd logów wywołań, błędów, retry.
- **Diagnostyka AKS** – kubectl logs, podgląd logów podów, monitoring kontenerów.
- **Diagnostyka VM** – Serial Console, Boot Diagnostics, logi systemowe.

## Scenariusze egzaminacyjne

- Konfiguracja Application Insights w Web App, Functions, AKS.
- Analiza błędów HTTP 500, restartów, timeoutów.
- Użycie Live Metrics do wykrywania problemów w czasie rzeczywistym.
- Zdalne debugowanie przez Visual Studio (App Service, VM).
- Pisanie zapytań KQL w Log Analytics do analizy logów.
- Diagnostyka problemów z połączeniem do bazy, timeoutów, błędów autoryzacji.
- Ustawienie alertów na metryki (np. CPU, liczba błędów).

## Przykłady użycia

### Włączenie Application Insights przez Azure CLI
```powershell
az monitor app-insights component create \
  --app myappinsights \
  --location westeurope \
  --resource-group myRG
az webapp config appsettings set \
  --name mywebapp \
  --resource-group myRG \
  --settings "APPINSIGHTS_INSTRUMENTATIONKEY=<key>"
```

### Live Metrics w Application Insights
- Otwórz Application Insights > Live Metrics Stream.
- Obserwuj żądania, błędy, zależności w czasie rzeczywistym.

### Snapshot Debugger (App Service)
- Włącz w Application Insights > Snapshot Debugger.
- Zainstaluj rozszerzenie w aplikacji (np. NuGet Microsoft.ApplicationInsights.SnapshotCollector).
- Po wystąpieniu wyjątku snapshot pojawi się w portalu.

### Remote Debugging przez Visual Studio
- Włącz Remote Debugging w ustawieniach App Service.
- Połącz się przez Visual Studio (Attach to Process).
- Debugowanie działa tylko w trybie Standard i wyższym.

### Diagnostyka App Service
- App Service > Diagnose and solve problems.
- Analiza restartów, błędów HTTP, problemów z wydajnością.

### Log Stream (App Service)
```powershell
az webapp log tail --name mywebapp --resource-group myRG
```

### Przykład C# (.NET 8) – rejestrowanie błędów do Application Insights
```csharp
using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.Extensibility;

var telemetry = new TelemetryClient(new TelemetryConfiguration("<instrumentation-key>"));
try
{
    // ... kod aplikacji ...
}
catch(Exception ex)
{
    telemetry.TrackException(ex);
    throw;
}
```

## Dobre praktyki

- Zawsze włącz Application Insights dla aplikacji produkcyjnych.
- Używaj niestandardowych metryk i logów (TrackEvent, TrackMetric).
- Analizuj logi i metryki regularnie, nie tylko przy awarii.
- Ustaw alerty na krytyczne metryki i błędy.
- Nie loguj danych wrażliwych (PII) do Application Insights.
- Używaj slotów do testowania zmian bez wpływu na produkcję.
- W przypadku problemów z wydajnością analizuj zależności (Dependencies).
- Włącz diagnostykę Storage/SQL jeśli aplikacja korzysta z tych usług.

## Wskazówki i pułapki egzaminacyjne

- Remote Debugging wymaga odpowiedniego planu App Service (Standard+).
- Snapshot Debugger nie działa na wszystkich platformach (np. Linux ograniczony).
- Brak telemetry = brak danych o błędach.
- Log Stream pokazuje tylko logi aplikacji, nie systemowe.
- Kudu pozwala na eksplorację plików, logów, uruchamianie poleceń.
- Application Insights wymaga connection string lub instrumentation key.
- Diagnostyka App Service wykrywa typowe błędy automatycznie.
