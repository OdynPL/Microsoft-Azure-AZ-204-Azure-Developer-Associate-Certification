# Azure API Apps
---

[Prev: Azure Service Fabric](service-fabric.md) | [Next: Azure Logic Apps Standard vs Consumption](logic-apps-standard-vs-consumption.md)

**Definicja:**
- Usługa PaaS do hostowania API (Web API) w Azure.
- Specjalizacja App Service, z dedykowanymi funkcjami dla API.

**Znaczenie na egzaminie AZ-204:**
- Często pytania o różnice App Service vs API Apps.
- Wsparcie dla Swagger, automatyczne generowanie dokumentacji.

## Kluczowe pojęcia
- **API Apps** – dedykowane środowisko dla Web API.
- **API Definition** – integracja ze Swagger/OpenAPI.
- **Authentication/Authorization** – wsparcie dla Azure AD, OAuth2.
- **Hybrid Connections** – dostęp do zasobów on-premises.
- **Deployment slots** – środowiska testowe/produkcyjne.

**Kluczowe pojęcia dodatkowe:**
- **App Service Plan** – zasoby obliczeniowe dla API Apps.
- **Managed Identity** – dostęp do zasobów Azure bez kluczy.
- **App Settings** – konfiguracja środowiska przez portal/CLI.

## Scenariusze egzaminacyjne
- Wdrażanie Web API jako API App.
- Konfiguracja Swagger UI w portalu.
- Różnice w funkcjach względem klasycznego App Service.

## Przykład użycia
- Publikacja Web API z OpenAPI do API Apps.
- Konfiguracja autoryzacji przez Azure AD.

## Komendy
- Tworzenie API App:
  `az webapp create --resource-group rg --plan myplan --name myapiapp --runtime "DOTNET:8" --deployment-container-image-name myimage`

- Tworzenie API App przez PowerShell:
  `New-AzWebApp -ResourceGroupName rg -Name myapiapp -Location westeurope -AppServicePlan myplan -Runtime "DOTNET:8"`

## Przykład kodu C# (.NET 8)
```csharp
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
var app = builder.Build();
app.UseSwagger();
app.UseSwaggerUI();
app.MapGet("/hello", () => "Hello API App!");
app.Run();

```

```csharp
// Przykład 2: API App z autoryzacją i obsługą błędów
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

var builder = WebApplication.CreateBuilder(args);
builder.Services.AddAuthentication("Bearer").AddJwtBearer();
builder.Services.AddAuthorization();
var app = builder.Build();
app.UseAuthentication();
app.UseAuthorization();
app.MapGet("/secure", [Authorize] () => Results.Ok("Tylko autoryzowani"));
app.MapGet("/error", () => Results.Problem("Błąd API App"));
app.Run();
```

## Wskazówka egzaminacyjna
- API Apps to specjalizacja App Service – większość funkcji jest wspólna.
- Najczęstszy błąd: brak poprawnej definicji OpenAPI lub brak autoryzacji.
  - API Apps dziedziczy limity i funkcje App Service.
  - Częsty błąd: brak ustawienia App Service Plan lub Managed Identity.
