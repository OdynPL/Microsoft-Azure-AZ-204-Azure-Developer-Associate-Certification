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

## Scenariusze egzaminacyjne
- Dodanie nowej wersji API bez przerywania działania starej.
- Przekierowanie ruchu do odpowiedniej wersji.

## Przykład użycia
- Definiowanie wersji w Azure API Management.

## Komendy
- Dodanie wersji w API Management:
  https://learn.microsoft.com/en-us/azure/api-management/api-management-get-started-create-versions

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

## Wskazówka egzaminacyjna
- Najczęstszy błąd: brak obsługi wersji w kliencie lub mylenie sposobów wersjonowania.
