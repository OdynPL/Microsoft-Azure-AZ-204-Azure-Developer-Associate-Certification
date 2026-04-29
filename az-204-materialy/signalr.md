
# Azure SignalR Service

- Usługa do komunikacji w czasie rzeczywistym (WebSocket, long polling, SSE).
- Umożliwia skalowanie aplikacji SignalR w chmurze bez zarządzania infrastrukturą.
- Integracja z .NET przez SDK, wsparcie dla wielu języków i frameworków.

## Znaczenie na AZ-204
- Pozwala na budowę skalowalnych aplikacji real-time (czat, powiadomienia, dashboardy).
- Upraszcza wdrożenie SignalR w środowisku rozproszonym.
- Obsługuje autoskalowanie, wysoką dostępność, autoryzację.

## Kluczowe pojęcia
- **Hub**: centralny punkt komunikacji (klasa dziedzicząca po Hub).
- **Client**: aplikacja odbierająca/wysyłająca wiadomości.
- **Connection**: połączenie klienta z usługą.
- **Group**: logiczna grupa klientów (np. pokój czatu).
- **Scale-out**: automatyczne skalowanie połączeń.
- **Access Token**: token JWT do autoryzacji połączenia.
- **Service Mode**: Classic, Serverless, Default (różne tryby integracji).
- **Upstream**: przekazywanie zdarzeń do backendu (serverless).

## Scenariusze egzaminacyjne
- Wysyłanie i odbieranie wiadomości przez Hub.
- Skalowanie aplikacji SignalR przez Azure SignalR Service.
- Autoryzacja połączeń (np. JWT, Azure AD).
- Użycie grup do broadcastu.
- Integracja z Functions (serverless).

## Przykład użycia
- Implementacja czatu w .NET 8 przez Hub.
- Wysyłanie wiadomości do wszystkich klientów lub grupy.
- Autoryzacja połączenia przez token.

## Komendy
- Tworzenie SignalR Service:
    `az signalr create --name mysignalr --resource-group rg --sku Standard_S1 --unit-count 1 --location westeurope`
- Pobranie connection string:
    `az signalr key list --name mysignalr --resource-group rg --query primaryConnectionString`

## Przykład C# (.NET 8, wysyłanie i odbieranie wiadomości)
```csharp
using Microsoft.AspNetCore.SignalR;

public class ChatHub : Hub
{
        public async Task SendMessage(string user, string message)
        {
                await Clients.All.SendAsync("ReceiveMessage", user, message);
        }

        public async Task SendToGroup(string group, string message)
        {
                await Clients.Group(group).SendAsync("ReceiveMessage", message);
        }

        public async Task JoinGroup(string group)
        {
                await Groups.AddToGroupAsync(Context.ConnectionId, group);
        }
}
```

## Wskazówka egzaminacyjna
- SignalR Service wymaga connection string w konfiguracji aplikacji.
- Najczęstszy błąd: brak autoryzacji połączenia lub przekroczenie limitu połączeń.
- W trybie serverless nie ma własnego backendu — obsługa przez Functions.

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
