
# Azure Service Bus

- Usługa kolejkowania i przesyłania komunikatów (enterprise messaging).
- Wspiera kolejki (queues) i tematy (topics/subscriptions).
- Umożliwia komunikację asynchroniczną, buforowanie, integrację systemów.

## Znaczenie na AZ-204
- Pozwala na niezawodną komunikację między usługami, mikroserwisami.
- Wspiera wzorce pub/sub, kolejki FIFO, delayed delivery.
- Integracja z Functions, Logic Apps, Event Grid.

## Kluczowe pojęcia
- **Queue**: kolejka komunikatów (FIFO).
- **Topic**: kanał publikacji komunikatów do wielu subskrypcji.
- **Subscription**: odbiorca komunikatów z topic.
- **Session**: grupowanie komunikatów (FIFO, ordering).
- **Dead-letter Queue (DLQ)**: przechowywanie nieprzetworzonych komunikatów.
- **PeekLock**: odczyt komunikatu bez usuwania (potwierdzenie po przetworzeniu).
- **ReceiveAndDelete**: odczyt i usunięcie komunikatu jednocześnie.
- **Auto-forwarding**: automatyczne przekierowanie komunikatów.
- **Duplicate Detection**: wykrywanie duplikatów.
- **Scheduled Delivery**: opóźnione dostarczenie komunikatu.
- **Message TTL**: czas życia komunikatu.

## Scenariusze egzaminacyjne
- Wysyłanie i odbieranie komunikatów przez .NET 8.
- Użycie topic/subscription do pub/sub.
- Obsługa dead-letter queue.
- Ustawienie TTL, duplicate detection, scheduled delivery.
- Integracja z Azure Functions jako trigger.

## Przykład użycia
- Wysyłanie komunikatu do kolejki przez .NET 8.
- Odbiór komunikatu przez Azure Function.
- Przekierowanie komunikatu do DLQ po błędzie.

## Komendy
- Tworzenie namespace:
    `az servicebus namespace create --resource-group rg --name myns --location westeurope`
- Tworzenie kolejki:
    `az servicebus queue create --resource-group rg --namespace-name myns --name myqueue`
- Tworzenie topic:
    `az servicebus topic create --resource-group rg --namespace-name myns --name mytopic`
- Tworzenie subscription:
    `az servicebus topic subscription create --resource-group rg --namespace-name myns --topic-name mytopic --name mysub`

## Przykład C# (.NET 8, wysyłanie i odbieranie wiadomości)
```csharp
using Azure.Messaging.ServiceBus;

// Wysyłanie
public async Task SendMessageAsync(string connectionString, string queueName, string message)
{
        var client = new ServiceBusClient(connectionString);
        var sender = client.CreateSender(queueName);
        await sender.SendMessageAsync(new ServiceBusMessage(message));
}

// Odbiór
public async Task<string> ReceiveMessageAsync(string connectionString, string queueName)
{
        var client = new ServiceBusClient(connectionString);
        var receiver = client.CreateReceiver(queueName);
        ServiceBusReceivedMessage msg = await receiver.ReceiveMessageAsync();
        return msg.Body.ToString();
}
```

// Odbiór przez Azure Function:
```csharp
[Function("ServiceBusHandler")]
public void Run([ServiceBusTrigger("myqueue", Connection = "ServiceBusConnection")] string message)
{
        // obsługa komunikatu
}
```

## Wskazówka egzaminacyjna
- Service Bus Premium obsługuje VNet, geo-replikację, lepsze SLA.
- Najczęstszy błąd: brak potwierdzenia odbioru (PeekLock) lub przekroczenie TTL.
- Kolejki i topic/subscription mają osobne limity i konfiguracje.

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
