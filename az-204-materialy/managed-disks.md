# Azure Managed Disks
---

[Prev: API Versioning](api-versioning.md) | [Next: Azure Files](files.md)

**Definicja:**
- **Azure Managed Disks** – zarządzane dyski blokowe dla VM, skalowalne, z backupem i snapshotami.

**Znaczenie na egzaminie AZ-204:**
- Pytania o typy dysków, snapshoty, bezpieczeństwo danych.

## Kluczowe pojęcia
- **Standard HDD/S, Premium SSD, Ultra Disk** – typy dysków.
- **Snapshot** – kopia dysku w danym momencie.
- **Encryption** – szyfrowanie danych w spoczynku.
- **Managed** – Azure zarządza storage, nie użytkownik.

## Scenariusze egzaminacyjne
- Tworzenie VM z określonym typem dysku.
- Tworzenie snapshotu dysku.

## Przykład użycia
- Tworzenie dysku i snapshotu przez CLI.

## Komendy
- Tworzenie dysku:
  `az disk create --resource-group myRG --name myDisk --size-gb 128 --sku Premium_LRS`
- Tworzenie snapshotu:
  `az snapshot create --resource-group myRG --source myDisk --name mySnapshot`

## Przykład kodu C# (.NET 8)
```csharp
// Brak SDK do zarządzania dyskami w runtime aplikacji. Operacje na poziomie infrastruktury.
```

## Wskazówka egzaminacyjna
- Managed Disks ≠ klasyczny storage account.
- Najczęstszy błąd: mylenie typów dysków i ich przeznaczenia.
