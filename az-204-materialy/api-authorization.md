

# Azure API Authorization
---

[Prev: VNet](vnet.md) | [Next: Deployment (Bicep)](deployment-bicep.md)

## Definicja
- Uwierzytelnianie (**authentication**) i autoryzacja (**authorization**) dostępu do API w Azure.
- Wsparcie dla **OAuth2**, **OpenID Connect**, **Azure AD**, **MSAL**.
- Możliwość ochrony API na poziomie aplikacji, gateway, funkcji.

## Znaczenie na AZ-204
- Bezpieczny dostęp do API, ochrona danych i operacji.
- Integracja z **Azure AD**, **App Service**, **Functions**, **API Management**.
- Wymuszanie uprawnień, ochrona przed nieautoryzowanym dostępem.
- Weryfikacja tożsamości użytkownika i aplikacji.

## Kluczowe pojęcia
- **OAuth2**: protokół autoryzacji, tokeny dostępu (access token).
- **OpenID Connect**: rozszerzenie OAuth2 o tożsamość użytkownika (id token).
- **Azure AD**: zarządzanie tożsamościami, federacja, SSO.
- **JWT**: tokeny autoryzacyjne, podpisane cyfrowo, zawierają claims.
- **Scopes**: zakresy uprawnień dla API, np. api.read, api.write.
- **Audience**: identyfikator API, dla którego wydano token.
- **Authority**: adres serwera uwierzytelniania (np. login.microsoftonline.com).
- **Claims**: dane w tokenie JWT (np. sub, roles, exp).
- **MSAL**: biblioteka do pobierania tokenów w aplikacjach klienckich.
- **App registration**: rejestracja aplikacji w Azure AD, generuje clientId.
- **Client secret/certificate**: dane uwierzytelniające aplikację.
- **[Authorize]**: atrybut wymuszający autoryzację w .NET.
- **Middleware**: komponent pośredniczący w obsłudze żądań HTTP.

## Scenariusze egzaminacyjne
- Konfiguracja autoryzacji JWT w .NET 8 (Web API, minimal API).
- Ochrona endpointów przez [Authorize] i role-based access.
- Integracja z Azure AD (rejestracja aplikacji, nadanie uprawnień API).
- Weryfikacja tokena JWT (aud, iss, exp, signature).
- Ochrona API Management przez Azure AD.
- Ustawienie scope w żądaniu klienta.
- Obsługa błędów autoryzacji (401, 403).

## Przykład użycia
- API chronione przez Azure AD (Web API, Functions, Logic Apps).
- Weryfikacja tokena JWT w .NET 8.
- Pobranie tokena przez MSAL w aplikacji klienckiej.

## Komendy
- Rejestracja aplikacji w Azure AD:
  Portal Azure > Azure Active Directory > Rejestracje aplikacji > Nowa rejestracja
- Pobranie clientId, tenantId, secret.
- Nadanie uprawnień API: Portal > Expose an API > Add scope
- Pobranie tokena przez CLI:
  `az account get-access-token --resource api://{clientId}`

## Przykład kodu C# (.NET 8)
```csharp
using Microsoft.AspNetCore.Authentication.JwtBearer;
using Microsoft.Identity.Web;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
  .AddMicrosoftIdentityWebApi(builder.Configuration.GetSection("AzureAd"));

builder.Services.AddAuthorization(options =>
{
  options.AddPolicy("AdminOnly", policy => policy.RequireRole("Admin"));
});

var app = builder.Build();
app.UseAuthentication();
app.UseAuthorization();
app.MapGet("/secure", [Authorize] () => "Tylko dla zalogowanych");
app.MapGet("/admin", [Authorize(Policy = "AdminOnly")] () => "Tylko admin");
```

appsettings.json:
```json
"AzureAd": {
  "Instance": "https://login.microsoftonline.com/",
  "Domain": "contoso.onmicrosoft.com",
  "TenantId": "{tenantId}",
  "ClientId": "{clientId}",
  "Audience": "api://{clientId}"
}
```

## Wskazówka egzaminacyjna
- **Audience** i **Authority** muszą być zgodne z rejestracją w Azure AD.
- Brak [Authorize] = endpoint publiczny.
- Token JWT ma określony czas życia (**exp**), po wygaśnięciu żądanie zostanie odrzucone.
- **Scopes** muszą być zgodne z deklaracją API.
- Najczęstszy błąd: nieprawidłowy audience lub brak uprawnień w tokenie.
- Claims są weryfikowane automatycznie przez middleware.


---

