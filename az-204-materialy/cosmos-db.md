# Azure Cosmos DB

- Globalnie rozproszona baza NoSQL.
- Obsługuje wiele modeli: dokumenty, klucz-wartość, grafy.
- Skalowanie i replikacja automatyczna.

## Przykład C# (.NET 8, dodanie dokumentu)

```csharp
public async Task AddItemAsync<T>(CosmosClient client, string db, string container, T item)
{
    var cont = client.GetDatabase(db).GetContainer(container);
    await cont.CreateItemAsync(item);
}
```

- Użycie Microsoft.Azure.Cosmos.
- Async/await.
- Przekazanie dowolnego obiektu.

---

[Prev: Blob Storage](blob-storage.md) | [Next: Deployment (Bicep)](deployment-bicep.md)
