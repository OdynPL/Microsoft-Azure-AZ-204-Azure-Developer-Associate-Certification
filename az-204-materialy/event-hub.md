# Azure Event Hub

- Usługa do zbierania i przetwarzania dużych ilości zdarzeń.
- Wspiera scenariusze IoT, telemetryka, logi.
- Integracja z Stream Analytics, Functions.

## Przykład C# (.NET 8, wysyłanie zdarzenia)

```csharp
public async Task SendEventAsync(string connectionString, string eventHubName, string data)
{
    var producer = new EventHubProducerClient(connectionString, eventHubName);
    using EventDataBatch batch = await producer.CreateBatchAsync();
    batch.TryAdd(new EventData(Encoding.UTF8.GetBytes(data)));
    await producer.SendAsync(batch);
}
```

- Użycie Azure.Messaging.EventHubs.
- Async/await.
- Przekazanie danych jako string.

---

[Prev: Event Grid](event-grid.md) | [Next: Front Door](front-door.md)
