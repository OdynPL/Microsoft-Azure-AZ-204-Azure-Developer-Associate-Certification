# Azure Storage Queue

- Prosta kolejka do przechowywania i przesyłania komunikatów.
- FIFO, niskie koszty, integracja z Functions.

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
