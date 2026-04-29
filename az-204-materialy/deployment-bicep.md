

# Azure Deployment (ARM/Bicep)
---

[Prev: API Authorization](api-authorization.md) | [Next: Event Grid](event-grid.md)

- Automatyzacja wdrożeń zasobów Azure.
- Użycie szablonów **ARM** (JSON) lub języka **Bicep** (DSL).
- Wersjonowanie infrastruktury jako kod (**IaC**).
- Deklaratywne opisywanie infrastruktury, powtarzalność wdrożeń.

## Znaczenie na AZ-204
- Pozwala na szybkie, powtarzalne i bezpieczne wdrażanie zasobów.
- Wymagane do automatyzacji, DevOps, CI/CD.
- Umożliwia kontrolę wersji infrastruktury.

## Kluczowe pojęcia
- **ARM Template**: szablon JSON opisujący zasoby Azure.
- **Bicep**: język deklaratywny, prostszy od ARM, kompiluje się do ARM.
- **Resource**: definicja zasobu (np. storage, webapp).
- **Parameter**: parametr wejściowy szablonu.
- **Variable**: zmienna pomocnicza w szablonie.
- **Output**: wartość zwracana po wdrożeniu.
- **Module**: możliwość podziału szablonów na części.
- **What-if**: symulacja zmian przed wdrożeniem.
- **Idempotency**: wielokrotne uruchomienie daje ten sam efekt.

## Scenariusze egzaminacyjne
- Tworzenie i wdrażanie szablonów Bicep/ARM.
- Parametryzacja wdrożeń (np. nazwa, lokalizacja).
- Użycie outputs do przekazania wartości.
- Modularność i ponowne użycie kodu (module).
- What-if deployment (symulacja zmian).
- Wersjonowanie i przechowywanie szablonów w repozytorium.

## Przykład Bicep (tworzenie Storage Account)

## Przykład Bicep (tworzenie Storage Account)


```bicep
param storageName string = 'examplestorage${uniqueString(resourceGroup().id)}'

resource storage 'Microsoft.Storage/storageAccounts@2022-09-01' = {
  name: storageName
  location: resourceGroup().location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
}

output storageId string = storage.id
```


## Komendy
- Wdrażanie Bicep:
  `az deployment group create --resource-group myrg --template-file main.bicep --parameters storageName=mystorage`
- What-if deployment:
  `az deployment group what-if --resource-group myrg --template-file main.bicep`
- Kompilacja Bicep do ARM:
  `bicep build main.bicep`
- Sprawdzenie poprawności:
  `az bicep build --file main.bicep`

## Przykład ARM Template (JSON)
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
  ]
}
```

## Wskazówka egzaminacyjna
- Bicep jest preferowany na egzaminie (prostsza składnia).
- Parametry wymagają podania przez CLI lub plik .parameters.json.
- What-if nie wprowadza zmian, tylko symuluje.
- Najczęstszy błąd: brak parametru lub literówka w nazwie.
- Brak kodu C# — całość deklaratywna.

---

