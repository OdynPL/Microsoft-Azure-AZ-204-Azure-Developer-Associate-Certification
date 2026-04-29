# Azure Blob Storage

- Przechowywanie dużych ilości danych nieustrukturyzowanych.
- Dostęp przez REST API, SDK.
- Wspiera wersjonowanie, szyfrowanie, backup.

## Przykład C# (.NET 8, upload pliku)

```csharp
public async Task UploadBlobAsync(string connectionString, string container, string filePath)
{
    var client = new BlobContainerClient(connectionString, container);
    var blob = client.GetBlobClient(Path.GetFileName(filePath));
    await blob.UploadAsync(filePath, overwrite: true);
}
```

- Użycie Azure.Storage.Blobs.
- Async/await.
- Przekazanie ścieżki do pliku.

---

[Prev: CDN](cdn.md) | [Next: Cosmos DB](cosmos-db.md)
