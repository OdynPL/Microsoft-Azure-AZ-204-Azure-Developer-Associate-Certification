

# Azure App Configuration
---

[Prev: App Service](app-service.md) | [Next: API Management](api-management.md)

## Definicja
- Centralne miejsce do zarządzania konfiguracją aplikacji i flagami funkcji (**feature flags**).
- Przechowywanie kluczy, wartości, feature flags, etykiet środowiskowych (**labels**).
- Umożliwia wersjonowanie i audyt zmian konfiguracji.

## Znaczenie na AZ-204
- Ułatwia zarządzanie konfiguracją w wielu środowiskach (dev, test, prod).
- Pozwala na dynamiczne włączanie/wyłączanie funkcji (**feature flags**).
- Oddziela konfigurację od kodu, wspiera DevOps.
- Umożliwia centralne zarządzanie connection stringami i ustawieniami.

## Kluczowe pojęcia
- **Key-Value**: para klucz-wartość, np. connection string, endpoint, ustawienie aplikacji.
- **Label**: etykieta środowiska (dev, prod, test), pozwala na rozdzielenie konfiguracji.
- **Feature Flag**: przełącznik funkcji, sterowanie zachowaniem aplikacji bez zmiany kodu.
- **Revision**: wersjonowanie konfiguracji, historia zmian.
- **Content Type**: typ danych przechowywanych w kluczu (np. application/json).
- **Locked**: klucz zablokowany przed modyfikacją.
- **Purge Protection**: ochrona przed trwałym usunięciem.
- **Provider**: integracja z .NET przez Microsoft.Extensions.Configuration.AzureAppConfiguration.
- **Dynamic Refresh**: automatyczne odświeżanie konfiguracji bez restartu aplikacji.

## Scenariusze egzaminacyjne
- Pobieranie konfiguracji z App Configuration w .NET 8 (Web API, Functions).
- Użycie feature flags do sterowania funkcjami (np. rollout nowej funkcji).
- Oddzielanie konfiguracji od kodu, zarządzanie środowiskami.
- Dynamiczne odświeżanie ustawień w aplikacji.
- Wersjonowanie i audyt zmian konfiguracji.
- Integracja z Key Vault do pobierania tajnych danych.

## Przykład użycia
- Dynamiczne przełączanie funkcji przez feature flag (np. beta feature dla wybranych użytkowników).
- Centralne zarządzanie connection stringami i endpointami.
- Odświeżanie konfiguracji bez restartu aplikacji.

## Komendy
- Tworzenie App Configuration:
    `az appconfig create --name myappconfig --resource-group rg --location westeurope`
- Dodanie klucza:
    `az appconfig kv set --name myappconfig --key MyKey --value MyValue --label prod`
- Dodanie feature flag:
    `az appconfig feature set --name myappconfig --feature betaFeature --label prod --yes`
- Wyświetlenie historii zmian:
    `az appconfig revision list --name myappconfig --key MyKey`

## Przykład kodu C# (.NET 8)
```csharp
using Azure.Identity;
using Microsoft.Extensions.Configuration;

var builder = WebApplication.CreateBuilder(args);

builder.Configuration.AddAzureAppConfiguration(options =>
{
    options.Connect(Environment.GetEnvironmentVariable("AppConfigConnectionString"))
       .UseFeatureFlags()
       .ConfigureRefresh(refresh =>
       {
           refresh.Register("MyKey", refreshAll: true)
              .SetCacheExpiration(TimeSpan.FromSeconds(30));
       });
});

var app = builder.Build();
// ...
```

## Wskazówka egzaminacyjna
- **Feature flags** mogą być odświeżane bez restartu aplikacji.
- Klucze mogą mieć etykiety środowiskowe (**labels**).
- App Configuration nie przechowuje tajnych danych (do tego **Key Vault**).
- Najczęstszy błąd: brak odświeżania konfiguracji lub nieprawidłowa etykieta.
- Feature flags nie są mechanizmem bezpieczeństwa, tylko sterowania logiką.


---

