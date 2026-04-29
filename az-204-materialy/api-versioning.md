# API Versioning
---

[Prev: Azure Private Link](private-link.md) | [Next: Azure Managed Disks](managed-disks.md)

**Definicja:**
- **API Versioning** – technika zarządzania wersjami API (np. REST) w Azure.

**Znaczenie na egzaminie AZ-204:**
- Pytania o sposoby wersjonowania, obsługę wielu wersji API.

## Kluczowe pojęcia
- **URL versioning** – wersja w ścieżce (np. /v1/).
- **Query string versioning** – wersja jako parametr (np. ?api-version=1.0).
- **Header versioning** – wersja w nagłówku HTTP.
- **Azure API Management** – obsługuje wersjonowanie API.

**Kluczowe pojęcia dodatkowe:**
- **Backward compatibility** – zachowanie zgodności wstecznej.
- **Deprecation** – oznaczanie wersji jako przestarzałej.
- **Default version** – domyślna wersja API.

## Scenariusze egzaminacyjne
- Dodanie nowej wersji API bez przerywania działania starej.
- Przekierowanie ruchu do odpowiedniej wersji.

## Przykład użycia
- Definiowanie wersji w Azure API Management.

## Komendy
- Dodanie wersji w API Management:
  https://learn.microsoft.com/en-us/azure/api-management/api-management-get-started-create-versions

- Pobranie wersji API przez PowerShell:
  `Invoke-RestMethod -Uri "https://myapi.azure-api.net/resource?api-version=2.0"`

## Przykład kodu C# (.NET 8)
```csharp
[ApiVersion("1.0")]
[Route("api/v{version:apiVersion}/[controller]")]
public class SampleController : ControllerBase
{
    [HttpGet]
    public IActionResult GetV1() => Ok("v1");
}
```

```csharp
// Przykład 2: Wersjonowanie przez query string i nagłówek
using Microsoft.AspNetCore.Mvc;

[ApiVersion("2.0")]
[Route("api/[controller]")]
public class SampleV2Controller : ControllerBase
{
  [HttpGet]
  public IActionResult GetV2() => Ok("v2");
}

// Startup:
builder.Services.AddApiVersioning(options =>
{
  options.AssumeDefaultVersionWhenUnspecified = true;
  options.DefaultApiVersion = new ApiVersion(1, 0);
  options.ApiVersionReader = ApiVersionReader.Combine(
    new QueryStringApiVersionReader("api-version"),
    new HeaderApiVersionReader("x-api-version")
  );
});
```

## Wskazówka egzaminacyjna
- Najczęstszy błąd: brak obsługi wersji w kliencie lub mylenie sposobów wersjonowania.
  - Częsty błąd: brak domyślnej wersji lub nieoznaczenie przestarzałej wersji.
