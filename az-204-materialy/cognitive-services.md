# Azure Cognitive Services
---

[Prev: Azure Notification Hubs](notification-hubs.md) | [Next: Azure API for FHIR](api-for-fhir.md)

**Definicja:**
- Zestaw usług AI (analiza obrazu, tekstu, mowy, tłumaczenia, rozpoznawanie twarzy).

**Znaczenie na egzaminie AZ-204:**
- Często pytania o wywołanie API, autoryzację, pricing.

## Kluczowe pojęcia
- **Resource** – instancja Cognitive Services (np. Vision, Speech).
- **Key/Endpoint** – klucz API i adres endpointu.
- **Pricing Tier** – poziom cenowy, limity.
- **SDK/REST API** – wywołania z poziomu kodu.

## Scenariusze egzaminacyjne
- Wywołanie API Vision, Text Analytics, Translator.
- Konfiguracja klucza i endpointu.
- Ograniczenia pricing tier.

## Przykład użycia
- Analiza obrazu przez REST API.
- Wykrywanie sentymentu przez SDK.

## Komendy
- Tworzenie Cognitive Services:
  `az cognitiveservices account create --name mycog --resource-group rg --kind TextAnalytics --sku S`

## Przykład kodu C# (.NET 8)
```csharp
using Azure.AI.TextAnalytics;
var client = new TextAnalyticsClient(new Uri(endpoint), new AzureKeyCredential(key));
var result = await client.AnalyzeSentimentAsync("To jest super!");
```

## Wskazówka egzaminacyjna
- Najczęstszy błąd: brak klucza lub zły endpoint.
- Pricing tier ogranicza liczbę wywołań na minutę.
