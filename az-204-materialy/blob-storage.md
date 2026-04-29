

# Azure Blob Storage
---

[Prev: CDN](cdn.md) | [Next: Cosmos DB](cosmos-db.md)

## Definicja
- Przechowywanie dużych ilości danych nieustrukturyzowanych (pliki, obrazy, backupy).
- Dostęp przez REST API, SDK, Azure Portal.

## Znaczenie na AZ-204
- Najczęściej używany storage do plików w aplikacjach chmurowych.
- Integracja z Functions, Logic Apps, App Service.

## Kluczowe pojęcia
- **Container**: logiczna grupa blobów.
- **Blob**: pojedynczy plik (Block, Append, Page).
- **Access Tier**: Hot, Cool, Archive.
- **SAS Token**: bezpieczny dostęp tymczasowy.
- **Blob Trigger**: wyzwalacz dla Functions.
- Wersjonowanie, soft delete, lifecycle management.

## Scenariusze egzaminacyjne
- Upload/download plików przez SDK.
- Udostępnianie plików przez SAS.
- Automatyczne przetwarzanie plików (np. Functions po uploadzie).
- Zarządzanie dostępem (RBAC, SAS, Access Policy).

## Przykład użycia
- Upload pliku przez SDK.
- Generowanie SAS do pobrania pliku.

## Komendy
- Tworzenie kontenera:
    `az storage container create --account-name mystorage --name mycontainer`
- Generowanie SAS:
    `az storage blob generate-sas --account-name mystorage --container-name mycontainer --name file.txt --permissions r --expiry 2026-12-31 --https-only`

## Przykład kodu C# (.NET 8)
```csharp
public async Task UploadBlobAsync(string connectionString, string container, string filePath)
{
        var client = new BlobContainerClient(connectionString, container);
        var blob = client.GetBlobClient(Path.GetFileName(filePath));
        try
        {
                await blob.UploadAsync(filePath, overwrite: true);
        }
        catch (RequestFailedException ex)
        {
                // Obsługa błędów dostępu, quota, itp.
                throw;
        }
}
```

```csharp
// Pobieranie pliku z Blob Storage
public async Task DownloadBlobAsync(string connectionString, string container, string blobName, string downloadPath)
{
        var client = new BlobContainerClient(connectionString, container);
        var blob = client.GetBlobClient(blobName);
        await blob.DownloadToAsync(downloadPath);
}

// Generowanie SAS dla bloba
public string GetBlobSasUri(string connectionString, string container, string blobName)
{
        var client = new BlobContainerClient(connectionString, container);
        var blob = client.GetBlobClient(blobName);
        var sas = blob.GenerateSasUri(Azure.Storage.Sas.BlobSasPermissions.Read, DateTimeOffset.UtcNow.AddHours(1));
        return sas.ToString();
}

// Usuwanie bloba
public async Task DeleteBlobAsync(string connectionString, string container, string blobName)
{
        var client = new BlobContainerClient(connectionString, container);
        var blob = client.GetBlobClient(blobName);
        await blob.DeleteIfExistsAsync();
}

// Listowanie blobów w kontenerze
public async Task<List<string>> ListBlobsAsync(string connectionString, string container)
{
        var client = new BlobContainerClient(connectionString, container);
        var result = new List<string>();
        await foreach (var blob in client.GetBlobsAsync())
        {
                result.Add(blob.Name);
        }
        return result;
}
```

## Wskazówka egzaminacyjna
- SAS Token wygasa, nie nadaje uprawnień na stałe.
- Access Tier wpływa na koszty i czas dostępu.
- RBAC dotyczy konta storage, nie pojedynczych blobów.


---

