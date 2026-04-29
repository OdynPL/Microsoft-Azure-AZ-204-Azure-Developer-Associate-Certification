# Azure Deployment (ARM/Bicep)

- Automatyzacja wdrożeń zasobów Azure.
- Użycie szablonów ARM lub języka Bicep.
- Wersjonowanie infrastruktury jako kod.

## Przykład Bicep (tworzenie Storage Account)

```bicep
resource storage 'Microsoft.Storage/storageAccounts@2022-09-01' = {
  name: 'examplestorage${uniqueString(resourceGroup().id)}'
  location: resourceGroup().location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
}
```

- Plik .bicep wdrażany przez Azure CLI lub portal.
- Brak kodu C#.

---

[Prev: API Authorization](api-authorization.md) | [Next: Event Grid](event-grid.md)
