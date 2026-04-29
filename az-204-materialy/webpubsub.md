

# Azure Web PubSub
---

[Prev: Table Storage](table-storage.md) | [Next: Cloud Shell](cloud-shell.md)

- Usługa do komunikacji w czasie rzeczywistym (WebSocket, PubSub, SignalR protocol).
- Umożliwia skalowanie komunikacji do tysięcy klientów bez zarządzania infrastrukturą.
- Integracja z .NET, Node.js, Python przez SDK i REST API.

## Znaczenie na AZ-204
- Pozwala na budowę skalowalnych aplikacji real-time (czat, powiadomienia, IoT).
- Obsługuje broadcast, grupy, autoryzację, WebSocket na dużą skalę.
- Alternatywa dla SignalR Service, wsparcie dla protokołu WebSocket i PubSub.

## Kluczowe pojęcia
- **Hub**: centralny punkt komunikacji (klasa dziedzicząca po WebPubSubHub).
- **Client**: aplikacja odbierająca/wysyłająca wiadomości.
- **Connection**: połączenie klienta z usługą.
- **Group**: logiczna grupa klientów (np. pokój czatu).
- **Broadcast**: wysyłanie wiadomości do wszystkich klientów.
- **Event Handler**: obsługa zdarzeń (OnConnected, OnDisconnected, OnMessageReceived).
- **Access Token**: token JWT do autoryzacji połączenia.
- **Upstream**: przekazywanie zdarzeń do backendu (serverless).

## Scenariusze egzaminacyjne
- Wysyłanie i odbieranie wiadomości przez Hub.
- Skalowanie aplikacji WebSocket przez Web PubSub.
- Autoryzacja połączeń (np. JWT, Azure AD).
- Użycie grup do broadcastu.
- Integracja z Functions (serverless).

## Przykład użycia
- Implementacja czatu w .NET 8 przez WebPubSubHub.
- Wysyłanie wiadomości do wszystkich klientów lub grupy.
- Autoryzacja połączenia przez token.

## Komendy
- Tworzenie Web PubSub:
    `az webpubsub create --name mypubsub --resource-group rg --sku Standard_S1 --unit-count 1 --location westeurope`
- Pobranie connection string:
    `az webpubsub key show --name mypubsub --resource-group rg --query primaryConnectionString`

## Przykład C# (.NET 8, wysyłanie i odbieranie wiadomości)
```csharp
using Azure.Messaging.WebPubSub.AspNetCore;

public class MyHub : WebPubSubHub
{
        public override async Task OnConnectedAsync(ConnectionContext context)
        {
                await Clients.All.SendToAllAsync("Nowy klient połączony");
        }

        public override async Task OnMessageReceivedAsync(ConnectionContext context, WebPubSubMessage message)
        {
                await Clients.All.SendToAllAsync($"Wiadomość: {message.Data}");
        }

        public override async Task OnDisconnectedAsync(ConnectionContext context)
        {
                await Clients.All.SendToAllAsync("Klient rozłączony");
        }
}
```

## Wskazówka egzaminacyjna
- Web PubSub wymaga connection string w konfiguracji aplikacji.
- Najczęstszy błąd: brak autoryzacji połączenia lub przekroczenie limitu połączeń.
- W trybie serverless nie ma własnego backendu — obsługa przez Functions.

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

