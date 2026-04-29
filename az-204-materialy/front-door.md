

# Azure Front Door
---

[Prev: Event Hub](event-hub.md) | [Next: Key Vault](key-vault.md)

- Globalny load balancer i akcelerator aplikacji (warstwa 7).
- Wsparcie dla SSL/TLS, WAF (Web Application Firewall), cache, health probes.
- Integracja z App Service, CDN, Storage, API Management.

## Znaczenie na AZ-204
- Zapewnia wysoką dostępność i niskie opóźnienia globalnie.
- Chroni aplikacje przez WAF, SSL, geo-filtering.
- Umożliwia routing na podstawie ścieżki, hosta, geolokalizacji.

## Kluczowe pojęcia
- **Frontend**: publiczny adres URL Front Door.
- **Backend Pool**: lista endpointów (np. App Service, VM).
- **Routing Rule**: reguła kierująca ruch do backendu (możliwość zaawansowanego routingu: path-based, geo, host).
- **Health Probe**: monitorowanie dostępności backendów (konfigurowalne: path, interval, protocol, probe method).
- **WAF**: ochrona przed atakami (np. SQLi, XSS, OWASP Top 10, custom rules).
- **Session Affinity**: utrzymanie sesji użytkownika (cookie-based).
- **Caching**: przyspieszenie dostarczania treści (możliwość wyłączenia dla dynamicznych endpointów).
- **Custom Domain**: własna domena z SSL (wymaga walidacji i przypisania certyfikatu).
- **URL Rewrite/Redirect**: modyfikacja adresów URL (np. przekierowanie HTTP→HTTPS).
## Zaawansowane scenariusze
- WAF z własnymi regułami (custom rules).
- Routing geo-based (na podstawie kraju użytkownika).
- Failover do innego regionu przy niedostępności backendu.
- Health probe z niestandardową ścieżką i metodą.
## Typowe pułapki egzaminacyjne
- Brak health probe = backend zawsze uznany za niedostępny.
- WAF wymaga przypisania do Front Door, samo utworzenie nie wystarczy.
- Front Door nie obsługuje TCP/UDP – tylko HTTP/HTTPS.
- Custom domain wymaga poprawnej konfiguracji DNS i SSL.

## Scenariusze egzaminacyjne
- Konfiguracja globalnego load balancera dla App Service.
- Włączenie WAF i SSL dla aplikacji.
- Routing na podstawie ścieżki lub hosta.
- Konfiguracja health probe i failover.
- Ustawienie cache dla statycznych zasobów.

## Przykład kodu C# (.NET 8)
```csharp
// Przykład: Pobranie konfiguracji Front Door przez REST API
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

public class FrontDoorExample
{
	public async Task<string> GetFrontDoorConfigAsync(string subscriptionId, string resourceGroup, string frontDoorName, string bearerToken)
	{
		using var client = new HttpClient();
		client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
		var url = $"https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Network/frontDoors/{frontDoorName}?api-version=2021-06-01";
		var response = await client.GetAsync(url);
		response.EnsureSuccessStatusCode();
		return await response.Content.ReadAsStringAsync();
	}
}
```

// Konfiguracja przez portal Azure lub ARM/Bicep.
// Ustawienie reguł routingu, SSL, WAF.
// Przekierowanie ruchu na podstawie ścieżki.
// Przykład ARM/Bicep:
```bicep
resource fd 'Microsoft.Network/frontDoors@2021-06-01' = {
	name: 'myFrontDoor'
	location: 'global'
	properties: {
		frontendEndpoints: [
			{
				name: 'myFrontend'
				properties: {
					hostName: 'myapp.azurefd.net'
				}
			}
		]
		backendPools: [
			{
				name: 'myBackendPool'
				properties: {
					backends: [
						{
							address: 'myapp.azurewebsites.net'
							httpPort: 80
							httpsPort: 443
						}
					]
				}
			}
		]
		routingRules: [
			{
				name: 'routeAll'
				properties: {
					frontendEndpoints: [
						{
							id: fd.frontendEndpoints[0].id
						}
					]
					acceptedProtocols: [ 'Http', 'Https' ]
					patternsToMatch: [ '/*' ]
					routeConfiguration: {
						odata.type: '#Microsoft.Network.FrontDoor.ForwardingConfiguration'
						backendPool: {
							id: fd.backendPools[0].id
						}
					}
				}
			}
		]
	}
}
```

## Komendy
- Tworzenie Front Door:
	`az network front-door create --resource-group rg --name myfd --backend-address app.azurewebsites.net`
- Dodanie custom domain:
	`az network front-door frontend-endpoint create --resource-group rg --front-door-name myfd --name mydomain --host-name www.mydomain.com`
- Włączenie WAF:
	`az network front-door waf-policy create --resource-group rg --name mywaf`
- Przypisanie WAF do Front Door:
	`az network front-door waf-policy update --resource-group rg --front-door-name myfd --policy-name mywaf`

## Wskazówka egzaminacyjna
- Front Door działa na warstwie 7 (HTTP/HTTPS), nie obsługuje TCP/UDP.
- Najczęstszy błąd: brak health probe lub zła konfiguracja backend pool.
- WAF wymaga osobnej konfiguracji i przypisania do Front Door.
- Przypisanie custom domain wymaga poprawnej konfiguracji DNS i walidacji SSL.
- Health probe musi być poprawnie ustawiony – domyślnie /, ale można zmienić na /health.
- Routing path-based wymaga unikalnych wzorców dla każdej reguły.

## Przykład użycia

- Konfiguracja przez portal Azure.
- Ustawienie reguł routingu i SSL.
- Brak kodu C#, konfiguracja graficzna.

---

