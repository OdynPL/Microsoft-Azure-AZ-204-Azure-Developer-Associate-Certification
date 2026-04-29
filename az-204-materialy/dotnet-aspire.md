# Azure .NET Aspire
---

[Prev: Azure Marketplace](marketplace.md) | [Next: Azure PowerShell](powershell.md)

**Definicja:**
- **Azure .NET Aspire** – narzędzia i szablony do budowy nowoczesnych aplikacji cloud-native w .NET 8 na Azure.

**Znaczenie na egzaminie AZ-204:**
- Pytania o integrację .NET z usługami Azure, deployment, monitoring.

## Kluczowe pojęcia
- **Aspire Dashboard** – monitoring i zarządzanie aplikacją.
- **Aspire Components** – gotowe integracje z usługami Azure (np. Storage, Service Bus).
- **Aspire Orchestrator** – zarządzanie cyklem życia aplikacji.

## Scenariusze egzaminacyjne
- Tworzenie aplikacji cloud-native z .NET 8.
- Integracja z Azure Storage, Service Bus, Key Vault.

## Przykład użycia
- Tworzenie projektu Aspire przez CLI.

## Komendy
- Instalacja Aspire:
  `dotnet new install Microsoft.Aspire.Templates`
- Tworzenie projektu:
  `dotnet new aspire-app -n MyAspireApp`

## Przykład kodu C# (.NET 8)
```csharp
var builder = DistributedApplication.CreateBuilder(args);
builder.AddAzureStorage("mystorage");
builder.AddAzureServiceBus("mybus");
var app = builder.Build();
app.Run();
```

## Wskazówka egzaminacyjna
- Aspire = szybki start cloud-native, integracja z Azure.
- Najczęstszy błąd: mylenie Aspire z klasycznym Web API.
