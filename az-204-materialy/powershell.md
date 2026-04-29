# Azure PowerShell
---

[Prev: Azure .NET Aspire](dotnet-aspire.md)

**Definicja:**
- **Azure PowerShell** – moduł PowerShell do zarządzania zasobami Azure z linii poleceń i skryptów.

**Znaczenie na egzaminie AZ-204:**
- Pytania o automatyzację, deployment, zarządzanie zasobami przez PowerShell.

## Kluczowe pojęcia
- **Az module** – główny moduł do pracy z Azure.
- **Cmdlet** – polecenie PowerShell (np. New-AzResourceGroup).
- **Context** – kontekst subskrypcji/logowania.

## Scenariusze egzaminacyjne
- Tworzenie zasobów przez PowerShell.
- Automatyzacja deploymentu.

## Przykład użycia
- Tworzenie grupy zasobów i VM przez PowerShell.

## Komendy

| Komenda | Zastosowanie | Kluczowe parametry |
|---------|--------------|--------------------|
| `Install-Module -Name Az` | Instalacja modułu Az | `-Scope`, `-Repository`, `-Force` |
| `Connect-AzAccount` | Logowanie do Azure | brak |
| `Set-AzContext` | Ustawienie subskrypcji/kontekstu | `-Subscription`, `-Name` |
| `New-AzResourceGroup` | Tworzenie grupy zasobów | `-Name`, `-Location` |
| `New-AzVM` | Tworzenie maszyny wirtualnej | `-ResourceGroupName`, `-Name`, `-Location`, `-Image` |
| `Get-AzResource` | Pobieranie zasobów | `-Name`, `-ResourceGroupName`, `-ResourceType` |
| `Remove-AzResourceGroup` | Usuwanie grupy zasobów | `-Name`, `-Force` |
| `New-AzStorageAccount` | Tworzenie konta storage | `-ResourceGroupName`, `-Name`, `-Location`, `-SkuName` |
| `Get-AzVM` | Pobieranie maszyn wirtualnych | `-Name`, `-ResourceGroupName` |
| `Start-AzVM` / `Stop-AzVM` | Uruchamianie/zatrzymywanie VM | `-Name`, `-ResourceGroupName` |
| `New-AzFunctionApp` | Tworzenie Function App | `-ResourceGroupName`, `-Name`, `-StorageAccountName`, `-Runtime` |
| `Get-AzWebApp` | Pobieranie App Service | `-Name`, `-ResourceGroupName` |
| `Set-AzWebApp` | Aktualizacja App Service | `-Name`, `-ResourceGroupName`, `-AppSettings` |
| `Get-AzKeyVaultSecret` | Pobieranie sekretu z Key Vault | `-VaultName`, `-Name` |
| `Set-AzKeyVaultSecret` | Dodanie/aktualizacja sekretu | `-VaultName`, `-Name`, `-SecretValue` |

## Przykład kodu PowerShell
```powershell
$rg = New-AzResourceGroup -Name "myRG" -Location "westeurope"
$vm = New-AzVM -ResourceGroupName $rg.ResourceGroupName -Name "myVM" -Location $rg.Location -Image "Win2019Datacenter"
```

## Wskazówka egzaminacyjna
- PowerShell = automatyzacja, nie runtime aplikacji.
- Najczęstszy błąd: mylenie cmdletów Az z klasycznymi AzureRM.
