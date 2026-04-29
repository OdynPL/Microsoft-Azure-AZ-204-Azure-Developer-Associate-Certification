# Azure Files
---

[Prev: Azure Managed Disks](managed-disks.md) | [Next: Azure Automation](automation.md)

**Definicja:**
- **Azure Files** – udostępnianie udziałów plikowych SMB/NFS w chmurze.

**Znaczenie na egzaminie AZ-204:**
- Pytania o montowanie udziałów, uprawnienia, integrację z AD.

## Kluczowe pojęcia
- **SMB/NFS** – protokoły udostępniania plików.
- **File Share** – udział plikowy.
- **Snapshot** – kopia udziału.
- **Private Endpoint** – prywatny dostęp do udziału.

## Scenariusze egzaminacyjne
- Montowanie udziału w VM lub kontenerze.
- Ograniczenie dostępu przez Private Endpoint.

## Przykład użycia
- Tworzenie udziału i montowanie przez CLI.

## Komendy
- Tworzenie udziału:
  `az storage share create --account-name mystorage --name myshare`
- Pobranie klucza:
  `az storage account keys list --account-name mystorage`

## Przykład kodu C# (.NET 8)
```csharp
var serviceClient = new ShareServiceClient(connectionString);
var shareClient = serviceClient.GetShareClient("myshare");
await shareClient.CreateIfNotExistsAsync();
```

```csharp
// Upload pliku do Azure Files
public async Task UploadFileAsync(string connectionString, string shareName, string filePath)
{
  var shareClient = new ShareClient(connectionString, shareName);
  var dirClient = shareClient.GetRootDirectoryClient();
  var fileClient = dirClient.GetFileClient(Path.GetFileName(filePath));
  await fileClient.CreateAsync(new FileInfo(filePath).Length);
  using var stream = File.OpenRead(filePath);
  await fileClient.UploadRangeAsync(new HttpRange(0, stream.Length), stream);
}

// Pobieranie pliku z Azure Files
public async Task DownloadFileAsync(string connectionString, string shareName, string fileName, string downloadPath)
{
  var shareClient = new ShareClient(connectionString, shareName);
  var dirClient = shareClient.GetRootDirectoryClient();
  var fileClient = dirClient.GetFileClient(fileName);
  var response = await fileClient.DownloadAsync();
  using var fs = File.Create(downloadPath);
  await response.Value.Content.CopyToAsync(fs);
}

// Listowanie plików w udziale
public async Task<List<string>> ListFilesAsync(string connectionString, string shareName)
{
  var shareClient = new ShareClient(connectionString, shareName);
  var dirClient = shareClient.GetRootDirectoryClient();
  var result = new List<string>();
  await foreach (var item in dirClient.GetFilesAndDirectoriesAsync())
  {
    if (!item.IsDirectory)
      result.Add(item.Name);
  }
  return result;
}

// Usuwanie pliku
public async Task DeleteFileAsync(string connectionString, string shareName, string fileName)
{
  var shareClient = new ShareClient(connectionString, shareName);
  var dirClient = shareClient.GetRootDirectoryClient();
  var fileClient = dirClient.GetFileClient(fileName);
  await fileClient.DeleteIfExistsAsync();
}
```

## Wskazówka egzaminacyjna
- Azure Files ≠ Blob Storage (Files = SMB/NFS, Blob = REST API).
- Najczęstszy błąd: mylenie uprawnień i sposobu montowania.
