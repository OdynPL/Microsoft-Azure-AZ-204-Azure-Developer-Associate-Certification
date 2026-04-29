
# Azure Front Door

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
- **Routing Rule**: reguła kierująca ruch do backendu.
- **Health Probe**: monitorowanie dostępności backendów.
- **WAF**: ochrona przed atakami (np. SQLi, XSS).
- **Session Affinity**: utrzymanie sesji użytkownika.
- **Caching**: przyspieszenie dostarczania treści.
- **Custom Domain**: własna domena z SSL.
- **URL Rewrite/Redirect**: modyfikacja adresów URL.

## Scenariusze egzaminacyjne
- Konfiguracja globalnego load balancera dla App Service.
- Włączenie WAF i SSL dla aplikacji.
- Routing na podstawie ścieżki lub hosta.
- Konfiguracja health probe i failover.
- Ustawienie cache dla statycznych zasobów.

## Przykład użycia
- Konfiguracja przez portal Azure lub ARM/Bicep.
- Ustawienie reguł routingu, SSL, WAF.
- Przekierowanie ruchu na podstawie ścieżki.

## Komendy
- Tworzenie Front Door:
	`az network front-door create --resource-group rg --name myfd --backend-address app.azurewebsites.net`
- Dodanie custom domain:
	`az network front-door frontend-endpoint create --resource-group rg --front-door-name myfd --name mydomain --host-name www.mydomain.com`
- Włączenie WAF:
	`az network front-door waf-policy create --resource-group rg --name mywaf`

## Wskazówka egzaminacyjna
- Front Door działa na warstwie 7 (HTTP/HTTPS), nie obsługuje TCP/UDP.
- Najczęstszy błąd: brak health probe lub zła konfiguracja backend pool.
- WAF wymaga osobnej konfiguracji i przypisania do Front Door.

## Przykład użycia

- Konfiguracja przez portal Azure.
- Ustawienie reguł routingu i SSL.
- Brak kodu C#, konfiguracja graficzna.

---

[Prev: Event Hub](event-hub.md) | [Next: Key Vault](key-vault.md)
