

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

## Przykład kodu
Brak — konfiguracja przez portal lub CLI.

## Wskazówka egzaminacyjna
- CDN nie przechowuje plików, tylko je cache'uje.
- Zmiana pliku w origin nie od razu aktualizuje cache.
- HTTPS wymaga aktywacji i propagacji certyfikatu.


---

