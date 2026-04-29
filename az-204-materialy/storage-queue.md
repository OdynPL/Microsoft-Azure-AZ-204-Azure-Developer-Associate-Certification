
# Azure Storage Queue

- Prosta kolejka do przechowywania i przesyłania komunikatów (FIFO).
- Niskie koszty, wysoka dostępność, integracja z Functions, Logic Apps.
- Odpowiednia do prostych scenariuszy kolejkowania, buforowania zadań.

## Znaczenie na AZ-204
- Umożliwia asynchroniczną komunikację między komponentami.
- Pozwala na buforowanie zadań, skalowanie przetwarzania.
- Integracja z Functions (QueueTrigger), automatyczne skalowanie.

## Kluczowe pojęcia
- **Queue**: kolejka komunikatów (FIFO).
- **Message**: pojedynczy komunikat (do 64 KB).
- **Visibility Timeout**: czas ukrycia komunikatu po pobraniu.
- **Poison Message**: komunikat nieprzetworzony po wielu próbach.
- **Dequeue Count**: liczba pobrań komunikatu.
- **Base64 Encoding**: domyślne kodowanie wiadomości.
- **SAS Token**: uwierzytelnianie do kolejki przez token.

## Scenariusze egzaminacyjne
- Wysyłanie i odbieranie komunikatów przez .NET 8.
- Integracja z Azure Functions (QueueTrigger).
- Obsługa poison messages.
- Ustawienie visibility timeout.

## Przykład użycia
- Wysyłanie komunikatu do kolejki przez .NET 8.
- Odbiór komunikatu przez Azure Function.
- Obsługa komunikatu nieprzetworzonego (poison message).

## Komendy
- Tworzenie kolejki:
    `az storage queue create --name myqueue --account-name mystorage`
- Wysyłanie komunikatu:
    `az storage message put --queue-name myqueue --account-name mystorage --content "Hello"`
- Pobranie komunikatu:
    `az storage message get --queue-name myqueue --account-name mystorage`

## Przykład C# (.NET 8, wysyłanie i odbieranie wiadomości)
```csharp
using Azure.Storage.Queues;

// Wysyłanie
public async Task SendQueueMessageAsync(string connectionString, string queueName, string message)
{
        var client = new QueueClient(connectionString, queueName);
        await client.CreateIfNotExistsAsync();
        await client.SendMessageAsync(message);
}

// Odbiór
public async Task<string> ReceiveQueueMessageAsync(string connectionString, string queueName)
{
        var client = new QueueClient(connectionString, queueName);
        var response = await client.ReceiveMessageAsync();
        return response.Value?.MessageText;
}
```

// Odbiór przez Azure Function:
```csharp
[Function("QueueHandler")]
public void Run([QueueTrigger("myqueue")] string message, FunctionContext context)
{
        var logger = context.GetLogger("QueueHandler");
        logger.LogInformation($"Odebrano: {message}");
}
```

## Wskazówka egzaminacyjna
- Storage Queue nie obsługuje transakcji ani ordering gwarantowanego przy dużym obciążeniu.
- Najczęstszy błąd: przekroczenie limitu rozmiaru wiadomości lub brak obsługi poison messages.
- Visibility timeout powinien być dostosowany do czasu przetwarzania zadania.

## Przykład C# (.NET 8, wysyłanie wiadomości)

```csharp
public async Task SendQueueMessageAsync(string connectionString, string queueName, string message)
{
    var client = new QueueClient(connectionString, queueName);
    await client.CreateIfNotExistsAsync();
    await client.SendMessageAsync(message);
}
```

- Użycie Azure.Storage.Queues.
- Async/await.
- Tworzenie kolejki jeśli nie istnieje.

---

[Prev: SQL Database](sql-database.md) | [Next: Table Storage](table-storage.md)
