# Azure API Authorization

- Uwierzytelnianie i autoryzacja API w Azure.
- Wsparcie dla OAuth2, OpenID Connect, Azure AD.
- Integracja z App Service, Functions, API Management.

## Przykład C# (.NET 8, autoryzacja JWT)

```csharp
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer(options =>
    {
        options.Authority = "https://login.microsoftonline.com/{tenantId}/v2.0";
        options.Audience = "api://{clientId}";
    });
```

- Użycie Microsoft.AspNetCore.Authentication.JwtBearer.
- Konfiguracja w DI.
- Wsparcie dla Azure AD.

---

[Prev: VNet](vnet.md) | [Next: Deployment (Bicep)](deployment-bicep.md)
