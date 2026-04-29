# Azure Private Link
---

[Prev: Azure Blueprints](blueprints.md) | [Next: API Versioning](api-versioning.md)

**Definicja:**
- **Azure Private Link** – umożliwia prywatny dostęp do usług PaaS przez sieć VNet, bez publicznego IP.

**Znaczenie na egzaminie AZ-204:**
- Pytania o bezpieczeństwo, izolację ruchu, dostęp do usług z VNet.

## Kluczowe pojęcia
- **Private Endpoint** – prywatny adres IP w VNet dla usługi.
- **Private Link Service** – własna usługa publikowana przez Private Link.
- **DNS Integration** – przekierowanie nazw na prywatne IP.

## Scenariusze egzaminacyjne
- Dostęp do Azure SQL, Storage, Web App przez VNet.
- Ograniczenie dostępu do usług tylko z prywatnej sieci.

## Przykład użycia
- Tworzenie Private Endpoint dla Storage przez CLI.

## Komendy
- Tworzenie Private Endpoint:
  `az network private-endpoint create --name myEndpoint --resource-group myRG --vnet-name myVNet --subnet mySubnet --private-connection-resource-id /subscriptions/.../resourceGroups/.../providers/Microsoft.Storage/storageAccounts/myStorage --group-ids blob`

## Przykład kodu C# (.NET 8)
```csharp
// Sprawdzenie czy połączenie pochodzi z Private Endpoint (np. w Web API)
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Http;

public class PrivateLinkController : ControllerBase
{
  [HttpGet("/check-private-link")]
  public IActionResult CheckPrivateLink()
  {
    var remoteIp = HttpContext.Connection.RemoteIpAddress;
    // Załóżmy, że Private Endpoint jest w zakresie 10.0.0.0/24
    if (remoteIp != null && remoteIp.ToString().StartsWith("10.0.0."))
      return Ok("Połączenie przez Private Endpoint");
    return Forbid();
  }
}
```

## Wskazówka egzaminacyjna
- Private Link ≠ Service Endpoint (Private Link = prywatny IP, Service Endpoint = routing przez backbone).
- Najczęstszy błąd: mylenie pojęć i zakresów działania.
