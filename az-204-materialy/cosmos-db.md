
# Azure Cosmos DB

## Definicja
- Globalnie rozproszona baza NoSQL.
- Obsługuje modele: dokumenty, klucz-wartość, grafy, kolumnowy.

## Znaczenie na AZ-204
- Wysoka dostępność, niskie opóźnienia, automatyczne skalowanie.
- Wybór dla aplikacji globalnych, IoT, systemów o dużej dostępności.

## Kluczowe pojęcia
- **Container**: logiczna kolekcja dokumentów.
- **Partition Key**: klucz partycjonowania, wpływa na wydajność.
- **RU/s**: jednostki Request Units, model rozliczania wydajności.
- **Consistency Level**: 5 poziomów spójności (np. Session, Strong).
- **Global Distribution**: replikacja do wielu regionów.
- TTL, indeksowanie, multi-master.

## Scenariusze egzaminacyjne
- Tworzenie kontenera z kluczem partycji.
- Dodawanie i pobieranie dokumentów.
- Ustawianie poziomu spójności.
- Skalowanie RU/s, globalna replikacja.

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

## Wskazówka egzaminacyjna
- Zły wybór Partition Key = słaba wydajność.
- RU/s = koszt, throttling przy przekroczeniu.
- Domyślny poziom spójności: Session.


---

[Prev: Blob Storage](blob-storage.md) | [Next: Deployment (Bicep)](deployment-bicep.md)
