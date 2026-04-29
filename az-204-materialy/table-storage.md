

# Azure Table Storage
---

[Prev: Storage Queue](storage-queue.md) | [Next: Web PubSub](webpubsub.md)

- Prosta baza NoSQL (klucz-wartość, schemat elastyczny).
- Przechowywanie dużych ilości danych tabelarycznych, logów, metadanych.
- Szybki dostęp do danych przez klucz partycji (PartitionKey) i wiersza (RowKey).

## Znaczenie na AZ-204
- Umożliwia tanie i skalowalne przechowywanie danych nienormowanych.
- Odpowiednia do logów, metadanych, danych telemetrycznych.
- Integracja z Functions, App Service, Storage Explorer.

## Kluczowe pojęcia
- **Table**: kolekcja encji (wierszy).
- **Entity**: pojedynczy rekord (obiekt).
- **PartitionKey**: klucz partycji, grupuje encje dla wydajności.
- **RowKey**: unikalny identyfikator w partycji.
- **ETag**: wersjonowanie encji, obsługa konkurencji.
- **Batch Operation**: operacje na wielu encjach w jednej partycji.
- **OData**: zapytania filtrowane po polach.
- **SAS Token**: uwierzytelnianie do tabeli przez token.

## Scenariusze egzaminacyjne
- Dodawanie, pobieranie, usuwanie encji przez .NET 8.
- Filtrowanie danych po PartitionKey, RowKey.
- Operacje batch (w obrębie jednej partycji).
- Integracja z Functions (Table input/output binding).

## Przykład użycia
- Dodanie encji przez Azure.Data.Tables.
- Pobranie encji po kluczu.
- Operacja batch na wielu encjach.

## Komendy
- Tworzenie tabeli:
    `az storage table create --name mytable --account-name mystorage`
- Dodanie encji:
    `az storage entity insert --entity PartitionKey=part1 RowKey=row1 Name=Adam --table-name mytable --account-name mystorage`
- Pobranie encji:
    `az storage entity show --table-name mytable --account-name mystorage --partition-key part1 --row-key row1`

## Przykład C# (.NET 8, dodanie i pobranie rekordu)
```csharp
using Azure.Data.Tables;

public async Task AddEntityAsync<T>(string connectionString, string tableName, T entity) where T : class, ITableEntity, new()
{
        var client = new TableClient(connectionString, tableName);
        await client.AddEntityAsync(entity);
}

public async Task<T> GetEntityAsync<T>(string connectionString, string tableName, string partitionKey, string rowKey) where T : class, ITableEntity, new()
{
        var client = new TableClient(connectionString, tableName);
        var response = await client.GetEntityAsync<T>(partitionKey, rowKey);
        return response.Value;
}
```

// Binding w Azure Functions:
```csharp
[Function("TableReader")]
public void Run([TableInput("mytable", "PartitionKey eq 'part1'")] MyEntity[] entities, FunctionContext context)
{
        var logger = context.GetLogger("TableReader");
        logger.LogInformation($"Liczba encji: {entities.Length}");
}
```

## Wskazówka egzaminacyjna
- Table Storage nie obsługuje transakcji między partycjami.
- Najczęstszy błąd: brak PartitionKey/RowKey lub przekroczenie limitu batch.
- OData pozwala na filtrowanie, ale nie na złożone zapytania SQL.

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

