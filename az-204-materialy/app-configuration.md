# Azure App Configuration

- Centralne zarządzanie konfiguracją aplikacji.
- Przechowywanie kluczy, wartości, feature flags.
- Integracja z .NET przez SDK.

## Przykład C# (.NET 8, pobranie wartości)

```csharp
public void ConfigureAppConfiguration(IConfigurationBuilder builder, string connectionString)
{
    builder.AddAzureAppConfiguration(connectionString);
}
```

- Użycie Microsoft.Extensions.Configuration.AzureAppConfiguration.
- Dodanie do konfiguracji aplikacji.

---

[Prev: App Service](app-service.md) | [Next: API Management](api-management.md)
