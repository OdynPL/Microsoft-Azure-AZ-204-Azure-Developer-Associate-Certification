# Azure Web PubSub

- Usługa do komunikacji w czasie rzeczywistym (WebSocket, PubSub).
- Umożliwia skalowanie komunikacji do wielu klientów.
- Integracja z .NET przez SDK.

## Przykład C# (.NET 8, wysyłanie wiadomości)

```csharp
public class MyHub : WebPubSubHub
{
    public override async Task OnConnectedAsync(ConnectionContext context)
    {
        await Clients.All.SendToAllAsync("Nowy klient połączony");
    }
}
```

- Użycie Azure.Messaging.WebPubSub.
- Klasa dziedziczy po WebPubSubHub.
- Async/await.

---

[Prev: Table Storage](table-storage.md) | [Next: Cloud Shell](cloud-shell.md)
