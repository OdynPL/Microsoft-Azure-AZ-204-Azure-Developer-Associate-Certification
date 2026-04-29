

# Azure API Management
---

[Prev: App Configuration](app-configuration.md) | [Next: Application Insights](application-insights.md)

## Definicja
- Usługa do zarządzania, zabezpieczania i monitorowania API.
- Tworzy **API Gateway**, publikuje API, wymusza polityki, udostępnia dokumentację.
- Umożliwia wersjonowanie, testowanie, limitowanie i transformację żądań.

## Znaczenie na AZ-204
- Centralny punkt zarządzania API, ochrona i monitoring.
- Wsparcie dla limitów, autoryzacji, cache, transformacji.
- Integracja z Azure AD, OAuth2, OpenID Connect.
- Ułatwia publikację API dla deweloperów i partnerów.

## Kluczowe pojęcia
- **API Gateway**: pośrednik między klientem a backendem, centralny punkt wejścia.
- **Polityki**: reguły XML (np. limit, rewrite, transformacja, cache, CORS, JWT validation).
- **Product**: grupowanie API, zarządzanie dostępem, publikacja do wybranych użytkowników.
- **Subscription**: klucz dostępu do API, wymuszanie limitów i autoryzacji.
- **Developer Portal**: portal do dokumentacji, testowania i rejestracji aplikacji.
- **Named Value**: zmienne konfiguracyjne używane w politykach.
- **Revision**: wersjonowanie API bez przerywania działania.
- **Version**: obsługa wielu wersji API (np. v1, v2).
- **Backend**: docelowy serwis obsługujący żądania (np. App Service, Function, Logic App).
- **Logger**: integracja z Application Insights, logowanie żądań.
- **Policy Expressions**: C#-like expressions w politykach.
- **Rate limit**: ograniczenie liczby żądań na klucz/subskrypcję.
- **Quota**: limit liczby żądań w określonym czasie.

**Kluczowe pojęcia dodatkowe:**
- **Inbound/Outbound policy** – polityki przetwarzania żądań przed i po backendzie.
- **SOAP passthrough** – wsparcie dla SOAP przez API Management.
- **Mock API** – symulacja odpowiedzi bez backendu.

## Scenariusze egzaminacyjne
- Import API przez OpenAPI, Swagger, WSDL.
- Konfiguracja polityk (rate-limit, rewrite, JWT validation, CORS, cache, transformacja nagłówków).
- Publikacja API do developer portal, testowanie endpointów.
- Ochrona API przez subskrypcje, wymuszanie klucza.
- Integracja z Azure AD (OAuth2, OpenID Connect).
- Wersjonowanie i rewizje API.
- Ustawienie named values i ich użycie w politykach.
- Logowanie żądań do Application Insights.

## Przykład użycia
- Import API przez portal lub CLI.
- Dodanie polityki limitu żądań (rate-limit-by-key):
```xml
<rate-limit-by-key calls="10" renewal-period="60" counter-key="@(context.Subscription.Id)" />
```
- Walidacja JWT:
```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" require-scheme="Bearer">
	<openid-config url="https://login.microsoftonline.com/{tenantId}/v2.0/.well-known/openid-configuration" />
	<audiences>
		<audience>api://{clientId}</audience>
	</audiences>
</validate-jwt>
```
- Transformacja nagłówka:
```xml
<set-header name="X-Api-Version" exists-action="override">
	<value>v2</value>
</set-header>
```

## Komendy
- Tworzenie API Management:
	`az apim create --name myapim --resource-group rg --publisher-email admin@contoso.com --publisher-name Contoso`
- Import API:
	`az apim api import --resource-group rg --service-name myapim --path myapi --specification-format OpenApi --specification-path openapi.json`
- Dodanie polityki:
	Portal > API > Design > Inbound processing > Add policy
- Pobranie klucza subskrypcji:
	Portal > API Management > Subscriptions

- Pobranie subskrypcji przez PowerShell:
  `Get-AzApiManagementSubscription -ResourceGroupName rg -ServiceName myapim`

## Przykład kodu C# (.NET 8)
// Konfiguracja po stronie API (np. walidacja JWT):
```csharp
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
	.AddJwtBearer(options =>
	{
		options.Authority = "https://login.microsoftonline.com/{tenantId}/v2.0";
		options.Audience = "api://{clientId}";
	});
```

```csharp
// Przykład 2: Weryfikacja subskrypcji i limitów po stronie backendu
using Microsoft.AspNetCore.Mvc;

var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();
app.MapGet("/data", ([FromHeader(Name = "Ocp-Apim-Subscription-Key")] string subscriptionKey) =>
{
    if (string.IsNullOrEmpty(subscriptionKey))
        return Results.Unauthorized();
    // Tu można dodać logikę limitowania lub walidacji klucza
    return Results.Ok("Dane tylko dla subskrybentów");
});
app.Run();
```

- Polityki są deklaratywne (XML), nie kod.
- Najczęstszy błąd: brak subskrypcji lub nieprawidłowy klucz.
- Polityki walidacji JWT wymagają poprawnego audience i issuer.
- Developer Portal można dostosować i wyłączyć publiczny dostęp.
- Wersjonowanie API nie przerywa działania istniejących klientów.
- Subskrypcje mogą być wymagane do wywołania API.
- Developer Portal można dostosować.

	- Częsty błąd: brak polityki rate-limit lub quota.
	- Mock API nie wymaga backendu – przydatne do testów.


---

