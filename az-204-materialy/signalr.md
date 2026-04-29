# Azure SignalR Service

- Usługa do komunikacji w czasie rzeczywistym (WebSocket).
- Umożliwia skalowanie aplikacji SignalR w chmurze.
- Integracja z .NET przez SDK.

## Przykład C# (.NET 8, wysyłanie wiadomości)

```csharp
public class ChatHub : Hub
{
    public async Task SendMessage(string user, string message)
    {
        await Clients.All.SendAsync("ReceiveMessage", user, message);
    }
}
```

- Użycie Microsoft.Azure.SignalR.
- Klasa Hub dziedziczy po Hub.
- Async/await.

---

[Prev: Service Bus](service-bus.md) | [Next: SQL Database](sql-database.md)
