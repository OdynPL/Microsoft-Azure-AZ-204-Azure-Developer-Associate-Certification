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
- Instalacja modułu:
  `Install-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force`
- Logowanie:
  `Connect-AzAccount`
- Tworzenie grupy zasobów:
  `New-AzResourceGroup -Name myRG -Location westeurope`

## Przykład kodu PowerShell
```powershell
$rg = New-AzResourceGroup -Name "myRG" -Location "westeurope"
$vm = New-AzVM -ResourceGroupName $rg.ResourceGroupName -Name "myVM" -Location $rg.Location -Image "Win2019Datacenter"
```

## Wskazówka egzaminacyjna
- PowerShell = automatyzacja, nie runtime aplikacji.
- Najczęstszy błąd: mylenie cmdletów Az z klasycznymi AzureRM.
