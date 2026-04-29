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

## Wskazówka egzaminacyjna
- Azure Files ≠ Blob Storage (Files = SMB/NFS, Blob = REST API).
- Najczęstszy błąd: mylenie uprawnień i sposobu montowania.
