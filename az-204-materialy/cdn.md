

# Azure CDN
---

[Prev: Azure Functions](azure-functions.md) | [Next: Blob Storage](blob-storage.md)

## Definicja
- Usługa Content Delivery Network do przyspieszania dostarczania treści.
- Cache'owanie plików statycznych blisko użytkownika.

## Znaczenie na AZ-204
- Zmniejsza opóźnienia i obciążenie backendu.
- Wspiera globalne aplikacje, poprawia wydajność.

## Kluczowe pojęcia
- **Endpoint**: punkt wejścia CDN, przypisany do domeny.
- **Origin**: źródło plików (Blob Storage, App Service).
- **Caching rules**: reguły cache, TTL.
- **Custom domain**: własna domena dla CDN.
- **HTTPS**: obsługa certyfikatów SSL.
- Dostawcy: Microsoft, Akamai, Verizon.

## Scenariusze egzaminacyjne
- Konfiguracja CDN dla statycznych plików z Blob Storage.
- Podpięcie własnej domeny i certyfikatu SSL.
- Ustawienie reguł cache.

## Przykład użycia
- Konfiguracja endpointu przez portal.
- Przypisanie custom domain.

## Komendy
- Tworzenie CDN:
	`az cdn profile create --name mycdn --resource-group rg --sku Standard_Microsoft`
- Tworzenie endpointu:
	`az cdn endpoint create --name myendpoint --profile-name mycdn --resource-group rg --origin mystorage.blob.core.windows.net`

## Przykład kodu C# (.NET 8)
```csharp
// Przykład: Purge (czyszczenie cache) endpointu CDN przez REST API
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text.Json;
using System.Threading.Tasks;

public class CdnPurgeExample
{
	public async Task PurgeCdnAsync(string subscriptionId, string resourceGroup, string profileName, string endpointName, string bearerToken)
	{
		using var client = new HttpClient();
		client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
		var url = $"https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/purge?api-version=2021-06-01";
		var body = JsonSerializer.Serialize(new { contentPaths = new[] { "/images/*" } });
		var response = await client.PostAsync(url, new StringContent(body, System.Text.Encoding.UTF8, "application/json"));
		response.EnsureSuccessStatusCode();
	}
}
```

## Wskazówka egzaminacyjna
- CDN nie przechowuje plików, tylko je cache'uje.
- Zmiana pliku w origin nie od razu aktualizuje cache.
- HTTPS wymaga aktywacji i propagacji certyfikatu.


---

