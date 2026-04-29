


# Azure Functions
---

[Prev: Blob Storage](blob-storage.md) | [Next: CDN](cdn.md)

## Definicja
- **Serverless compute** do uruchamiania kodu na żądanie.
- Obsługa wielu języków (C#, JavaScript, Python, PowerShell, Java).
- Automatyczne skalowanie, rozliczanie za wywołania.

## Znaczenie na AZ-204
- Pozwala budować skalowalne API, automaty, integracje, ETL.
- Minimalizuje koszty i zarządzanie infrastrukturą.
- Wspiera architekturę event-driven, automatyzację, DevOps.

## Kluczowe pojęcia
- **Trigger (wyzwalacz)**: uruchamia funkcję (HTTP, Timer, Queue, Blob, Event Grid, Service Bus, Cosmos DB, Event Hub).
- **Input/Output bindings**: szybki dostęp do Storage, DB, kolejek, bez kodowania logiki połączenia.
- **Consumption Plan**: płatność za wywołania, automatyczne skalowanie, cold start.
- **Premium Plan**: brak cold start, VNet, dłuższy timeout, autoskalowanie.
- **Dedicated (App Service) Plan**: stałe zasoby, brak cold start.
- **Deployment slots**: środowiska testowe/produkcyjne.
- **Dependency Injection**: wstrzykiwanie zależności przez DI (od .NET 5+).
- **Function App**: kontener logiczny dla funkcji.
- **Host.json**: plik konfiguracyjny funkcji.
- **Local.settings.json**: ustawienia lokalne (tylko dev).

## Triggery (wyzwalacze)
| Trigger         | Opis | Przykład |
|-----------------|------|----------|
| HTTP            | Wywołanie przez żądanie HTTP | API, webhook |
| Timer           | Harmonogram (CRON) | Automatyczne zadania |
| Queue Storage   | Nowa wiadomość w kolejce | Przetwarzanie zadań |
| Service Bus     | Nowa wiadomość w Service Bus | Integracja systemów |
| Event Grid      | Zdarzenie w Event Grid | Reakcja na zdarzenia |
| Blob Storage    | Nowy plik w kontenerze | Przetwarzanie plików |
| Cosmos DB       | Zmiana w bazie | ETL, synchronizacja |
| Event Hub       | Nowe zdarzenie | Telemetria, IoT |

## Rodzaje funkcji
- **HTTP-triggered**: API, webhooki, integracje z zewnętrznymi systemami.
- **Event-driven**: reagowanie na zdarzenia z Event Grid, Service Bus, Storage.
- **Timer-triggered**: zadania cykliczne, automatyzacja.
- **Data processing**: przetwarzanie plików, danych, kolejek.

## Autoryzacja funkcji
- **AuthorizationLevel**:
  - `Anonymous`: brak autoryzacji, każdy może wywołać.
  - `Function`: wymaga klucza funkcji (x-functions-key).
  - `Admin`: wymaga klucza admina (x-functions-admin-key).
  - `User`: integracja z Azure AD (tylko Premium/Dedicated).
- **Azure AD**: ochrona endpointów przez OAuth2/OpenID Connect.
- **App Service Authentication**: włączenie autoryzacji przez portal (Easy Auth).

### Przykład autoryzacji przez Azure AD (minimal API)
```csharp
[Function("SecureApi")]
public async Task<HttpResponseData> Run(
    [HttpTrigger(AuthorizationLevel.Anonymous, "get")] HttpRequestData req,
    FunctionContext context)
{
    var principal = context.GetHttpContext().User;
    if (!principal.Identity.IsAuthenticated)
        return req.CreateResponse(HttpStatusCode.Unauthorized);
    // ...
}
```

## Przykłady kodu C# (.NET 8)

### 1. HTTP Trigger (API)
```csharp
[Function("HttpExample")]
public async Task<HttpResponseData> Run(
    [HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req)
{
    var response = req.CreateResponse(HttpStatusCode.OK);
    await response.WriteStringAsync("Hello from Azure Function!");
    return response;
}
```

### 2. Queue Trigger
```csharp
[Function("QueueProcessor")]
public void Run([QueueTrigger("myqueue")] string message, FunctionContext context)
{
    var logger = context.GetLogger("QueueProcessor");
    logger.LogInformation($"Wiadomość: {message}");
}
```

### 3. Blob Trigger
```csharp
[Function("BlobProcessor")]
public void Run([BlobTrigger("container/{name}")] Stream blob, string name, FunctionContext context)
{
    var logger = context.GetLogger("BlobProcessor");
    logger.LogInformation($"Nowy plik: {name}");
}
```

### 4. Timer Trigger
```csharp
[Function("TimerJob")]
public void Run([TimerTrigger("0 */5 * * * *")] TimerInfo timer, FunctionContext context)
{
    var logger = context.GetLogger("TimerJob");
    logger.LogInformation($"Timer wywołany: {DateTime.Now}");
}
```

### 5. Service Bus Trigger
```csharp
[Function("ServiceBusProcessor")]
public void Run([ServiceBusTrigger("myqueue", Connection = "ServiceBusConnection")] string message, FunctionContext context)
{
    var logger = context.GetLogger("ServiceBusProcessor");
    logger.LogInformation($"Odebrano: {message}");
}
```

## Komendy
- Tworzenie Function App:
  `az functionapp create --resource-group rg --consumption-plan-location westeurope --runtime dotnet --functions-version 4 --name myfuncapp --storage-account mystorage`
- Publikacja kodu:
  `func azure functionapp publish myfuncapp`
- Dodanie triggera:
  `func new --template "Http Trigger" --name MyFunction`

## Wskazówka egzaminacyjna
- Consumption Plan ma cold start (opóźnienie przy pierwszym wywołaniu).
- Premium Plan nie ma cold start, obsługuje VNet, dłuższy timeout.
- Nie każda biblioteka .NET jest wspierana (sandbox).
- Ograniczenia timeout: 5 min (Consumption), 60 min (Premium/Dedicated).
- Najczęstszy błąd: brak uprawnień do Storage lub złe ustawienie AuthorizationLevel.

---

---

