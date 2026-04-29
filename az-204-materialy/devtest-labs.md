# Azure DevTest Labs
---

[Prev: Azure Automation](automation.md) | [Next: Azure Cost Management](cost-management.md)

**Definicja:**
- **Azure DevTest Labs** – środowisko do szybkiego tworzenia, zarządzania i automatyzacji VM na potrzeby testów i developmentu.

**Znaczenie na egzaminie AZ-204:**
- Pytania o ograniczanie kosztów, automatyzację środowisk testowych.

## Kluczowe pojęcia
- **Lab** – środowisko z VM, szablonami, artefaktami.
- **Artifact** – skrypt lub narzędzie instalowane na VM.
- **Policy** – limity kosztów, harmonogramy wyłączania VM.

## Scenariusze egzaminacyjne
- Automatyczne wyłączanie VM po godzinach.
- Szybkie odtwarzanie środowisk testowych.

## Przykład użycia
- Tworzenie labu i VM przez CLI.

## Komendy
- Tworzenie labu:
  `az lab create --resource-group myRG --name mylab --location westeurope`
- Tworzenie VM:
  `az lab vm create --lab-name mylab --name myvm --image UbuntuLTS --size Standard_DS1_v2 --resource-group myRG`

## Przykład kodu C# (.NET 8)
```csharp
// Brak SDK do zarządzania labami w runtime aplikacji. Operacje przez CLI/portal.
```

## Wskazówka egzaminacyjna
- DevTest Labs = optymalizacja kosztów testów.
- Najczęstszy błąd: mylenie z klasycznymi VM lub Azure Automation.
