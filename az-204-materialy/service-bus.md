# Azure Service Bus

- Usługa kolejkowania i przesyłania komunikatów.
- Wspiera kolejki i tematy (topics).
- Umożliwia komunikację asynchroniczną między usługami.

## Przykład C# (.NET 8, wysyłanie wiadomości)

```csharp
public async Task SendMessageAsync(string connectionString, string queueName, string message)
{
    var client = new ServiceBusClient(connectionString);
    var sender = client.CreateSender(queueName);
    await sender.SendMessageAsync(new ServiceBusMessage(message));
}
```

- Użycie Azure.Messaging.ServiceBus.
- Async/await.
- Przekazanie tekstu wiadomości.

---

[Prev: Redis](redis.md) | [Next: SignalR](signalr.md)
