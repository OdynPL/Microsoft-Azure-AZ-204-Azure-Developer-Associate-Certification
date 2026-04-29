

# Azure Cosmos DB
---

[Prev: Blob Storage](blob-storage.md) | [Next: Deployment (Bicep)](deployment-bicep.md)

## Definicja
- **Azure Cosmos DB** to globalnie rozproszona, w pełni zarządzana baza NoSQL.
- Obsługuje modele: dokumenty (SQL API), klucz-wartość (Table API), grafy (Gremlin API), kolumnowy (Cassandra API).
- Zapewnia niskie opóźnienia (<10 ms), wysoką dostępność (99,999%), automatyczne skalowanie i globalną replikację.

## Znaczenie na AZ-204
- Wysoka dostępność, niskie opóźnienia, automatyczne skalowanie.
- Wybór dla aplikacji globalnych, IoT, systemów o dużej dostępności.

## Kluczowe pojęcia
- **Container**: logiczna kolekcja dokumentów.
- **Partition Key**: klucz partycjonowania, wpływa na wydajność.
- **RU/s**: jednostki Request Units, model rozliczania wydajności.
- **Consistency Level**: 5 poziomów spójności (np. Session, Strong).
- **Global Distribution**: replikacja do wielu regionów.
- **TTL**: automatyczne usuwanie dokumentów po czasie.
- **Indeksowanie**: automatyczne, można dostosować dla wydajności.
- **Multi-master**: zapis w wielu regionach jednocześnie.

## Scenariusze egzaminacyjne
- Tworzenie kontenera z kluczem partycji.
- Dodawanie i pobieranie dokumentów.
- Ustawianie poziomu spójności.
- Skalowanie RU/s, globalna replikacja.
- Zapytania SQL, paginacja wyników.
- TTL i indeksowanie.

## Przykład użycia
- Dodanie dokumentu do kontenera.
- Pobranie dokumentu po id i partycji.

## Komendy
- Tworzenie bazy:
    `az cosmosdb create --name mycosmos --resource-group rg --kind GlobalDocumentDB`
- Tworzenie kontenera:
    `az cosmosdb sql container create --account-name mycosmos --database-name db --name cont --partition-key-path /userId --throughput 400`

## Przykład kodu C# (.NET 8)
```csharp
public async Task AddItemAsync<T>(CosmosClient client, string db, string container, T item)
{
        var cont = client.GetDatabase(db).GetContainer(container);
        try
        {
                await cont.CreateItemAsync(item);
        }
        catch (CosmosException ex)
        {
                // Obsługa błędów: 404, 429 (throttling), 409 (duplikat)
                throw;
        }
}
```

```csharp
// Pobieranie dokumentu po id i partycji
public async Task<T> GetItemAsync<T>(CosmosClient client, string db, string container, string id, string partitionKey)
{
        var cont = client.GetDatabase(db).GetContainer(container);
        try
        {
                var response = await cont.ReadItemAsync<T>(id, new PartitionKey(partitionKey));
                return response.Resource;
        }
        catch (CosmosException ex)
        {
                // Obsługa błędów: 404 (not found)
                throw;
        }
}

// Aktualizacja dokumentu
public async Task UpdateItemAsync<T>(CosmosClient client, string db, string container, string id, T item)
{
        var cont = client.GetDatabase(db).GetContainer(container);
        await cont.ReplaceItemAsync(item, id);
}

// Usuwanie dokumentu
public async Task DeleteItemAsync(CosmosClient client, string db, string container, string id, string partitionKey)
{
        var cont = client.GetDatabase(db).GetContainer(container);
        await cont.DeleteItemAsync<object>(id, new PartitionKey(partitionKey));
}

// Zapytanie SQL i paginacja
public async Task<List<T>> QueryItemsAsync<T>(CosmosClient client, string db, string container, string sql)
{
        var cont = client.GetDatabase(db).GetContainer(container);
        var query = cont.GetItemQueryIterator<T>(sql);
        var results = new List<T>();
        while (query.HasMoreResults)
        {
                var response = await query.ReadNextAsync();
                results.AddRange(response);
        }
        return results;
}

// Ustawienie TTL dla kontenera (przykład CLI)
// az cosmosdb sql container update --account-name mycosmos --database-name db --name cont --ttl 3600

// Przykład indeksowania (fragment definicji kontenera)
// new ContainerProperties("cont", "/userId") { IndexingPolicy = new IndexingPolicy { Automatic = true, IndexingMode = IndexingMode.Consistent } }
```

## Wskazówka egzaminacyjna
- Zły wybór Partition Key = słaba wydajność.
- RU/s = koszt, throttling przy przekroczeniu.
- Domyślny poziom spójności: Session.
- TTL pozwala automatycznie usuwać stare dane.
- Indeksowanie można wyłączyć dla dużych kolekcji z rzadkimi zapytaniami.
- Paginacja przez continuation token lub iterator.


---

