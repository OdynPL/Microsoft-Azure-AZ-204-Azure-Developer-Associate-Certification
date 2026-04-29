# Azure Table Storage

- Prosta baza NoSQL (klucz-wartość).
- Przechowywanie dużych ilości danych tabelarycznych.
- Szybki dostęp do danych przez klucz partycji i wiersza.

## Przykład C# (.NET 8, dodanie rekordu)

```csharp
public async Task AddEntityAsync<T>(string connectionString, string tableName, T entity) where T : class, ITableEntity, new()
{
    var client = new TableClient(connectionString, tableName);
    await client.AddEntityAsync(entity);
}
```

- Użycie Azure.Data.Tables.
- Async/await.
- Przekazanie obiektu implementującego ITableEntity.

---

[Prev: Storage Queue](storage-queue.md) | [Next: Web PubSub](webpubsub.md)
