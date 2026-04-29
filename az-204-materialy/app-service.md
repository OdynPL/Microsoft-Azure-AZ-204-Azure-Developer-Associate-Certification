

# Azure App Service
---

[Prev: Application Insights](application-insights.md) | [Next: App Configuration](app-configuration.md)

## Definicja
- Usługa **PaaS** do hostowania aplikacji webowych i API.
- Obsługuje .NET, Java, Node.js, Python, PHP, Ruby, Go.
- Umożliwia szybkie wdrażanie, skalowanie i zarządzanie aplikacjami.

## Znaczenie na AZ-204
- Najczęściej wybierana platforma do hostowania aplikacji biznesowych.
- Wsparcie dla automatycznego skalowania, deploymentu, SSL, backupu.
- Integracja z Key Vault, Application Insights, Azure AD.
- Obsługa deployment slots, blue-green deployment.
- Możliwość konfiguracji custom domains, certyfikatów SSL.

## Kluczowe pojęcia
- **Plan App Service**: Free, Shared, Basic, Standard, Premium, Isolated; określa zasoby i funkcje.
- **Deployment slots**: środowiska (np. staging, production), swap bez przestoju.
- **Skalowanie poziome** (więcej instancji) i **pionowe** (większa maszyna).
- **Always On**: utrzymuje aplikację aktywną (tylko od Standard).
- **Custom domains**: własne domeny, certyfikaty SSL.
- **App Settings**: zmienne środowiskowe, connection strings.
- **Managed Identity**: dostęp do innych usług bez hasła.
- **Hybrid Connections**: dostęp do zasobów on-premises.
- **Diagnostic logs**: logi aplikacji, logi serwera, streaming logów.
- **Auto Heal**: automatyczne restartowanie przy błędach.
- **Scale out/in**: automatyczne zwiększanie/zmniejszanie liczby instancji.
- **CI/CD**: integracja z GitHub Actions, Azure DevOps, Bitbucket.

**Kluczowe pojęcia dodatkowe:**
- **Slot-specific settings** – ustawienia przypisane do slotu, nie kopiowane przy swap.
- **Outbound IP addresses** – adresy wychodzące App Service.

## Scenariusze egzaminacyjne
- Wdrażanie aplikacji .NET/Node.js/Python przez portal, CLI, CI/CD.
- Konfiguracja deployment slots i swap (np. blue-green deployment).
- Ustawienia autoskalowania (CPU, RAM, harmonogram).
- Integracja z Key Vault (sekrety), Application Insights (monitoring).
- Konfiguracja custom domains i certyfikatów SSL.
- Ustawienia App Settings i connection strings.
- Włączenie Always On.
- Użycie Managed Identity do dostępu do innych usług.

## Przykład użycia
- Minimal API .NET 8.
- Swap slotów po wdrożeniu (staging -> production).
- Ustawienie App Settings przez portal lub CLI.
- Włączenie Always On.

## Komendy
- Tworzenie App Service:
	`az webapp create --resource-group rg --plan myplan --name myapp --runtime "DOTNET:8"`
- Dodanie slotu:
	`az webapp deployment slot create --resource-group rg --name myapp --slot staging`
- Swap slotów:
	`az webapp deployment slot swap --resource-group rg --name myapp --slot staging --target-slot production`
- Ustawienie App Settings:
	`az webapp config appsettings set --resource-group rg --name myapp --settings Key=Value`

- Pobranie App Settings przez PowerShell:
  `Get-AzWebApp -ResourceGroup rg -Name myapp | Get-AzWebAppConfig`

## Przykład kodu C# (.NET 8)
```csharp
var builder = WebApplication.CreateBuilder(args);
builder.Configuration.AddEnvironmentVariables();
var app = builder.Build();

app.MapGet("/", () => $"Hello from App Service! ENV: {Environment.GetEnvironmentVariable("ASPNETCORE_ENVIRONMENT")}");

app.Run();
```

```csharp
// Przykład 2: Użycie Managed Identity i App Settings
using Azure.Identity;
using Azure.Security.KeyVault.Secrets;

var builder = WebApplication.CreateBuilder(args);
builder.Configuration.AddEnvironmentVariables();
var keyVaultUrl = builder.Configuration["KeyVaultUrl"];
var secretClient = new SecretClient(new Uri(keyVaultUrl), new DefaultAzureCredential());
var app = builder.Build();
app.MapGet("/secret", async () =>
{
	var secret = await secretClient.GetSecretAsync("MySecret");
	return Results.Ok(secret.Value.Value);
});
app.Run();
```

## Wskazówka egzaminacyjna
- App Service nie obsługuje Windows Authentication.
- Ograniczenia planów Free/Shared (brak SSL, autoskalowania, Always On).
- Swap slotów nie przenosi ustawień slot-specific (np. connection strings oznaczonych jako slot setting).
- Managed Identity wymaga włączenia w ustawieniach aplikacji.
- Najczęstszy błąd: brak Always On powoduje usypianie aplikacji.
	- Częsty błąd: brak slot-specific settings lub nieprawidłowa konfiguracja Managed Identity.

---

