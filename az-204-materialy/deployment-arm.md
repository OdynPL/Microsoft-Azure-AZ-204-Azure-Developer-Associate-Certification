
# Azure Deployment (ARM)
---

[Prev: Debugowanie aplikacji w Azure](debugowanie.md) | [Next: Deployment (Bicep)](deployment-bicep.md)

- Automatyzacja wdrożeń zasobów Azure za pomocą szablonów ARM (JSON).
- Wersjonowanie infrastruktury jako kod (**IaC**).
- Deklaratywne opisywanie infrastruktury, powtarzalność wdrożeń.

## Znaczenie na AZ-204
- Pozwala na szybkie, powtarzalne i bezpieczne wdrażanie zasobów.
- Wymagane do automatyzacji, DevOps, CI/CD.
- Umożliwia kontrolę wersji infrastruktury.

## Kluczowe pojęcia
- **ARM Template**: szablon JSON opisujący zasoby Azure.
- **Resource**: definicja zasobu (np. storage, webapp).
- **Parameter**: parametr wejściowy szablonu.
- **Variable**: zmienna pomocnicza w szablonie.
- **Output**: wartość zwracana po wdrożeniu.
- **What-if**: symulacja zmian przed wdrożeniem.
- **Idempotency**: wielokrotne uruchomienie daje ten sam efekt.

## Scenariusze egzaminacyjne
- Tworzenie i wdrażanie szablonów ARM.
- Parametryzacja wdrożeń (np. nazwa, lokalizacja).
- Użycie outputs do przekazania wartości.
- What-if deployment (symulacja zmian).
- Wersjonowanie i przechowywanie szablonów w repozytorium.

## Przykład ARM Template (tworzenie Storage Account)
```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": { "type": "string" }
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2022-09-01",
      "name": "[parameters('storageName')]",
      "location": "[resourceGroup().location]",
      "sku": { "name": "Standard_LRS" },
      "kind": "StorageV2"
    }
  ],
  "outputs": {
    "storageId": {
      "type": "string",
      "value": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageName'))]"
    }
  }
}
```

## Komendy
- Wdrażanie ARM:
  `az deployment group create --resource-group myrg --template-file main.json --parameters storageName=mystorage`
- What-if deployment:
  `az deployment group what-if --resource-group myrg --template-file main.json`

## Wskazówka egzaminacyjna
- ARM wymaga poprawnej składni JSON i zgodności z API version.
- Parametry wymagają podania przez CLI lub plik .parameters.json.
- What-if nie wprowadza zmian, tylko symuluje.
- Najczęstszy błąd: brak parametru lub literówka w nazwie.
- Brak kodu C# — całość deklaratywna.
