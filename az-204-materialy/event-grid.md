# Azure Event Grid

- Usługa do obsługi zdarzeń (eventing) w Azure.
- Umożliwia routing zdarzeń między usługami.
- Wspiera subskrypcje i filtrowanie zdarzeń.

## Przykład C# (.NET 8, wysyłanie zdarzenia)

```csharp
public async Task SendEventAsync(string topicEndpoint, string key, EventGridEvent eventGridEvent)
{
    var credentials = new AzureKeyCredential(key);
    var client = new EventGridPublisherClient(new Uri(topicEndpoint), credentials);
    await client.SendEventAsync(eventGridEvent);
}
```

- Użycie Azure.Messaging.EventGrid.
- Async/await.
- Przekazanie obiektu EventGridEvent.

---

[Prev: Deployment (Bicep)](deployment-bicep.md) | [Next: Event Hub](event-hub.md)
