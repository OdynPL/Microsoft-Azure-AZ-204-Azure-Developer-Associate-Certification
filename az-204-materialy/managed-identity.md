# Azure Managed Identity

- Automatyczne zarządzanie tożsamością dla zasobów Azure.
- Umożliwia uwierzytelnianie bez przechowywania haseł.
- Integracja z Key Vault, Storage, SQL itp.

## Przykład C# (.NET 8, użycie DefaultAzureCredential)

```csharp
var credential = new DefaultAzureCredential();
```

- Użycie Azure.Identity.
- Brak konieczności podawania loginu/hasła.

---

[Prev: Logic Apps](logic-apps.md) | [Next: Monitor](monitor.md)
