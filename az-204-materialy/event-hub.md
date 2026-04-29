

# Azure Event Hub
---

[Prev: Event Grid](event-grid.md) | [Next: Front Door](front-door.md)

- Usługa do zbierania i przetwarzania dużych ilości zdarzeń (**event streaming**).
- Wspiera scenariusze IoT, telemetryka, logi, big data.
- Integracja z Stream Analytics, Functions, Databricks, Logic Apps.

## Znaczenie na AZ-204
- Pozwala na skalowalne zbieranie i przetwarzanie zdarzeń w czasie rzeczywistym.
- Umożliwia integrację z systemami analitycznymi i przetwarzanie strumieniowe.

## Kluczowe pojęcia
- **Event Hub Namespace**: kontener logiczny dla hubów.
- **Event Hub**: kanał do przesyłania zdarzeń.
- **Partition**: partycjonowanie danych dla skalowalności.
- **Consumer Group**: niezależni odbiorcy zdarzeń.
- **Event Publisher**: nadawca zdarzeń (np. aplikacja, IoT device).
- **Event Receiver**: odbiorca zdarzeń (np. Function, Stream Analytics).
- **Capture**: automatyczne zapisywanie zdarzeń do Storage/ADLS.
- **Throughput Units**: jednostki przepustowości (skalowanie).
- **Checkpointing**: zapamiętywanie pozycji odczytu.

## Scenariusze egzaminacyjne
- Wysyłanie i odbieranie zdarzeń przez .NET 8.
- Integracja z Azure Functions jako odbiorca.
- Ustawienie liczby partycji i consumer groups.
- Skorzystanie z Event Hub Capture.
- Skalowanie przez throughput units.

## Przykład użycia
- Wysyłanie zdarzenia przez .NET 8.
- Odbiór zdarzenia przez Azure Function.
- Automatyczne zapisywanie zdarzeń do Storage (Capture).

## Komendy
- Tworzenie namespace:
    `az eventhubs namespace create --resource-group rg --name myns --location westeurope`
- Tworzenie Event Hub:
    `az eventhubs eventhub create --resource-group rg --namespace-name myns --name myhub --partition-count 2`
- Tworzenie consumer group:
    `az eventhubs eventhub consumer-group create --resource-group rg --namespace-name myns --eventhub-name myhub --name mygroup`

## Przykład C# (.NET 8, wysyłanie zdarzenia)

## Przykład C# (.NET 8, wysyłanie zdarzenia)


```csharp
using Azure.Messaging.EventHubs;
using Azure.Messaging.EventHubs.Producer;
using System.Text;

public async Task SendEventAsync(string connectionString, string eventHubName, string data)
{
    var producer = new EventHubProducerClient(connectionString, eventHubName);
    using EventDataBatch batch = await producer.CreateBatchAsync();
    batch.TryAdd(new EventData(Encoding.UTF8.GetBytes(data)));
    await producer.SendAsync(batch);
}
```

// Odbiór zdarzenia w Azure Function:
```csharp
[Function("EventHubHandler")]
public void Run([EventHubTrigger("myhub", Connection = "EventHubConnection")] string eventData)
{
    // obsługa zdarzenia
}
```


- Użycie Azure.Messaging.EventHubs.
- Async/await.
- Przekazanie danych jako string.
- Odbiór przez Azure Function lub Stream Analytics.

## Wskazówka egzaminacyjna
- Event Hub nie przechowuje zdarzeń na stałe (domyślnie 1-7 dni).
- Najczęstszy błąd: zła liczba partycji lub brak consumer group.
- Capture wymaga Storage/ADLS i odpowiednich uprawnień.

---

